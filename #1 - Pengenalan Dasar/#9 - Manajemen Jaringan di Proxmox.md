# 🌐 #9 - Manajemen Jaringan di Proxmox

Selamat datang di dunia **networking** Proxmox!  
Bayangkan jaringan di Proxmox itu seperti **pipa-pipa air** yang menghubungkan rumah-rumah (VM/Container) ke kota (internet), atau ke rumah lain (node/VM lainnya). 💧🏠🌐

---

## 🧠 Konsep Dasar Jaringan di Proxmox

Proxmox menggunakan **Linux bridge** sebagai dasar sistem jaringan.  
Bridge ini berfungsi seperti **switch virtual**, menghubungkan VM ke jaringan nyata atau antar VM.

### 🔌 Komponen Jaringan Utama:
- **Linux Bridge (`vmbrX`)**: Seperti colokan/panel jaringan utama
- **Physical NIC (`ethX` atau `enpXsX`)**: Kartu jaringan fisik server
- **IP Address**: Alamat rumah dari node/VM
- **Gateway**: Gerbang keluar menuju internet

---

## 🧱 Struktur Dasar Setup

Misalnya:

| Interface | Peran               | Terkait            |
|-----------|---------------------|--------------------|
| `eth0`    | NIC fisik utama     | Terhubung ke LAN   |
| `vmbr0`   | Bridge utama        | Digunakan oleh VM  |
| `vmbr1`   | Isolasi jaringan VM | VLAN internal      |

---

## 🔧 Konfigurasi Jaringan (GUI)

Berikut ini contoh mengatur bridge `vmbr0` dari GUI Proxmox, seperti pada gambar:

![Edit Linux Bridge - Proxmox GUI](https://img.vembu.com/wp-content/uploads/2024/04/Network-Configuration-04.png)

### Langkah-langkah:
1. Masuk ke web Proxmox ➝ pilih node (misal: `proxmox`)
2. Arahkan ke menu **System ➝ Network**
3. Klik **Create ➝ Linux Bridge** (atau klik **Edit** untuk mengubah)
4. Atur isian seperti berikut:
   - **Name**: `vmbr0`
   - **IPv4/CIDR**: `192.168.3.101/24` (atau kosong jika hanya untuk VM)
   - **Gateway (IPv4)**: `192.168.3.1` (jika node ini butuh akses internet)
   - **Bridge ports**: `ens33` (atau NIC lain seperti `eno1`, `eth0`, dll)

5. Klik **OK** untuk menyimpan
6. Klik **Apply Configuration**, lalu reboot jika diperlukan

📌 Jika `Bridge ports` dikosongkan, maka bridge tidak terhubung ke dunia luar dan hanya bisa dipakai antar VM.

---

## 💡 Contoh Kasus

### 1. VM Butuh Akses Internet
→ Hubungkan VM ke `vmbr0` yang bridged ke `eth0`.

### 2. Cluster Proxmox (2+ Node)
→ Butuh interface untuk **corosync** (idealnya dedicated NIC atau VLAN).

### 3. Isolasi Jaringan
→ Buat `vmbr1`, tidak diberi akses ke NIC, hanya untuk antar VM (misal jaringan internal apps & DB).

---

## 🧙 Tips Pro

- Gunakan **static IP** untuk node Proxmox, jangan DHCP.
- Cek ulang NIC yang aktif dengan `ip a` jika bingung NIC mana yang dipakai
- Untuk cluster, jaringan stabil dan latency rendah sangat penting.
- Jangan ubah pengaturan jaringan via SSH saat Proxmox online di production — bisa disconnect!

---

🎯 Selanjutnya, kita masuk ke dunia **VM (Virtual Machine)** yang jadi aktor utama dari pertunjukan ini!

🔗 Lanjut ke [#10 - Membuat dan Mengelola VM.md](./#10%20-%20Membuat%20dan%20Mengelola%20VM.md)
