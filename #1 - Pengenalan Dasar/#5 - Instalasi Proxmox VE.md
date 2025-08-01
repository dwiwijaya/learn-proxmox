# 💽 #5 - Instalasi Proxmox VE

Selamat datang di momen yang sakral! 🛠️  
Di tahap ini, kita akan benar-benar **mengubah sebuah PC menjadi server Proxmox**.  
Ibaratnya seperti **menyulap laptop biasa jadi markas Avengers versi IT!** 🦾🖥️

---


## ⚙️ Syarat Sistem (System Requirements)

Sebelum menginstal, pastikan perangkatmu memenuhi kebutuhan minimal Proxmox:

### ✅ Minimum (bisa jalan, cocok lab/testing)
- CPU: 64-bit (Intel VT-x / AMD-V support)
- RAM: 2 GB (minimum absolute; sangat terbatas)
- Storage: 16 GB (minimal), disarankan SSD
- Network: 1x Ethernet card (onboard atau PCIe)

### 💡 Rekomendasi (untuk penggunaan ringan-menengah)
- CPU: 2 core atau lebih, mendukung VT-x/AMD-V
- RAM: 8 GB atau lebih
- Storage: SSD 120 GB+
- Network: 1–2 NIC (kalau ingin cluster atau dedicated LAN)

### 🔥 Untuk Clustering (future use)
- CPU: 4 core+
- RAM: 16–32 GB
- 2 NIC (LAN internal + LAN akses luar)
- Support IOMMU kalau ingin PCI passthrough

---

## 📥 1. Download Proxmox ISO

Langkah pertama: ambil dulu instalernya!

🔗 [Download Proxmox VE ISO terbaru](https://www.proxmox.com/en/downloads/category/iso-images-pve)

Pilih versi paling baru dari daftar. Setelah download, kamu akan mendapatkan file `.iso`.

---

## 🔥 2. Siapkan Media Instalasi (USB Bootable)

Gunakan tool seperti:
- 🪟 **Rufus** (Windows)
- 🧊 **Balena Etcher** (Linux/Mac/Windows)
- 🧠 **Ventoy** (multi-boot, praktis banget!)

Langkah:
1. Masukkan USB minimal 2GB
2. Buka tool pilihanmu
3. Pilih file `.iso` Proxmox tadi
4. Jalankan proses flashing

Setelah selesai, USB kamu siap jadi "kunci ajaib" untuk masuk dunia Proxmox ✨

---

## 🚀 3. Boot dan Install

1. Masukkan USB ke PC target
2. Masuk ke BIOS/UEFI (biasanya tekan `DEL`, `F2`, atau `F12` saat boot)
3. Pilih boot dari USB
4. Proxmox installer akan muncul! Pilih:
   - **Install Proxmox VE**
   - Pilih disk target (SSD kamu)
   - Atur region, timezone, dan password admin
   - Pilih hostname dan IP server (bisa DHCP dulu atau langsung statik)

💡 *Tips:*  
Kalau kamu ingin jaringan stabil dan digunakan untuk cluster, **sebaiknya langsung atur IP statis**!

---

## ✅ 4. Setelah Install, Akses via Web!

Setelah restart selesai, kamu akan melihat pesan seperti ini:

```

You can now connect to the Proxmox VE web interface:
[https://192.168.1.xx:8006](https://192.168.1.xx:8006)

````

💻 Buka browser dari laptop/PC lain yang terhubung di jaringan yang sama, lalu ketik URL itu.

⚠️ Jangan lupa, gunakan `https://` dan port `:8006`!

---

## 🔐 5. Login Pertama

- Username: `root`
- Password: (yang kamu buat saat install)
- Realm: `pam` (standar)

Selamat! Kamu berhasil masuk ke **Proxmox Web Interface** 🎉  
Sekarang kamu sudah bisa:
- Membuat VM
- Membuat Container
- Mengatur storage & backup
- Dan nanti… setup **cluster!**

---

## 🧠 Sedikit Catatan

- Jika kamu pakai versi gratis, akan muncul notifikasi subscription. Abaikan saja (tidak mengganggu fungsi utama).
- Disarankan langsung update package Proxmox setelah login.

```bash
apt update && apt full-upgrade
````

---

🎯 Sudah siap menjelajah fitur-fitur Proxmox dan mulai membangun cluster?

🔗 Lanjut ke [#6 - Dasar Navigasi Proxmox.md](./#6%20-%20Dasar%20Navigasi%20Proxmox.md)

