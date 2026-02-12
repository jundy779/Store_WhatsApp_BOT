# Technical Overview — Fusionify BOT

## 1. Stack & Runtime
- Runtime: Node.js (ESM)
- WhatsApp library: Baileys (`@rexxhayanasi/elaina-baileys`)
- Persistence:
  - JSON lokal (`global.db`) untuk state umum
  - MongoDB (Mongoose) untuk data store/grup/sewa/settings/payment/dll
- Web monitor: server HTTP internal (dashboard + API) dengan token

## 2. Struktur Modul (High-level)
- `src/index.js`: bootstrap bot (init client, load db, load plugins, register events)
- `src/configs/plugins.js`: loader command (import dinamis + watch reload)
- `src/events/messages.js`: entry event WA messages → serialize → router handler
- `src/handler.js`: engine eksekusi plugin (permission, filters, before/execute)
- `commands/`: kumpulan command per kategori (`shop`, `group`, `owner`, dll)
- `src/models/`: Mongoose schema
- `src/lib/`: helper (group settings, command usage, monitor helpers, dll)

## 3. Alur Pesan (Runtime Flow)
1) WA event `messages.upsert` diterima.
2) Pesan diserialisasi menjadi object `m`.
3) Button handler diproses (jika ada).
4) Router/handler melakukan:
   - load default localdb shape ke `global.db`
   - filter: self mode, mute, banned, anti-spam, sewa, dll
5) Handler iterasi seluruh plugin:
   - `plugin.all(m)` (opsional)
   - `plugin.before(m)` (opsional)
   - match command (`plugin.cmd`) + cek permission → `plugin.execute(m, ctx)`

## 4. Store List Engine
Implementasi utama ada di `commands/shop/store.js`:
- `before()` menangani pesan non-command untuk auto-reply produk berdasarkan `key`.
- Command `list` membangun katalog + mengirim interactive picker.
- Store settings (header/footer/symbol/template/closeText/closeSticker) dibaca dari Mongo via helper group.

## 5. Group Settings
Ada dua jalur setting yang perlu distandarkan:
- Mongo `Group` (via `groupSchema` + `antiHelper.getGroup`)
- JSON lokal `global.db` (sebagian flag lama masih dicek di handler)

Rekomendasi teknis: definisikan satu “Settings Layer” sebagai source of truth per domain:
- Domain anti suite + store settings: Mongo `Group`
- Domain user counters/afk/temporary flags: JSON lokal

## 6. Database Model (Ringkas)
Mongo models (Mongoose) berada di `src/models`:
- `Store`: item per `groupId` + `key` (unique composite index)
- `Group`: anti-feature config + storeSettings per grup
- `Sewa`: masa aktif sewa per grup
- `Settings`: global settings + commandUsage
- `Payment`: metode pembayaran per grup
- Lainnya: transaction/autoResponse/dll sesuai kebutuhan command

## 7. Non-Functional Checklist (Engineering)
- Tidak boleh ada secret/token ke log.
- Semua akses owner/admin wajib via permission check.
- Hindari query berat per pesan; gunakan index/caching bila perlu.
- Refactor file besar secara bertahap ke modul util agar mudah dirawat.
- Hindari duplikasi logic: satukan helper (formatting, parsing args, validation).

## 8. Known Hotspots (Target Refactor)
- `commands/shop/store.js` sangat besar; pecah jadi modul:
  - `storeRepository` (query DB)
  - `storeRenderer` (template/header/footer/symbol)
  - `storeMatcher` (exact + smart match)
  - `storeCommands` (mapping command ke handler kecil)
- Inkonistensi settings: handler masih baca beberapa flag dari `global.db` sementara fitur modern di Mongo.
