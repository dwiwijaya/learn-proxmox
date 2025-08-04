# 🛠️ 09 - Buat VM dan Container Pertamamu

Akhirnya kita sampai di tahap paling praktikal! 🎉  
Kita akan membuat dua hal penting di Proxmox:

1. **Virtual Machine (VM)** berbasis ISO  
2. **Container (LXC)** berbasis template  

---

## 🧠 Sekilas Perbedaan: VM vs LXC

| Aspek      | Virtual Machine (VM)                  | LXC Container                            |
|------------|----------------------------------------|-------------------------------------------|
| Kernel     | Punya kernel sendiri (lebih berat)    | Pakai kernel host (lebih ringan)         |
| Performa   | Lebih lambat tapi fleksibel           | Cepat & efisien tapi terbatas            |
| OS Support | Bisa Windows & Linux                  | Umumnya Linux                            |
| Use-case   | Full OS, software kompleks            | Web app, API server, automation ringan   |

---

## 🎯 Tujuan Bab Ini

- Membuat VM dari ISO
- Memahami pengaturan seperti format disk, BIOS/UEFI, dan network bridge
- Install OS ke dalam VM
- Jalankan & akses VM
- Mengenal cara membuat container (LXC)

---

## 🧱 Apa Itu VM?

VM (Virtual Machine) itu seperti “komputer palsu” di dalam server Proxmox.  
Ia punya CPU, RAM, hard disk, dan koneksi internet — semua virtual.

> 💡 **Analogi**: Seperti menjalankan beberapa laptop di dalam 1 laptop besar.

---

## 📋 Syarat Sebelum Membuat VM

- Sudah upload ISO OS ke storage (misalnya Ubuntu Server)
- Sudah tahu storage `local` vs `local-lvm`
- Bridge jaringan (`vmbr0`) sudah aktif (default)

---

## 🧙‍♂️ Langkah Membuat VM + Penjelasan

### 1. **General**
![Set Name](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Name.png)

| Opsi      | Penjelasan                         |
|-----------|-------------------------------------|
| Node      | Nama server host kamu (`pve1`)     |
| VM ID     | ID unik VM (boleh auto)            |
| Name      | Nama VM, misalnya `ubuntu-server`  |

---

### 2. **OS**
![Choose ISO](https://www.tecmint.com/wp-content/uploads/2023/12/Choose-Fedora-ISO-File.png)

| Opsi        | Penjelasan                                       |
|-------------|---------------------------------------------------|
| ISO Image   | File ISO OS (misalnya `ubuntu-22.04.iso`)        |
| Guest OS    | Jenis OS, misal: Linux > Ubuntu                   |

---

### 3. **System**
![System Settings](https://www.tecmint.com/wp-content/uploads/2023/12/Keep-Default-System-Settings.png)

| Opsi            | Penjelasan                                       |
|-----------------|---------------------------------------------------|
| BIOS            | `SeaBIOS` (legacy), `OVMF (UEFI)` untuk OS modern |
| Machine         | Default saja (`i440fx` / `q35`)                   |
| Graphic         | Biarkan default                                   |
| SCSI Controller | Pilih `VirtIO SCSI` jika OS support               |

> 💡 BIOS = rumah jadul | UEFI = rumah modern, boot lebih cepat

---

### 4. **Hard Disk**
![Set Disk](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Disk-Size.png)

| Opsi       | Penjelasan                                                                   |
|------------|-------------------------------------------------------------------------------|
| Storage    | `local` = file `.qcow2` biasa, `local-lvm` = volume block (lebih cepat)       |
| Format     | `qcow2` = support snapshot, `raw` = lebih sederhana, performa bagus           |
| Size       | Minimal 8–20 GB, tergantung OS                                                |

---

### 5 & 6. **CPU & Memory**
![CPU Settings](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-CPU-Settings.png)  
![Memory Settings](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Memory-Settings.png)

| Opsi     | Penjelasan                        |
|----------|-----------------------------------|
| Sockets  | Jumlah prosesor fisik             |
| Cores    | Core CPU virtual untuk VM         |
| Memory   | RAM virtual (misal 2048 MB)       |

---

### 7. **Network**
![Network Settings](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Network-Settings.png)

| Opsi      | Penjelasan                                                                 |
|-----------|------------------------------------------------------------------------------|
| Bridge    | Gunakan `vmbr0` (jembatan ke LAN)                                           |
| Model     | `virtio` = cepat, `Intel E1000` = lebih kompatibel (untuk OS lama)         |

> 🌉 `vmbr0` = seperti “colokan LAN” virtual  
> Kalau VM nyolok ke `vmbr0`, dia bisa langsung dapat IP dari router

---

### 8. **Confirm**
![Confirm Settings](https://www.tecmint.com/wp-content/uploads/2023/12/Confirm-VM-Settings.png)

Klik **Finish**, maka Proxmox akan membuat VM sesuai konfigurasi kamu.

---

## 🚀 Jalankan dan Install OS

1. Klik VM → **Start**
2. Klik **Console** → layar instalasi OS akan muncul
3. Ikuti proses instalasi seperti biasa (next-next-finish 🧑‍🍳)
4. Setelah selesai, login ke dalam OS

Cek koneksi internet dengan:
```bash
ip a
````

Kalau tidak dapat IP:

* Cek apakah `vmbr0` terhubung ke LAN
* Atur IP statis di dalam OS

---

## 📦 Membuat Container (LXC)

LXC lebih ringan dari VM dan cocok untuk web server, API, atau automation tools.

### Langkah Membuat LXC:

1. Klik **Create CT**
2. Isi:

   * CT ID & Hostname
   * Password root
   * Template `.tar.zst` (misalnya: Debian 12)
3. Disk: 4–8 GB
4. CPU & RAM: 1 core, 512 MB cukup
5. Network:

   * IP: DHCP atau statis (misal 192.168.1.100)
   * Gateway: 192.168.1.1
6. Confirm dan Start

### Akses Container:

* Klik **Console** → langsung masuk ke shell Linux
* Cek koneksi & lakukan konfigurasi sesuai kebutuhan

---

## 🎯 Tugas Mandiri

✅ Buat 1 VM baru (misalnya Ubuntu Server)
✅ Buat 1 Container (misalnya Debian LXC)
✅ Install OS dan cek jaringan di keduanya
✅ Coba install `openssh-server` untuk akses SSH

---

📍 Lanjut ke: [`10_Review_Materi_Level_Ini.md`](10_Review_Materi_Level_Ini.md)
Yuk kita review dan kuis kecil untuk menguatkan semua yang sudah kamu pelajari! 💡🔥



Kalau ini udah aman, kita gas lanjut ke bab terakhir level 2 ya, review dan quiz! Mau langsung masuk ke sana sekarang, Dwi? 😎
```
