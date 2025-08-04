# 💾 06 - Menambah Disk dan Setting Storage di Proxmox

Pernah merasa penyimpanan node Proxmox kamu cepat habis?  
Nah, di sini kamu akan belajar menambahkan disk baru dan mengonfigurasikannya jadi storage VM, ISO, atau backup 📦

---

## 🎯 Tujuan Bab Ini

- Mengenali jenis storage yang bisa digunakan di Proxmox
- Menambahkan disk tambahan ke node
- Memformat dan mounting disk
- Menambahkan storage ke Proxmox (via WebUI atau CLI)

---

## 🔍 Jenis Storage di Proxmox

| Tipe Storage | Contoh                   | Kegunaan                             |
|--------------|--------------------------|--------------------------------------|
| **Directory** | Disk lokal (ext4, xfs)   | Simpan VM, ISO, Backup               |
| **ZFS**       | Pool berbasis RAID ZFS   | Redundansi, snapshot, error recovery |
| **LVM/LVM-Thin** | Disk block             | VM berbasis blok (cepat & ringan)    |
| **NFS/CIFS**  | Storage jaringan         | Backup atau storage shared           |

---

## 🧠 Sebelum Menambahkan Disk…

1. Pastikan disk sudah **terpasang** secara fisik atau virtual
2. Cek disk dengan:
   ```bash
   lsblk
   ````

    Contoh hasil:
    
    ```
    ➜  ~ lsblk
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
    sda      8:0    0 223,6G  0 disk 
    ├─sda1   8:1    0     1M  0 part 
    ├─sda2   8:2    0   513M  0 part /boot/efi
    └─sda3   8:3    0 223,1G  0 part /
    sdb      8:16   0 111,8G  0 disk 
    └─sdb1   8:17   0  50,8G  0 part 
    ```
    
    ### 🧠 Penjelasan Output:
    
    | Kolom         | Arti                                                    |
    | ------------- | ------------------------------------------------------- |
    | `NAME`        | Nama disk dan partisi (misal `sda`, `sdb`, `sda1`, dst) |
    | `SIZE`        | Ukuran total disk atau partisinya                       |
    | `TYPE`        | Jenis: `disk` (fisik), `part` (partisi), `lvm`, dll     |
    | `MOUNTPOINTS` | Lokasi partisi "dipasangkan" dalam sistem               |
    
    ### 📦 sda vs sdb itu apa?
    Di sistem Linux, device seperti harddisk dan SSD diidentifikasi dengan nama **`sdX`**, di mana:

    * **`sd`** = SCSI/SATA Disk (termasuk SSD)
    * **`X`** = huruf urutan mulai dari `a`, `b`, `c`, dst.

---

## 🛠️ Langkah 1: Format & Mount Disk (ext4)

```bash
# Format disk
mkfs.ext4 /dev/sdb

# Buat folder mount point
mkdir /mnt/disk2

# Mount disk
mount /dev/sdb /mnt/disk2
```

### Agar Otomatis Mount Saat Boot:

Edit file `/etc/fstab` dan tambahkan:

```
/dev/sdb   /mnt/disk2   ext4   defaults   0  2
```

> 📝 Pastikan folder `/mnt/disk2` sudah dibuat!

---

## 🛠️ Langkah 2: Tambahkan ke Storage Proxmox

1. WebUI → Datacenter → Storage → Add → Directory
2. Masukkan:

   * ID: `disk2` (atau nama lain)
   * Directory: `/mnt/disk2`
   * Content: centang yang kamu butuhkan (ISO, VZDump, Disk image, dsb)
3. Klik **Add**

Selesai! Disk baru siap dipakai 💪

---

## 🔁 Alternatif: Tambah ZFS Storage

Kalau kamu butuh redundancy dan snapshot, bisa gunakan ZFS:

```bash
zpool create tank /dev/sdb
```

Kemudian di WebUI:

* Add → ZFS
* Pool name: `tank`
* Centang content: Disk image, container, dsb

> ⚠️ ZFS butuh RAM besar (disarankan 8GB+) dan tidak cocok digabung ext4/xfs biasa.

---

## 🎯 Tugas Mandiri

✅ Cek disk yang tersedia
✅ Format dan mount 1 disk ke `/mnt/`
✅ Tambahkan sebagai storage ke Proxmox
✅ Coba upload ISO atau buat backup ke disk baru

---

📍 Lanjut ke: [`07_Update_Repo_dan_Lisensi_CEPH_NonSub.md`](07_Update_Repo_dan_Lisensi_CEPH_NonSub.md)
Yuk atur repo biar update-nya aman dan gratis walau tanpa subscription 🧩
