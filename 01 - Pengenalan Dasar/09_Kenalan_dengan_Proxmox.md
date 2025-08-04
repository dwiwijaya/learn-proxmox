# 🖥️ 09 - Kenalan dengan Proxmox VE

Selamat datang di bab paling ditunggu! 🎉  
Proxmox VE adalah platform virtualisasi open-source yang powerful — dan sangat ramah untuk tim kecil maupun besar.

---

## ❓ Apa Itu Proxmox VE?

Proxmox VE (Virtual Environment) adalah sistem operasi berbasis Debian Linux yang digunakan untuk **menjalankan virtual machine (VM)** dan **container (CT)** secara efisien.

> 🧠 Gampangnya: Proxmox itu seperti **"mesin besar yang bisa nyalain banyak komputer virtual di dalamnya"**

---

## 🛠️ Fitur Utama Proxmox

| Fitur               | Penjelasan Singkat                                |
|---------------------|----------------------------------------------------|
| Virtual Machine (VM)| Komputer virtual berbasis KVM/QEMU                |
| Container (CT)      | Isolasi ringan menggunakan LXC                    |
| Web UI & CLI        | Akses mudah via web + kekuatan penuh lewat terminal |
| Backup & Snapshot   | Simpan/muat ulang kondisi VM/CT dengan mudah      |
| Cluster & HA        | Gabungkan banyak server jadi satu sistem          |
| Storage fleksibel   | Dukungan ZFS, LVM, NFS, Ceph, dll                 |
| Network Virtualisasi| VLAN, Bridge, NAT, dan bonding jaringan           |

---

## 🧠 Komponen Inti Proxmox

Di balik antarmuka web yang simpel, Proxmox punya mesin kuat. Ini dia komponennya:

### 🔧 1. `pvedaemon`
- Proses utama backend Proxmox.
- Bertugas menangani request dari web UI atau CLI.
- Dialah otak di balik semua eksekusi perintah.

### ⚙️ 2. `pveproxy`
- Web server bawaan Proxmox.
- Menyediakan antarmuka web di port `8006`.

### 🧱 3. `pve-cluster`
- Menyinkronkan data antar node di cluster Proxmox.
- Gunakan sistem file **Corosync** dan `pmxcfs`.

### 🖥️ 4. `qemu-kvm`
- Hypervisor untuk menjalankan VM.
- Setiap VM Proxmox dijalankan sebagai proses QEMU.

### 📦 5. `lxc`
- Teknologi container ringan di Linux.
- Proxmox pakai LXC untuk jalankan container.

### 💾 6. `vzdump`
- Tool built-in untuk backup VM dan CT.
- Bisa buat backup ke file `.tar` atau `.vma.zst`.

---

## 🔗 Antarmuka Akses Proxmox

| Akses     | Cara                                      |
|-----------|-------------------------------------------|
| Web UI    | https://[ip-proxmox]:8006                 |
| SSH       | `ssh root@[ip-proxmox]`                   |
| CLI lokal | Terminal langsung di server Proxmox       |
| API       | Untuk integrasi otomatisasi/devops        |

---

## 🧰 File & Direktori Penting

| Lokasi                            | Fungsi                                    |
|----------------------------------|-------------------------------------------|
| `/etc/pve/`                      | Konfigurasi utama Proxmox (cluster-aware) |
| `/var/lib/vz/`                   | Lokasi default VM & CT                    |
| `/etc/network/interfaces`        | Konfigurasi jaringan                      |
| `/etc/pve/storage.cfg`           | Pengaturan storage backend                |

---

## 📸 Snapshot & Backup

| Fitur     | Snapshot                         | Backup                                    |
|-----------|----------------------------------|-------------------------------------------|
| Fungsi    | Simpan keadaan VM saat ini       | Salin penuh VM/CT ke file                 |
| Waktu     | Sangat cepat (detik)             | Lebih lama, tergantung ukuran             |
| Tujuan    | Rollback jika ada masalah        | Recovery jangka panjang                   |

---

## 🚦 Alur Dasar Penggunaan Proxmox

1. Install Proxmox di server fisik
2. Akses Web UI (`https://ip-server:8006`)
3. Tambah storage & atur jaringan
4. Buat VM atau CT
5. Kelola, snapshot, backup
6. (Opsional) Gabung ke cluster

---

## 🎯 Kapan Pakai VM vs CT?

| Kriteria          | VM                         | CT (Container)                 |
|-------------------|-----------------------------|--------------------------------|
| Sistem operasi    | Semua (Windows, Linux, BSD) | Hanya Linux                    |
| Isolasi           | Penuh (hypervisor)          | Ringan (kernel share)          |
| Performa          | Lebih berat                 | Lebih ringan dan cepat         |
| Kompatibilitas    | Lebih fleksibel             | Terbatas (hanya Linux)         |

---

## 🧠 Pertanyaan Reflektif

- Apa fungsi `pvedaemon` dan `pveproxy`?
- Kapan kamu lebih baik pakai Container dibanding VM?
- Apa beda snapshot dan backup?

---

📍 Next: [`10_Review_Materi_Level_Ini.md`](10_Review_Materi_Level_Ini.md)  
Kita akan rangkum semua petualangan di Level 01 ini, dan uji pemahaman kamu dengan kuis kecil! 🧠📚
