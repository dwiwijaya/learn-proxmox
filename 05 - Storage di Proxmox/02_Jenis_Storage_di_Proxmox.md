# 🗃️ 02 - Jenis Storage di Proxmox

Proxmox mendukung **beragam jenis backend storage**, dari yang lokal sampai yang bisa dipakai bareng-bareng di banyak node (shared).
Di bab ini, kita akan petakan semua jenis storage backend, kelebihan & kekurangannya. Siap berlayar? 🏴‍☠️

---

## 🎯 Tujuan Bab Ini

* Mengenal berbagai jenis backend storage di Proxmox
* Memahami karakteristik dan use-case masing-masing
* Menentukan pilihan storage sesuai kebutuhan

---

## 📦 Daftar Jenis Storage di Proxmox

| Jenis Backend | Lokal / Network  | Cocok Untuk             | Kelebihan                         | Kekurangan                   |
| ------------- | ---------------- | ----------------------- | --------------------------------- | ---------------------------- |
| **Directory** | Lokal            | Pemula / Simpel         | Mudah setup, fleksibel            | Snapshot tidak native        |
| **LVM**       | Lokal            | Produksi kecil          | Performa tinggi                   | Snapshot perlu LVM-thin      |
| **LVM-thin**  | Lokal            | Snapshot VM             | Mendukung snapshot                | Perlu manajemen cermat       |
| **ZFS**       | Lokal            | Power user / redundancy | Snapshot, compression, redundancy | Konsumsi RAM besar           |
| **Btrfs**     | Lokal            | Eksperimen              | Snapshot, integritas data         | Kurang populer, experimental |
| **NFS**       | Network (shared) | Cluster & backup        | Mudah digunakan, fleksibel        | Bergantung jaringan          |
| **iSCSI**     | Network (shared) | Enterprise SAN          | Performa tinggi                   | Setup lebih rumit            |
| **Ceph**      | Network (shared) | Cluster skala besar     | Redundansi, shared native         | Kompleks, perlu 3+ node      |
| **GlusterFS** | Network (shared) | Alternatif Ceph         | Mirip Ceph, lebih simpel          | Tidak sekuat Ceph            |

---

## 🔍 Penjelasan Singkat Tiap Backend

### 🗂️ Directory (tipe `dir`)

* Penyimpanan berbasis folder di filesystem Linux
* Default storage Proxmox (`/var/lib/vz`)
* Cocok untuk ISO, backup, template, VM disk

### 💽 LVM / LVM-thin

* Menggunakan Logical Volume Manager
* LVM-thin mendukung snapshot dan provisioning fleksibel
* Umumnya digunakan di storage `local-lvm`

### 💧 ZFS

* Filesystem canggih: snapshot, mirror, compression
* Redundansi built-in (mirroring, RAID-Z)
* Ideal untuk yang ingin fitur tingkat lanjut
* Butuh RAM besar (min. 8GB direkomendasikan)

### 🗃️ Btrfs

* Filesystem modern dengan fitur mirip ZFS
* Masih eksperimental di beberapa sistem
* Snapshot cepat, cocok buat testing

---

### 🌐 NFS (Network File System)

* Simpel dan mudah digunakan untuk storage bersama
* Bisa digunakan untuk ISO, VM disk, backup
* Cukup andal jika jaringan stabil

### 🧱 iSCSI

* Block storage over network
* Dikenal cepat dan stabil di lingkungan enterprise
* Bisa di-cluster dengan tambahan LVM di atasnya

### 🐙 Ceph

* Clustered distributed storage buatan Proxmox (native)
* Redundant, scalable, self-healing
* Ideal untuk setup HA/Cluster besar
* Kompleks dan butuh resource tinggi (RAM, CPU, disk)

---

## 📊 Perbandingan Singkat

| Fitur            | Directory  | LVM             | ZFS   | NFS            | Ceph   |
| ---------------- | ---------- | --------------- | ----- | -------------- | ------ |
| Lokal / Shared   | Lokal      | Lokal           | Lokal | Shared         | Shared |
| Support Snapshot | ❌ (manual) | ✅ (dengan thin) | ✅     | ✅ (file-based) | ✅      |
| Mudah Setup      | ✅          | ✅               | ⚠️    | ✅              | ❌      |
| Performansi      | ⚠️         | ✅               | ✅     | ⚠️             | ✅      |
| Redundansi       | ❌          | ❌               | ✅     | ❌              | ✅      |
| Resource Ringan  | ✅          | ✅               | ❌     | ✅              | ❌      |

---

## 🧠 Tips Memilih Storage

| Kebutuhan                     | Rekomendasi                 |
| ----------------------------- | --------------------------- |
| Belajar / testing             | Directory / ZFS             |
| Produksi ringan (single node) | LVM-thin / ZFS              |
| Cluster Proxmox               | NFS (sederhana) / Ceph (HA) |
| Snapshot cepat                | LVM-thin / ZFS              |
| Redundansi built-in           | ZFS / Ceph                  |

---

## 🧪 Contoh Nyata

> Kamu punya server single node, 1 disk 512 GB:
> Gunakan `ZFS` → dapat snapshot, performa, dan mirroring (kalau punya 2 disk).

> Kamu mau setup 3 node Proxmox buat cluster:
> Gunakan `Ceph` → agar VM bisa berpindah antar node, dengan disk shared dan aman.

---

## 🎯 Tugas Mandiri

✅ Buka `Datacenter > Storage` dan klik tombol **Add**
✅ Lihat opsi yang tersedia: Directory, LVM, ZFS, NFS, dll
✅ Coba tambahkan 1 storage (misal: NFS atau directory baru untuk backup)
✅ Amati apakah bisa digunakan untuk ISO, disk, backup, atau snapshot

---

📍 Selanjutnya: [`03_Menambahkan_Storage_Baru.md`](03_Menambahkan_Storage_Baru.md)
Di bab itu, kita akan praktek **menambahkan storage baru** ke Proxmox VE — baik lokal maupun network. 🛠️📂

Kalau siap lanjut, tinggal bilang: **"lanjut tambah storage!"** 💬
