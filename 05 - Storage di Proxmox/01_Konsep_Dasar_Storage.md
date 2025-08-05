# 💾 01 - Konsep Dasar Storage di Proxmox

Dalam dunia Proxmox, storage itu ibarat **lemari penyimpanan** besar tempat kamu nyimpan segalanya — mulai dari file installer ISO, image VM, disk container, sampai backup dan snapshot.
Tanpa storage, nggak akan ada tempat buat "hidupin" VM-mu! 😱

---

## 🎯 Tujuan Bab Ini

* Memahami peran storage dalam virtualisasi
* Mengenal tipe-tipe storage object di Proxmox
* Mengetahui struktur penyimpanan VM, CT, ISO, dan lainnya
* Paham istilah penting: volume, pool, backend

---

## 🧱 Apa Itu Storage di Proxmox?

Bayangkan Proxmox punya **beberapa lemari** dengan fungsi berbeda:

| 📦 Jenis "Isi" | 📁 Nama Storage-nya | Fungsi                                              |
| -------------- | ------------------- | --------------------------------------------------- |
| ISO / Image    | `iso`               | Simpan file `.iso` buat install OS                  |
| Disk VM/CT     | `images`            | Menyimpan virtual disk (file `.qcow2`, `.raw`, dll) |
| Container CT   | `rootdir`           | Isi file root container LXC                         |
| Backup         | `backup`            | Hasil snapshot dan backup VM/CT                     |
| Template       | `vztmpl`            | Template LXC container siap pakai                   |
| Snippet        | `snippets`          | Script atau file kecil otomatisasi                  |

---

## 📚 Istilah Penting

| Istilah               | Penjelasan Singkat                                      |
| --------------------- | ------------------------------------------------------- |
| **Volume**            | Satuan disk yang dipakai VM/CT (misal: `vm-100-disk-0`) |
| **Storage Pool**      | Sekumpulan volume yang ada di 1 backend                 |
| **Storage Backend**   | Teknologi di balik storage: LVM, ZFS, NFS, Directory    |
| **Thin Provisioning** | Disk virtual dibuat "tipis", alokasi sesuai kebutuhan   |

---

## 🔍 Storage Local vs Network

| Tipe        | Contoh Backend      | Cocok Untuk        |
| ----------- | ------------------- | ------------------ |
| **Local**   | Directory, LVM, ZFS | Server tunggal     |
| **Network** | NFS, iSCSI, Ceph    | Cluster multi node |

> 🔧 **Directory** = folder biasa di disk Linux
> 🔬 **LVM/ZFS** = manajemen disk yang lebih canggih (snapshot, pool, redundancy)
> 🌐 **NFS/iSCSI/Ceph** = storage yang bisa dishare ke banyak node

---

## 🧠 Analogi Simpel

Bayangkan VM-mu itu seperti **rumah**.

* `Disk` = lantai rumah
* `ISO` = CD instalasi furnitur
* `Snapshot` = foto rumah saat rapi
* `Backup` = salinan seluruh rumah buat restore
* `Template` = rumah yang udah dikasih furnitur dasar, tinggal pakai ulang

Semua itu... **butuh tempat**. Itulah Storage 🏠💽

---

## 🗃️ File Lokasi Default Storage

Jika kamu pakai directory-based storage (default):

| Jenis File | Lokasi Default di Proxmox                   |
| ---------- | ------------------------------------------- |
| ISO        | `/var/lib/vz/template/iso/`                 |
| VM Disk    | `/var/lib/vz/images/`                       |
| CT Root    | `/var/lib/lxc/` atau `/var/lib/vz/private/` |
| Backup     | `/var/lib/vz/dump/`                         |

> 💡 Folder bisa berbeda tergantung backend storage-mu

---

## 🚀 Apa yang Terjadi Saat Buat VM?

1. Proxmox bikin disk virtual di `images` (misal: `vm-100-disk-0`)
2. File `.iso` dipasang dari storage `iso`
3. VM dinyalakan, install OS
4. Semua berjalan di atas backend seperti LVM, ZFS, atau Directory

---

## 🎯 Tugas Mandiri

✅ Coba login ke Proxmox > menu **Datacenter > Storage**   
✅ Lihat storage default yang sudah ada (biasanya `local`, `local-lvm`)    
✅ Lihat isinya: ISO, backup, VM disk   
✅ Pahami storage backend apa yang digunakan: `dir`, `lvm`, atau lainnya   

---

📍 Selanjutnya: [`02_Jenis_Storage_di_Proxmox.md`](02_Jenis_Storage_di_Proxmox.md)
Kita akan bedah lebih dalam: **macam-macam backend storage** yang tersedia di Proxmox 🧠✨

Kalau siap lanjut, tinggal bilang: **"gas jenis storage"**! 💬
