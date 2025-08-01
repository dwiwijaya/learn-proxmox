# 💾 #8 - Manajemen Storage di Proxmox
Di sini kita akan belajar cara kerja dan pengelolaan storage di Proxmox.    
Analoginya? Bayangkan storage seperti lemari penyimpanan di rumahmu. Ada yang cepat tapi kecil (SSD), ada juga yang besar tapi lambat (HDD). Nah, Proxmox bisa mengatur banyak lemari ini sesuai keperluan VM/CT kamu! 🗄️🔧  

Dalam Proxmox, storage adalah tempat menyimpan semua aset penting:

- File ISO (instalasi OS)
- Disk untuk VM/CT
- Backup & snapshot
- Template container

---

## 🗂️ Jenis Storage yang Didukung

Proxmox sangat fleksibel! Beberapa jenis storage yang bisa kamu pakai:

| Tipe Storage      | Contoh                        | Kelebihan                      |
|-------------------|-------------------------------|--------------------------------|
| Directory         | Local disk (ext4, xfs)        | Mudah & cepat                  |
| LVM/LVM-Thin      | Logical Volume Manager        | Snapshot-friendly              |
| ZFS               | RAID software, snapshot       | Redundansi & performa tinggi   |
| NFS               | Network File System           | Berbagi via jaringan           |
| CIFS/SMB          | Share dari Windows/Linux NAS  | Kompatibel luas                |
| iSCSI             | Block-level network storage   | Performa tinggi (enterprise)   |
| Ceph              | Clustered distributed storage | Sangat scalable                |

---

## 📦 Struktur Storage di UI

![Struktur Storage Proxmox](https://files.programster.org/tutorials/kvm/proxmox/storage-guide/storage-configurations.png)

Setiap node di Proxmox bisa memiliki lebih dari satu storage.  
Storage bisa lokal (hanya node tertentu) atau shared (bisa diakses semua node).

---

## 🔧 Menambahkan Storage Baru

Untuk menambahkan storage baru:

1. Masuk ke menu `Datacenter` (panel kiri) ➝ `Storage`
2. Klik **Add**
3. Pilih jenis storage: `Directory`, `LVM`, `ZFS`, dsb.
4. Isi informasi:
   - ID storage
   - Path mount/disk
   - Pilih VM disk / backup / ISO / CT
5. Simpan dan storage siap digunakan! ✅

---

## 📂 Mengelola Konten Storage

Setelah storage terdaftar, kamu bisa:

- Upload ISO
- Restore VM dari backup
- Buat template untuk Container
- Melihat penggunaan storage (disk usage)

---

## 💡 Tips Praktis

- Simpan ISO & template di **storage khusus**, jangan campur dengan disk VM.
- Backup sebaiknya ditaruh di storage terpisah, idealnya eksternal/NAS.
- Untuk high-availability, pertimbangkan pakai storage **shared** (NFS/Ceph).

---

🎯 Siap lanjut ke dunia **networking** di Proxmox?

🔗 Lanjut ke [#9 - Manajemen Jaringan di Proxmox.md](./#9%20-%20Manajemen%20Jaringan%20di%20Proxmox.md)
