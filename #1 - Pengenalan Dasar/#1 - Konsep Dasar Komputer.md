# 🧩 #1 - Konsep Dasar Komputer

Sebelum menjelajah dunia virtualisasi, kita perlu kenal dulu dengan "dunia nyata" alias perangkat keras dan perangkat lunak dasar. Ini seperti belajar mengenali isi ransel dan perlengkapan sebelum naik gunung! 🏔️🎒

---

## 🖥️ Apa Itu Komputer?

Komputer adalah alat elektronik yang memproses data menjadi informasi yang berguna. Tapi jangan salah, komputer itu bukan cuma laptop lho! Ada juga:

- 💼 **Laptop/PC** — untuk pengguna umum
- 🏢 **Server** — komputer khusus untuk melayani komputer lain
- ⚙️ **Embedded System** — seperti komputer mini di mesin cuci, mobil, dll

---

## 🧱 Komponen Dasar Komputer

Mari kita ibaratkan komputer seperti **sebuah pabrik mini** 🏭:

| Komponen | Fungsi | Analogi |
|----------|--------|---------|
| **CPU** (Processor) | Otak utama | Manajer pabrik yang mengatur semuanya |
| **RAM** | Penyimpanan sementara | Meja kerja tempat proses cepat dilakukan |
| **Storage** (HDD/SSD) | Penyimpanan permanen | Gudang tempat menyimpan barang |
| **Motherboard** | Papan sirkuit utama | Lantai dan jalur penghubung antar bagian |
| **PSU** (Power Supply) | Sumber listrik | Generator listrik internal |
| **Cooling** | Pendingin | Kipas atau AC pabrik supaya tidak overheat |

> 💡 *Server biasanya pakai komponen yang tahan kerja keras dan hidup 24 jam nonstop.*

---

## 📀 Sistem Operasi (OS)

Setelah pabrik siap, dibutuhkan **manajer software** yang mengatur semuanya. Itulah peran sistem operasi seperti:

- 🪟 **Windows** — umum untuk pengguna pribadi
- 🐧 **Linux** — stabil, gratis, sering dipakai server
- 🍏 **macOS** — eksklusif untuk perangkat Apple

> Untuk server dan Proxmox, **Linux lebih umum digunakan** karena ringan dan fleksibel.

---

## 🌐 Server: Komputer yang Melayani

Server itu seperti **restoran dapur besar** 🍽️ — tidak makan sendiri, tapi melayani banyak tamu (komputer lain).

Contoh server:
- 🌐 Web server (melayani website)
- 📧 Mail server (melayani email)
- 🗃️ File server (berbagi file)
- ☁️ Virtualization server (menjalankan VM dan container — ini tugas Proxmox!)

---

## 🔧 Bare Metal vs Virtual

| Istilah | Artinya |
|--------|---------|
| **Bare Metal** | Menjalankan sistem langsung di atas perangkat keras fisik |
| **Virtual Machine (VM)** | Sistem operasi yang dijalankan di dalam software virtual |
| **Container (CT)** | Sistem ringan yang berjalan di atas OS utama, lebih efisien dari VM |

> ⚖️ *Virtualisasi memungkinkan kamu menjalankan banyak sistem dalam satu mesin fisik — itulah yang bikin hemat dan fleksibel!*

---

## ✨ Rangkuman

- Komputer/server terdiri dari beberapa komponen utama.
- OS berperan mengatur kerja perangkat.
- Server berfungsi untuk **melayani pengguna lain**, bukan untuk penggunaan pribadi.
- Dunia virtualisasi memungkinkan **satu komputer jadi banyak server kecil** secara efisien.

---

✅ Setelah kamu memahami bagian ini, kita bisa lanjut ke dunia virtualisasi lebih dalam!

🔗 Lanjut ke [#2 - Apa Itu Virtualisasi.md](./#2%20-%20Apa%20Itu%20Virtualisasi.md)
