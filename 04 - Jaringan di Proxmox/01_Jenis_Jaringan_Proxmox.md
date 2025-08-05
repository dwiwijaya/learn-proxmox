# 🌐 01 - Konsep Jaringan dalam Virtualisasi

Selamat datang di dunia **jaringan virtual**! 🎉  
Kalau sebelumnya kamu sudah jago bikin VM dan Container, sekarang kita belajar cara mereka bisa **berkomunikasi**—baik satu sama lain, maupun ke dunia luar (internet). 🌍

---

## 🎯 Tujuan Bab Ini

- Memahami konsep dasar jaringan di dunia virtual
- Mengenal **bridge**, **NAT**, dan mode jaringan lainnya
- Memahami peran **virtual switch** di Proxmox
- Menyiapkan mindset untuk konfigurasi jaringan ke depan

---

## 🧠 Apa Itu Jaringan Virtual?

Dalam dunia virtualisasi, jaringan tidak hanya terdiri dari kabel dan switch fisik.  
Kita bisa **menciptakan jaringan digital**, seolah-olah seperti di dunia nyata.

Bayangkan kamu main **The Sims**, tapi kali ini kamu bikin rumah, jalan, dan kabel internet sendiri 🏡📡

---

## 🧩 Elemen Penting Jaringan Virtual

| Komponen | Fungsi | Analogi |
|----------|--------|---------|
| **NIC (Network Interface Card)** | Antena-nya VM | Seperti WiFi adapter laptop |
| **Bridge (vmbr)** | Penghubung antara VM dan dunia luar | Seperti switch LAN |
| **vSwitch / Virtual Switch** | Switch virtual internal | Bayangkan colokan LAN digital |
| **NAT (Network Address Translation)** | Jembatan VM ke internet dengan IP privat | Seperti WiFi router di rumah |

---

## 🌉 Apa Itu Bridge?

Bridge (`vmbr0`, `vmbr1`, dst) adalah **jembatan** antara:

- NIC fisik (misalnya `enp3s0`)
- dan VM/Container (yang punya virtual NIC)

Dengan bridge, VM bisa **berkomunikasi seperti komputer fisik di jaringan yang sama**.

> 📌 Default install Proxmox akan bikin `vmbr0` otomatis, biasanya dikaitkan ke NIC utama.

---

## 🔄 Perbedaan Mode Jaringan

| Mode | Bisa Internet? | Bisa Akses Host? | Bisa Akses VM lain? | Cocok Untuk |
|------|----------------|------------------|----------------------|-------------|
| **Bridged** | ✅ | ✅ | ✅ | Produksi, koneksi LAN |
| **NAT**     | ✅ | ❌ | ✅ | Lab/testing pribadi |
| **Host-only** | ❌ | ✅ | ✅ | Simulasi isolasi jaringan |
| **Isolated LAN** | ❌ | ❌ | ✅ | Topologi lab internal-only |
| **Routed** | ✅ | ⚠️ Kompleks | ✅ | Advanced networking |

> 🔎 NAT = VM pakai IP privat, keluar ke internet lewat IP host  
> 🔎 Bridged = VM seolah-olah punya IP sendiri di LAN

---

## 🖼️ Visualisasi Sederhana

```

+-------------+         +-----------+         +----------------+
\|     VM      | <---->  |  vmbr0    | <---->  | NIC fisik (eth0)|
+-------------+         +-----------+         +----------------+
\|                     |
Virtual NIC          Virtual Switch

```

---

## ⚠️ Kesalahan Umum Pemula

❌ Pikir VM langsung bisa internet tanpa setup  
✅ Harus pilih bridge yang tepat dan pastikan routing benar

❌ Bingung kenapa VM tidak bisa ping ke luar  
✅ Mungkin kamu pakai host-only atau isolated LAN

---

## 🧪 Eksperimen Mandiri

Kalau kamu pakai Proxmox di nested VM (VirtualBox/VMware), coba:

- Cek `vmbr0` pakai `ip a` atau `ifconfig`
- Buat VM kecil (Alpine atau Debian)
- Assign ke `vmbr0` → install DHCP client → coba `ping google.com`

> Jika berhasil, artinya jaringan bridged kamu jalan 🚀

---

## 🧭 Penutup

🎉 Sekarang kamu sudah mengerti **landasan konsep jaringan di Proxmox**!  
Di bab selanjutnya, kita akan gali lebih dalam: **jenis-jenis jaringan yang bisa kamu pilih dan konfigurasi langsung**.

---

📍 Selanjutnya: [`02_Jenis_Jaringan_di_Proxmox.md`](02_Jenis_Jaringan_di_Proxmox.md)  
Akan membahas mode jaringan yang tersedia di Proxmox dan kapan sebaiknya kamu pakai masing-masingnya! 🔧📡


Kalau kamu setuju, kita langsung lanjut ke `02_Jenis_Jaringan_di_Proxmox.md` ya! 💨
Siap?
