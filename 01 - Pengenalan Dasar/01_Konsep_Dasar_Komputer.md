# 💻 01 - Konsep Dasar Komputer

Selamat datang di level pertama petualangan kita! 🧙‍♂️  
Sebelum membangun kastil virtual bernama Proxmox, kamu perlu tahu dulu bagaimana "bata-batanya" bekerja.

Bayangkan kamu mau jadi **arsitek infrastruktur IT** — kamu perlu ngerti fondasi dari sebuah komputer dulu. Yuk mulai!

---

## 🧠 Apa Itu Komputer?

> Komputer adalah mesin elektronik yang bisa menerima input, memproses data, menyimpan informasi, dan memberikan output.

Secara umum, komputer terdiri dari 2 komponen utama:
- **Hardware** 🧱 (perangkat keras): Semua yang bisa kamu pegang
- **Software** 🧠 (perangkat lunak): Semua instruksi digitalnya

---

## 🧱 Komponen Dasar Komputer

### 🔸 1. **CPU (Central Processing Unit)**
- Otaknya komputer.
- Semua perhitungan dan logika terjadi di sini.
- Di Proxmox, CPU sangat penting untuk **menjalankan banyak VM atau container** sekaligus.

> Analogi: CPU = Kepala koki di dapur, yang memproses semua pesanan masuk.

---

### 🔸 2. **RAM (Random Access Memory)**
- Tempat penyimpanan sementara saat komputer bekerja.
- Akses cepat, tapi akan hilang datanya saat dimatikan.

> Analogi: RAM = Meja kerja di dapur. Semakin besar, semakin banyak bahan yang bisa disiapkan sekaligus.

---

### 🔸 3. **Storage (Harddisk/SSD/NVMe)**
- Tempat menyimpan data jangka panjang.
- Ada berbagai jenis: HDD, SSD, NVMe
- Proxmox bisa mengatur banyak jenis penyimpanan: local, NFS, Ceph, dll.

> Analogi: Storage = Lemari dapur tempat kamu simpan bahan makanan.

---

### 🔸 4. **Motherboard**
- Papan utama yang menghubungkan semua komponen.
- Menyediakan jalur komunikasi antar hardware.

---

### 🔸 5. **Power Supply (PSU)**
- Menyuplai daya ke seluruh komponen.
- Di server fisik, kualitas PSU sangat berpengaruh terhadap kestabilan sistem.

---

### 🔸 6. **Network Interface (LAN Card)**
- Menghubungkan komputer dengan jaringan (internet atau LAN).
- Penting banget di Proxmox, apalagi kalau kamu bikin **cluster**.

---

## 💾 Software: OS, Kernel & Aplikasi

### 👨‍🏫 Operating System (OS)
- Sistem yang mengatur semua interaksi antara user dan hardware.
- Contoh: Windows, Linux, macOS.
- Proxmox sendiri berbasis **Debian Linux**!

### 🔧 Kernel
- Bagian inti dari OS yang mengatur komunikasi antara software & hardware.
- Kernel Linux = jantung dari sistem Proxmox.

---

## 💡 Kenapa Harus Ngerti Ini Dulu?

> Karena semua hal di Proxmox berhubungan erat dengan hardware & OS!

Contoh:
- Mau buat VM? Butuh CPU, RAM, Storage.
- Mau set storage ZFS? Harus ngerti jenis disk.
- Mau bikin cluster? Butuh pemahaman jaringan & hardware fisik.

---

## 🧩 Kesimpulan

| Komponen | Fungsi | Peran di Proxmox |
|----------|--------|------------------|
| CPU | Proses logika & data | Jalankan VM/LXC |
| RAM | Penyimpanan sementara | Diperlukan tiap VM |
| Storage | Simpan data permanen | Simpan image VM, backup |
| NIC | Koneksi jaringan | Komunikasi VM, clustering |
| OS | Mengatur sistem | Proxmox = OS berbasis Debian |

---

## 🧠 Pertanyaan Reflektif

- Apa beda RAM dan Storage?
- Mengapa NIC penting di server virtual?
- Mengapa kernel Linux berperan penting di Proxmox?

---

🎯 Kalau sudah paham, yuk lanjut ke:
👉 [`02_Pengenalan_Virtualisasi.md`](02_Pengenalan_Virtualisasi.md)

