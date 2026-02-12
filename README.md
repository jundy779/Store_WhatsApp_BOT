<div align="center">

<!-- Wave Header -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=215&section=header&text=Fusionify%20BOT&fontSize=78&fontAlignY=35&animation=twinkling&fontColor=fff&desc=Store-First%20WhatsApp%20Bot%20%7C%20Group%20Management%20%7C%20Web%20Monitor&descAlignY=58&descSize=18" width="100%" />

<img src="https://files.catbox.moe/3xv7p0.png" width="180" alt="Fusionify Bot" />

_🌸 Fusionify_  
**FTV BOT — Store-First WhatsApp Bot (Premium)**  
_Store List dulu, baru grup jadi rapih._ (≧◡≦) ♡

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-18%2B-3c873a?style=for-the-badge&logo=node.js&logoColor=white" alt="node">
  <img src="https://img.shields.io/badge/MongoDB-Supported-4db33d?style=for-the-badge&logo=mongodb&logoColor=white" alt="mongodb">
  <img src="https://img.shields.io/badge/WhatsApp-Bot-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="whatsapp">
  <img src="https://img.shields.io/badge/Type-Premium-111827?style=for-the-badge" alt="premium">
</p>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

</div>

<div align="center">
  <sub>Built on Baileys • Written in JavaScript • Designed for store sellers & admins</sub>
  <br/>
  <sub>
    <a href="#-overview">Overview</a> •
    <a href="#-paket--harga">Harga</a> •
    <a href="#-store-list-fokus-utama">Store List</a> •
    <a href="#-highlight-command-asli-dari-bot">Commands</a> •
    <a href="#-order--kerja-sama">Order</a>
  </sub>
</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🚀 Overview

Fusionify BOT adalah bot WhatsApp premium yang fokusnya jelas: **STORE LIST dulu**, lalu manajemen grup, dan monitoring.

<table>
  <tr>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/Tarikul-Islam-Anik/Animated-Fluent-Emojis/master/Emojis/Activities/Shopping%20Bags.png" width="50" alt="Store"/>
      <br/>
      <b>Store List</b><br/>
      keyword auto-reply<br/>
      status order + feedback<br/>
      open / close
    </td>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/Tarikul-Islam-Anik/Animated-Fluent-Emojis/master/Emojis/Objects/Locked.png" width="50" alt="Group"/>
      <br/>
      <b>Group Management</b><br/>
      anti suite<br/>
      welcome & rules<br/>
      admin tools
    </td>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/Tarikul-Islam-Anik/Animated-Fluent-Emojis/master/Emojis/Objects/Bar%20Chart.png" width="50" alt="Monitor"/>
      <br/>
      <b>Web Monitor</b><br/>
      realtime stats<br/>
      logs + sewa list<br/>
      command usage
    </td>
  </tr>
</table>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 💎 Paket & Harga
<div align="center">

<table>
  <tr>
    <th align="left">Paket</th>
    <th align="left">Harga</th>
  </tr>
  <tr>
    <td><b>Sewa Bot</b> (per grup)</td>
    <td><b>7K / bulan</b></td>
  </tr>
  <tr>
    <td><b>Source Code (SC)</b></td>
    <td><b>180K</b> (sekali bayar)</td>
  </tr>
</table>

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🛍️ Store List (Fokus Utama)
<table>
  <tr>
    <td align="center" width="33%">
      <b>📋 List Produk</b><br/>
      Auto-reply keyword<br/>
      Support gambar<br/>
      Anti typo (smart match)
    </td>
    <td align="center" width="33%">
      <b>🧾 Status Order</b><br/>
      proses / done<br/>
      batal / refund<br/>
      feedback per item
    </td>
    <td align="center" width="33%">
      <b>💳 Store Tools</b><br/>
      payment (QRIS/e-wallet)<br/>
      struk + PDF<br/>
      testimonial
    </td>
  </tr>
</table>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🛡️ Manajemen Grup
<table>
  <tr>
    <td align="center" width="33%">
      <b>🚫 Anti Suite</b><br/>
      antilink, antiforward<br/>
      antispam, antidelete<br/>
      antivirtex, antitoxic
    </td>
    <td align="center" width="33%">
      <b>👋 Welcome & Rules</b><br/>
      welcome, left<br/>
      rules management<br/>
      mute/restrict
    </td>
    <td align="center" width="33%">
      <b>🧰 Admin Tools</b><br/>
      hidetag, pin, poll<br/>
      kick/add/promote<br/>
      votekick
    </td>
  </tr>
</table>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🏗️ Architecture (High-level)

```mermaid
flowchart TD
  A[User Message] --> B[Baileys Client]
  B --> C[Message Handler]
  C --> D{Command Parser}
  D -->|Store List| E[Store Engine]
  D -->|Group Command| F[Group Engine]
  D -->|Owner/Tools| G[Owner & Utility]
  E --> H[(MongoDB)]
  F --> H
  C --> I[Web Monitor]
  I --> H
```

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🧩 Highlight Command (Asli dari Bot)

<details>
<summary><b>Klik untuk lihat daftar command</b> (≧◡≦) ♡</summary>

<br/>

**Store List**
- `list`, `addlist`, `updatelist`, `dellist`, `dellistno`, `viewlist`, `previewlist`
- `proses` / `p`, `done` / `d`, `batal` / `b`, `refund` / `r`
- `feedback`, `storestats` / `stats`, `open`, `close`

**Payment**
- `paymentdl`, `setpayment`, `updatepayment`, `delpayment`

**Struk**
- `struk`, `laporadmin`, `getpdf`

**Testimonial**
- `testi`, `addtesti`, `deltesti`, `settesti`, `exporttesti`, `importtesti`

**Grup**
- `antilink`, `antiforward`, `antispam`, `antidelete`, `antivirtex`, `antitoxic`, `antiviewonce`, `antimedia`, `antiforeign`
- `welcome`, `rules`, `mute`, `hidetag`, `kick`, `add`, `promote`, `demote`, `pin`, `poll`, `votekick`

**Sewa (Owner)**
- `addsewa`, `renewsewa`, `ceksewa`, `listsewa`, `cekexpired`, `delsewa`

</details>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 📩 Order / Kerja Sama
<div align="center">

**Minat sewa / beli SC? Yuk chat sekarang~** (｡•̀ᴗ-)✧

<a href="https://t.me/TempestVPNOfficial">
  <img src="https://img.shields.io/badge/Telegram-@TempestVPNOfficial-26A5E4?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram">
</a>
<a href="https://wa.me/6285156218249">
  <img src="https://img.shields.io/badge/WhatsApp-6285156218249-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp">
</a>

<br/>
<sub>Fast response • Bisa tanya dulu kok • Jangan malu~ (≧◡≦) ♡</sub>

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🔒 Lisensi & Distribusi
Repo ini adalah **halaman publik** untuk informasi & showcase.  
Kode/SC tetap **private** dan hanya dibagikan via jalur resmi.
- Dilarang re-upload / re-sell / claim ownership tanpa izin
- Dilarang membagikan file SC ke publik

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=120&section=footer&text=Thank%20You!&fontSize=40&fontColor=ffffff&animation=twinkling&fontAlignY=75" width="100%" alt="Footer"/>
</div>
