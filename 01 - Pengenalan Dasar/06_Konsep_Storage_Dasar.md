# 💾 06 - Konsep Storage Dasar

Yuk kenalan dengan dunia storage — tempat semua VM, container, ISO, backup, dan snapshot disimpan!

---

## 📖 Apa Itu Storage?

Storage = tempat menyimpan data.

Tapi di dunia server & Proxmox, kita gak cuma ngomongin soal *harddisk biasa*. Ada banyak jenis dan konsep yang perlu kamu tahu.

---

## 💽 Tipe Media Penyimpanan

| Jenis     | Karakteristik                           |
|----------|------------------------------------------|
| HDD      | Kapasitas besar, murah, lambat           |
| SSD      | Cepat, lebih mahal, tahan guncangan      |
| NVMe     | Super cepat, sangat responsif            |
| RAMDisk  | Sangat cepat, tapi data hilang saat reboot |

---

## 🧱 Struktur Disk di Linux

Linux mengenal disk sebagai file perangkat:
- `/dev/sda`, `/dev/sdb` → disk
- `/dev/sda1`, `/dev/sdb2` → partisi

Mount point: lokasi folder di mana disk di-*pasang*.  
Contoh:
```bash
mount /dev/sdb1 /mnt/data
````

---

## 🧊 MBR vs GPT: Skema Partisi

Sebelum kita bisa menyimpan data di sebuah disk, kita harus **membagi disk itu menjadi partisi**.
Nah, *cara membagi* ini diatur oleh yang namanya **skema partisi**, yaitu MBR atau GPT.

### 🧠 Apa itu Skema Partisi?

Bayangin kamu punya lemari besar (harddisk), dan kamu mau bagi jadi beberapa laci (partisi).
Tapi, kamu harus pilih sistem *pembagian laci*-nya dulu — itulah MBR atau GPT.

| Skema                          | Maks Partisi         | Maks Ukuran Disk | Dipakai di             | Cocok Untuk       |
| ------------------------------ | -------------------- | ---------------- | ---------------------- | ----------------- |
| **MBR** (Master Boot Record)   | 4 Primary Partitions | 2 TB             | Komputer lama (BIOS)   | Legacy system     |
| **GPT** (GUID Partition Table) | 128 Partisi          | >2 TB            | Komputer modern (UEFI) | Semua sistem baru |

🟢 **Gunakan GPT** kalau kamu pakai Proxmox di server atau PC modern (support UEFI).
🔴 Hindari MBR kecuali kamu terpaksa pakai hardware lama.


---

## 📂 **Apa itu File System?**

Setelah disk dipartisi, kita masih belum bisa menyimpan data…
Kita butuh **file system**: sistem yang mengatur bagaimana file disimpan, dibaca, dan dikelola.

📦 **Analogi:**
File system itu kayak **arsiparis digital** — dia yang tahu di mana letak semua file, siapa pemiliknya, dan bagaimana membacanya.

Contoh file system: `ext4`, `ZFS`, `XFS`

---

## 🧪 Perbandingan File System

| File System       | Cocok Untuk               | Keunggulan Utama                          | Kekurangan                                 |
|-------------------|---------------------------|-------------------------------------------|--------------------------------------------|
| **ext4**          | Sistem standar Linux      | Stabil, ringan, mudah digunakan           | Tidak punya fitur snapshot / RAID bawaan   |
| **ZFS**           | Server, Proxmox, backup   | Snapshot, RAID, koreksi error, kompresi   | Butuh RAM besar, konfigurasi lebih kompleks|
| **XFS**           | File besar (video, log)   | Performa tinggi untuk file besar          | Tidak support snapshot                     |
| **FAT32 / exFAT** | USB flash drive, portable | Kompatibel lintas OS (Windows, Linux)     | Tidak mendukung permission Linux & VM      |
| **NTFS**          | Sistem Windows            | Bisa dibaca/tulis oleh Linux (dengan driver) | Tidak optimal untuk server/Linux native    |


---

### 🔍 Penjelasan Lebih Dalam

#### ✅ **ext4**

* Digunakan hampir di semua distro Linux
* Cocok buat penggunaan biasa
* Mudah di-repair kalau rusak

#### 🌀 **ZFS**

* Bukan cuma file system, tapi juga volume manager!
* Bisa bikin **snapshot** (backup instan)
* Bisa otomatis **cek & perbaiki error** pada data
* Bisa bikin RAID sendiri (tanpa perangkat tambahan)
* Tapi: butuh **RAM besar** (ideal min. 8 GB)

#### ⚡ **XFS**

* Kuat di kecepatan tulis file besar (video, log)
* Banyak dipakai di server enterprise (RedHat, CentOS)

---

### 🔧 Mana yang Harus Saya Pilih?

| Kebutuhan Kamu                 | Pilihan Ideal |
| ------------------------------ | ------------- |
| Belajar Linux dasar            | ext4          |
| Bangun server Proxmox produksi | ZFS           |
| Menyimpan file besar / log     | XFS           |
---

## 🔁 RAID - Redundant Array of Independent Disks

RAID = teknik menggabungkan beberapa disk agar:

* Lebih cepat (performance)
* Lebih aman (redundansi)
* Lebih besar (kapasitas)

| Jenis RAID | Karakteristik                             |
| ---------- | ----------------------------------------- |
| RAID 0     | Gabung disk → cepat, tapi tidak aman      |
| RAID 1     | Mirroring → aman, lambat, 50% kapasitas   |
| RAID 5     | Kombinasi speed + redundancy, min. 3 disk |
| RAID 10    | Gabungan RAID 1 + 0 → cepat & aman        |

💡 Proxmox support ZFS RAID secara bawaan!

---

## 🌀 ZFS - File System Ajaib

> ZFS adalah file system dan volume manager modern yang powerful!

Keunggulan ZFS:

* Snapshot & cloning VM/CT
* Deteksi & koreksi error (data integrity)
* Built-in RAID: RAIDZ1, Z2, Z3
* Kompresi & deduplikasi otomatis

Contoh setup ZFS pool:

```bash
zpool create data mirror /dev/sdb /dev/sdc
```

---

## 🔌 Jenis Storage di Proxmox

| Tipe       | Contoh          | Keterangan                        |
| ---------- | --------------- | --------------------------------- |
| Local Disk | `/var/lib/vz`   | Default folder VM & CT            |
| LVM        | `local-lvm`     | Logical Volume Manager untuk VM   |
| Directory  | `/mnt/data`     | Folder biasa (bisa ISO/backup)    |
| NFS        | dari NAS        | Network File Storage (shared)     |
| Ceph       | storage cluster | Untuk HA dan cluster Proxmox      |
| ZFS        | `zpool1`        | Snapshot + RAID + performa tinggi |

---

## 🧠 Perbandingan Singkat

| Fitur       | ext4         | ZFS            | XFS            |
| ----------- | ------------ | -------------- | -------------- |
| Snapshot    | ❌            | ✅              | ❌              |
| RAID        | ❌            | ✅              | ❌              |
| Kompresi    | ❌            | ✅              | ❌              |
| Stabilitas  | ✅            | ✅              | ✅              |
| RAM Usage   | rendah       | tinggi         | sedang         |
| Cocok Untuk | sistem biasa | server/cluster | data besar/log |

---

## 🤔 Pertanyaan Reflektif

* Kapan kamu perlu RAID?
* Kapan kamu pilih ext4, dan kapan ZFS?
* Kalau storage kamu terbatas tapi butuh snapshot, pilih apa?

---

📍 Yuk lanjut ke:
👉 [`07_Konsep_Networking_Dasar.md`](07_Konsep_Networking_Dasar.md)
Di bab berikutnya kita bakal bahas IP, subnet, DNS, gateway, dan jaringan di dunia server! 🌐

