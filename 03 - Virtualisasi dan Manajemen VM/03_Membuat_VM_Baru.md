# 🛠️ 03 - Membuat VM Baru di Proxmox

Selamat datang di tahap seru berikutnya! 🎉  
Setelah kita memahami jenis virtualisasi dan sudah import ISO OS favoritmu, sekarang saatnya **membuat VM (Virtual Machine)** pertama kamu di Proxmox! 🖥️✨

---

## 🎯 Tujuan Bab Ini

- Mengenal langkah-langkah membuat VM di Proxmox
- Memahami parameter penting: disk, CPU, RAM, NIC
- Mampu menjalankan dan mengakses VM pertamamu

---

## 🤔 Apa Itu Virtual Machine?

Sederhananya, **Virtual Machine (VM)** adalah komputer virtual yang berjalan di dalam komputer fisik.  
Bayangkan seperti "komputer di dalam komputer", yang punya sistem operasi, RAM, CPU, dan penyimpanan sendiri.

> 🎮 Analogi: VM itu seperti game **The Sims**. Kamu bisa bikin rumah, atur orang di dalamnya, dan mereka hidup mandiri — meskipun semuanya cuma simulasi di layar. Sama halnya, VM adalah "komputer simulasi" yang bisa kamu atur dari luar.

---

## 🧪 Langkah-Langkah Membuat VM di Proxmox

Ikuti panduan berikut, dan kamu akan punya VM yang siap pakai!

### 1️⃣ Klik Tombol **Create VM**

Buka antarmuka Proxmox ➡️ klik node ➡️ pilih **Create VM** di kanan atas.

> Pastikan kamu sudah upload file ISO di langkah sebelumnya ya!

---

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

## 🧠 Ringkasan Konsep Penting

| Komponen | Fungsi | Tips |
|----------|--------|------|
| ISO | Seperti CD instalasi OS | Harus diupload sebelum buat VM |
| Disk | Ruang penyimpanan virtual | Gunakan qcow2 agar fleksibel |
| CPU/RAM | Menentukan kekuatan VM | Sesuaikan dengan host |
| Network | Akses internet & LAN | Gunakan bridge (`vmbr0`) |

---

## 📦 Tugas Mandiri

✅ Buat satu VM baru dengan OS yang kamu pilih (misal Debian atau Ubuntu)  
✅ Coba jalankan dan akses via **Console**  
✅ Catat pengalaman pertamamu: apakah sukses booting? apakah jaringan aktif?

---

## 🔗 Selanjutnya: [`04_Membuat_LXC_Container.md`](04_Membuat_LXC_Container.md)

Setelah jago bikin VM, kita akan belajar bikin **Container (LXC)** — cara virtualisasi yang lebih ringan dan efisien! ⚡📦  
Siap menyelam lebih dalam? Ayo gas! 🐳🚀

