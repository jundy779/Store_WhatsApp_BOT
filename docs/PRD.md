# PRD — Fusionify BOT (WA Store List)

## 1. Ringkasan
Fusionify BOT adalah bot WhatsApp premium yang berfokus pada fitur **Store List** (katalog produk berbasis keyword) untuk grup, dilengkapi tools toko (payment, struk, testimonial, hutang), manajemen & proteksi grup, sistem sewa per grup, dan web monitor.

## 2. Tujuan
- Mempercepat alur jualan di grup: user cukup ketik keyword produk → bot membalas detail produk secara konsisten.
- Memudahkan admin mengelola katalog dan status order (proses/done/batal/refund) tanpa ribet.
- Menjaga grup tetap rapi via proteksi anti suite dan tooling admin.
- Memberikan visibilitas operasional (monitor, logs, statistik penggunaan command).

## 3. Non-Goals (Di luar scope)
- Payment gateway otomatis (cek mutasi/settlement otomatis) dan rekonsiliasi transaksi.
- Sistem inventory/stock management yang kompleks.
- Marketplace multi-toko atau multi-tenant dashboard terpisah per user.

## 4. Persona & Hak Akses
- **Owner**: konfigurasi global, kelola sewa grup, monitoring, maintenance.
- **Admin Grup**: kelola store list di grup, set payment, atur proteksi grup.
- **Member/Buyer**: melihat katalog dan melakukan interaksi store (keyword produk, lihat testi, lihat payment).

## 5. Problem Statement
Jualan via grup sering tidak konsisten karena:
- katalog manual tercecer,
- jawaban admin tidak seragam,
- status order sulit dilacak,
- grup mudah spam/iklan,
- monitoring bot minim.

## 6. Ruang Lingkup Fitur

### 6.1 Store List (Core)
**Fitur utama**
- Katalog produk per grup berbasis `key` (keyword).
- Auto-reply saat member mengirim pesan yang cocok dengan `key` produk (tanpa prefix).
- Smart match (anti typo) untuk menyarankan produk terdekat.
- Produk bisa memiliki konten teks + media (mis. gambar).

**Manajemen katalog**
- Tambah/update/hapus item.
- Rename key.
- Preview list & view list.
- Template list (header/footer/symbol/fullTemplate).

**Status & operasional**
- Status item: `open/closed/processing/done/refunded/batal` (tergantung implementasi).
- Close message custom (teks dan/atau sticker) saat produk status `closed`.
- Feedback per item.
- Statistik store (mis. jumlah item/aktivitas/status).

### 6.2 Payment (Core Toko)
- Menampilkan metode pembayaran yang tersedia (QRIS/e-wallet).
- Admin dapat set/update/hapus metode pembayaran per grup.
- Pengalaman user: tombol copy/link untuk memudahkan pembayaran.

### 6.3 Struk (Core Toko)
- Generate struk digital untuk transaksi.
- Ekspor PDF.
- Tombol untuk lapor admin.
- Pembatasan akses (mis. premium/owner) sesuai kebijakan produk.

### 6.4 Testimonial (Core Toko)
- Menampilkan testimonial.
- Tambah/hapus testimonial.
- Export/import testimonial.
- Testimonial terikat pada item store (validasi key).

### 6.5 Hutang & Utility (Support)
- Catat hutang, edit, bayar, list.
- Kalkulator + konversi mata uang (support kebutuhan seller).

### 6.6 Manajemen & Proteksi Grup
- Proteksi anti suite (antilink/antiforward/antispam/antidelete/dll).
- Welcome, rules, mute/restrict, admin tools (kick/add/promote/demote/pin/poll/votekick).

### 6.7 Sistem Sewa Grup
- Sewa per grup dengan masa aktif.
- Reminder sebelum expired.
- Auto leave grup setelah expired (dengan grace period untuk renew).

### 6.8 Web Monitor
- Dashboard monitoring status proses (CPU/RAM/Disk/Network/Heap).
- Logs.
- Rekap sewa.
- Statistik pemakaian command.
- Auth token untuk akses dashboard.

## 7. Requirement Detail (Checklist)

### 7.1 Store List
- R1: Admin dapat menambah item store dengan key unik per grup.
- R2: Admin dapat update/hapus item store.
- R3: Bot merespons pesan non-command jika match key produk (case-insensitive).
- R4: Jika produk `closed`, bot mengirim close text/sticker sesuai setting grup.
- R5: Bot menyediakan command list untuk menampilkan katalog + picker produk.
- R6: Bot menyediakan fitur status order dan feedback per item.
- R7: Bot menyediakan statistik store untuk admin.

### 7.2 Payment
- R8: Admin dapat set/update/del metode pembayaran per grup.
- R9: User dapat melihat payment dengan UX yang cepat (copy/link).

### 7.3 Struk
- R10: Bot membuat struk dengan input terstruktur.
- R11: Bot dapat mengekspor PDF dan menyediakan tombol “lapor admin”.

### 7.4 Testimonial
- R12: User dapat melihat testimonial per item / list.
- R13: Admin dapat export/import testimonial.

### 7.5 Group Protection
- R14: Admin dapat enable/disable proteksi grup per fitur.
- R15: Proteksi memiliki action yang konsisten (delete/warn/kick) bila relevan.

### 7.6 Sewa
- R16: Owner dapat add/renew/del sewa per grup.
- R17: Bot melakukan reminder & auto leave sesuai aturan.

### 7.7 Monitor
- R18: Dashboard wajib dilindungi token.
- R19: Statistik command usage tidak boleh hilang saat restart/DB reconnect.

## 8. Data Model (Ringkas)
- **StoreItem**: `groupId`, `key`, `content`, `status`, `imageUrl`, metadata.
- **GroupSettings**: `groupId`, anti-feature flags, `storeSettings` (template, symbol, close text/sticker).
- **PaymentSettings**: `groupId`, method map (qris/dana/gopay/dll).
- **Sewa**: `groupId`, `expiredAt`, flags notifikasi.
- **Settings**: global settings + command usage.
- **Transaction** (opsional): catat aktivitas transaksi jika dipakai.

## 9. Non-Functional Requirements
- **Stabil**: bot tetap jalan jika Mongo belum siap; tidak kehilangan counter penting.
- **Performa**: query Mongo terindeks (key per group), beban per pesan minim.
- **Keamanan**: token monitor tidak boleh bocor/log; command owner dijaga ketat.
- **Maintainability**: clean code, minim duplikasi, modul jelas, testing minimal untuk fitur kritikal.

## 10. Risiko & Mitigasi
- Dual source of truth (JSON lokal vs Mongo) untuk setting → standardisasi layer settings.
- File command besar (mis. store) → refactor bertahap ke modul util.
- Flood message grup besar → caching settings + rate limit.

## 11. Metrik Keberhasilan
- Median waktu respon katalog/produk (P95) tetap rendah di grup rame.
- Error rate Mongo/query rendah.
- Peningkatan penggunaan fitur store list (storestats/command usage).
