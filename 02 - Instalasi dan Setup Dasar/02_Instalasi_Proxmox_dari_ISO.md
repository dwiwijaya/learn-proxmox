# 💿 02 - Instalasi Proxmox dari ISO

Sekarang saatnya kita benar-benar *install* Proxmox VE di perangkat atau virtualisasi yang sudah kamu siapkan.  
Di bab ini, kamu akan belajar mulai dari **download ISO** hingga **install Proxmox sampai selesai**. 🚀

---

## 🎯 Tujuan Bab Ini

- Download ISO resmi Proxmox
- Membuat bootable USB (jika bare metal)
- Instalasi Proxmox step by step
- Verifikasi instalasi berhasil

---

## 🌐 Download ISO Proxmox

1. Buka website resmi:
   👉 [https://www.proxmox.com/en/downloads](https://www.proxmox.com/en/downloads)
2. Pilih: **Proxmox VE Latest ISO Installer**
3. Download file `.iso`-nya (biasanya sekitar 1 GB)

---

## 💽 Membuat Bootable USB (jika install di server fisik)

Gunakan tools berikut:

### 🪟 Windows:
- [Rufus](https://rufus.ie) – pilih ISO, target USB, klik Start

### 🐧 Linux:
```bash
sudo dd if=proxmox-ve.iso of=/dev/sdX bs=4M status=progress
````

> Ganti `/dev/sdX` dengan path USB drive kamu (hati-hati, bisa nge-wipe disk!)

---

## 🖥 Langkah Instalasi Proxmox

Setelah ISO siap:

1. **Boot ke USB / ISO**

   * Di BIOS/UEFI, atur boot priority ke USB/DVD
2. Muncul menu: pilih `Install Proxmox VE`
3. Ikuti wizard instalasi:

   * 🧠 **Target Harddisk**
     Pilih disk tempat Proxmox akan diinstall
   * 🔐 **Password & Email**
     Untuk login ke WebUI
   * 🌐 **Hostname & IP Address**
     Atur IP static agar WebUI bisa diakses dari jaringan
   * 🗺️ **Timezone & Mirror**
     Pilih zona waktu dan mirror lokal (untuk update cepat)
4. Klik **Install**, tunggu proses selesai
5. Reboot sistem

---

## 🌐 Akses Web Interface

Setelah reboot, kamu akan melihat tampilan terminal seperti ini:

```
You can now connect to the Proxmox VE web interface:

    https://192.168.1.100:8006

Login with your 'root' account and the password you set earlier.
```

💡 Akses WebUI dari browser lokal:
🔗 `https://<alamat-ip-kamu>:8006`
Contoh: `https://192.168.1.100:8006`

> Jika kamu install di nested VM, pastikan NIC pakai **bridged mode** biar bisa diakses dari host.

---

## ⚠️ Masalah Umum

| Masalah                      | Solusi                                                                     |
| ---------------------------- | -------------------------------------------------------------------------- |
| Tidak bisa boot dari USB     | Cek BIOS Boot Mode (UEFI/Legacy), ganti port USB, pastikan USB tidak rusak |
| Tidak bisa akses WebUI       | Cek IP di terminal, pastikan tidak salah subnet, tes `ping` dari host      |
| Error certificate saat akses | Abaikan warning SSL self-signed saat pertama kali, lanjutkan saja          |

---

## 🎯 Tugas Mandiri

✅ Download ISO Proxmox VE   
✅ Install Proxmox di bare-metal atau VM   
✅ Akses Web UI dari browser   
✅ Catat IP address Proxmox kamu   

---

📍 Lanjut ke: [`03_Konfigurasi_Awal_Setelah_Install.md`](03_Konfigurasi_Awal_Setelah_Install.md)   
Kita akan melakukan pengaturan awal agar Proxmox siap tempur! ⚙️

