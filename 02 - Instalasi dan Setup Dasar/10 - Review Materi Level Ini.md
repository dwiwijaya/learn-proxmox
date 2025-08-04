# 🔁 10 - Review Materi Level Ini

Selamat! Kamu sudah menyelesaikan satu level penuh tentang instalasi dan setup Proxmox! 🎉  
Sebelum lanjut ke level berikutnya, mari kita review dan pastikan semua konsepnya benar-benar dipahami.

---

## 📚 Ringkasan Materi

| Bab | Judul                                      | Inti Pembahasan                                                 |
|-----|--------------------------------------------|------------------------------------------------------------------|
| 01  | Mempersiapkan Hardware & Virtualisasi      | CPU-VT, minimal spek Proxmox, BIOS, dan perbandingan baremetal  |
| 02  | Instalasi Proxmox dari ISO                 | Flash ISO ke USB, booting, install ke disk                      |
| 03  | Konfigurasi Awal Setelah Install           | Hostname, network awal, akses WebUI                             |
| 04  | Mengenal WebUI & Pengaturan Dasar          | Navigasi, node, storage, dashboard, shell                       |
| 05  | Konfigurasi Jaringan LAN dan Bridge        | Bridge `vmbr0`, static IP, DHCP, LAN vs WAN                     |
| 06  | Menambah Disk & Setting Storage            | Format disk, LVM, mount disk tambahan                           |
| 07  | Update Repo & Lisensi Non-Subscription     | Ganti ke repo community, hapus notifikasi error                 |
| 08  | Menambahkan ISO VM & Template LXC          | Upload ISO, download template container                        |
| 09  | Buat VM & Container Pertamamu              | Proses step-by-step bikin VM & LXC, pengaturan disk & network   |

---

## 🧠 Istilah Penting

| Istilah         | Arti Singkat                                                                          |
|------------------|----------------------------------------------------------------------------------------|
| **VM**           | Virtual Machine, komputer virtual full OS                                             |
| **LXC**          | Container Linux ringan, share kernel host                                             |
| **Bridge (vmbr0)**| Jembatan dari VM ke LAN, supaya bisa dapet IP                                        |
| **ISO**          | File instalasi OS                                                                     |
| **Storage**      | Tempat simpan file VM/CT, bisa `local`, `local-lvm`, ZFS, dll                         |
| **BIOS vs UEFI** | Sistem boot lama vs modern                                                            |
| **LVM**          | Logical Volume Manager — cara Proxmox ngatur disk dinamis                            |
| **Repository**   | Sumber paket & update Proxmox/OS, biasanya HTTP link ke Debian/Proxmox CDN            |
| **CT Template**  | Gambar dasar container, biasanya format `.tar.zst`                                   |

---

## ❓ Mini Quiz — Tes Pemahamanmu!

> Jawablah dengan jujur dulu di kepala kamu. Penjelasan ada di bawah!

1. Apa perbedaan utama VM dan Container?
2. Apa fungsi dari `vmbr0`?
3. Kenapa kita perlu mengganti repository Proxmox?
4. Storage `local-lvm` itu bentuknya file atau block?
5. Kalau VM tidak dapat IP, langkah pengecekan apa yang bisa dilakukan?

---

## ✅ Jawaban dan Penjelasan

1. **VM** punya kernel sendiri (lebih berat), **LXC** share kernel host (lebih ringan & cepat)
2. `vmbr0` adalah bridge — jembatan virtual dari VM ke LAN router supaya bisa dapet IP
3. Proxmox default pakai repo berbayar (non-subscription error), jadi perlu ganti ke versi community agar bisa update tanpa lisensi
4. `local-lvm` adalah storage berbasis *volume block*, bukan file `.qcow2`
5. Cek apakah bridge (`vmbr0`) tersambung ke LAN, lalu cek `ip a` di dalam VM. Kalau perlu, atur IP statis

---

## 🎯 Tugas Akhir Level Ini

✅ Ambil waktu 1–2 hari untuk **ulangi semua langkah**:  
- Install ulang Proxmox di VM test  
- Setup jaringan dan upload ISO  
- Buat minimal 1 VM dan 1 LXC  
- Coba remote masuk lewat SSH ke VM dan LXC  

Kalau semua sudah lancar tanpa tutorial — **kamu siap naik level berikutnya!**

---

## 📘 Next: Level 3 — Manajemen Lanjut Proxmox

Kita akan pelajari:
- Backup & Restore
- Snapshot
- Clone
- Firewall & Keamanan
- Monitoring (Grafana, Proxmox Mail notif)
- Cluster & High Availability 🚀

Stay tuned!


