# 📂 08 - Memahami Struktur Direktori Proxmox

> "Kalau kita mau menjelajah hutan, kita butuh peta. Kalau mau menjelajah Proxmox, kita butuh tahu di mana letak semua file pentingnya!" 🌲🗺️
> Nah, Proxmox juga begitu. Sebelum kamu jadi jagoan VM dan cluster, yuk kenalan dulu sama **struktur file dan direktori penting** di balik layar Proxmox. 🧠🛠️

Di bab ini, kita akan **menjelajahi isi dapur** Proxmox — tempat di mana semua konfigurasi, log, dan data penting disimpan. Ini penting banget buat:
- Ngecek masalah (troubleshooting) 🔍
- Otomatisasi & scripting 🧪
- Backup manual 💾
- Pahami cluster Proxmox 🔗

---

## 🧠 Dasar Teori: Linux Filesystem 101

Sebelum ke Proxmox, pahami dulu prinsip ini:

> **Linux = Segalanya adalah file**
> Semua device, konfigurasi, bahkan disk dianggap sebagai file. Dan semuanya punya "rumah" di direktori root `/`.

Contohnya:

* `/etc` = pusat konfigurasi
* `/var` = tempat data berjalan (log, cache, dll)
* `/dev` = device seperti disk, USB
* `/home` = direktori user biasa

---

## 🗺️ Peta Direktori Penting di Proxmox

| 📂 **Lokasi**             | 🧠 **Fungsi**                                                                                                                |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `/etc/pve/`               | 💡 Direktori khusus Proxmox berisi semua konfigurasi utama (VM, storage, user, dsb). Ini **tersinkron otomatis** di cluster. |
| `/etc/pve/qemu-server/`   | 💽 File konfigurasi untuk semua VM (KVM/QEMU). Misalnya: `100.conf`, `101.conf`, dst.                                        |
| `/etc/pve/lxc/`           | 📄 Konfigurasi untuk setiap LXC container. Mirip dengan VM tapi untuk container.                                             |
| `/etc/pve/datacenter.cfg` | 🏢 Konfigurasi global datacenter (misal: setting backup default, mail, dll).                                                 |
| `/etc/pve/storage.cfg`    | 💾 Daftar storage pool (LVM, ZFS, NFS, dll) yang akan muncul di WebUI.                                                       |
| `/etc/pve/user.cfg`       | 👤 Konfigurasi user, permission, dan grup.                                                                                   |
| `/etc/pve/firewall/`      | 🔥 Semua aturan firewall global, per VM, atau container disimpan di sini.                                                    |

---

| 📂 **Lokasi**             | 🧠 **Fungsi**                                                                       |
| ------------------------- | ----------------------------------------------------------------------------------- |
| `/etc/hosts`              | 🌍 Mapping DNS lokal: node-name dan IP internal kamu ada di sini.                   |
| `/etc/network/interfaces` | 🌐 Konfigurasi IP statis, bridge (`vmbr0`, `vmbr1`, dst) dan interface lainnya.     |
| `/etc/resolv.conf`        | 🌐 DNS resolver: daftar server DNS yang digunakan oleh sistem untuk resolve domain. |

---

| 📂 **Lokasi**         | 🧠 **Fungsi**                                                                             |
| --------------------- | ----------------------------------------------------------------------------------------- |
| `/var/lib/vz/`        | 📦 Tempat default penyimpanan VM, container, ISO, template (kalau pakai storage `local`). |
| `/var/lib/lxc/`       | 📁 Struktur folder dan data container LXC (kalau gak pakai LVM).                          |
| `/var/log/syslog`     | 📜 Log umum sistem Linux: semua error, info, warning dari semua service.                  |
| `/var/log/pve/`       | 📋 Log Proxmox: task yang dieksekusi, error backup, log VM, dsb.                          |
| `/var/log/pve/tasks/` | ✅ Log detil semua *task* seperti start/stop VM, backup, snapshot, dsb.                    |

---

| 📂 **Lokasi Tambahan** | 🧠 **Fungsi**                                                                                        |
| ---------------------- | ---------------------------------------------------------------------------------------------------- |
| `/dev/`                | 📟 Berisi device seperti disk (`/dev/sda`, `/dev/zvol/`, dll). Semua dianggap sebagai "file device". |
| `/mnt/`                | 📂 Mount point disk tambahan (misalnya NFS, USB, ZFS, atau mount manual).                            |
| `/etc/apt/`            | 🔄 Setting repository & update Proxmox/Debian (`sources.list`, `*.list`).                            |

---

Kalau butuh gambaran lebih hidup, kamu bisa anggap begini:

> 🧳 **Analogi cepat:**
>
> * `/etc/pve` = pusat komando dan rencana induk
> * `/var/lib/vz` = gudang penyimpanan utama
> * `/var/log/` = buku catatan harian
> * `/dev/` = lemari device keras
> * `/mnt/` = rak titipan tambahan

---

## 🧠 Penjelasan Beberapa Folder Kunci

### 📁 `/etc/pve/` – Pusat Komando
Folder ini bisa dibilang **jantung Proxmox**. Semua config utama ada di sini:
- Setting VM & container
- User & role
- Storage
- Firewall
- Clustering

⚠️ Uniknya, folder ini akan **otomatis tersinkronisasi antar node** kalau kamu pakai Proxmox Cluster. Jadi, satu perubahan langsung terasa di semua server! Keren, kan?

---

### 📁 `/var/lib/vz/` – Gudang Default
Folder ini adalah tempat default Proxmox menyimpan berbagai *barang digital*, seperti:
- 🧠 Image disk VM (`/images/`)
- 📦 Backup (`/dump/`)
- 📀 ISO atau template (`/template/`)

Kalau kamu belum atur storage lain, semuanya akan numpuk di sini. Jadi pastikan cukup ruangnya ya!

---

### 📄 `/etc/network/interfaces` – Jalur Komunikasi
Semua setting jaringan kamu ada di sini. Misalnya:
- IP statis
- Bridge (`vmbr0`, `vmbr1`, dst)
- VLAN atau bonding interface

Contoh isi file:
```bash
auto vmbr0
iface vmbr0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    bridge_ports enp3s0
    bridge_stp off
    bridge_fd 0
````

> 🔍 *Analogi:* Bayangin kamu lagi pasang kabel LAN ke beberapa komputer, nah di sini kamu atur kabel virtualnya.

---

### 📄 `/etc/pve/qemu-server/100.conf` – File VM

Setiap VM punya satu file `.conf` yang menyimpan semua setting-nya:

* Jumlah core CPU
* RAM
* Disk dan ISO
* Network

Semua ada di sini dan bisa diubah manual (tapi hati-hati ya!).

---

### 📄 `/etc/pve/lxc/101.conf` – File LXC

Mirip seperti di atas, tapi ini untuk container LXC.

---

## 🛠️ Perintah Praktis Buat Eksplorasi

Beberapa perintah CLI yang bisa kamu coba langsung:

```bash
# Lihat isi direktori konfigurasi utama
ls -lh /etc/pve/

# Cek daftar semua VM & Container
ls /etc/pve/qemu-server/
ls /etc/pve/lxc/

# Cek konfigurasi storage
cat /etc/pve/storage.cfg

# Lihat isi default storage
ls /var/lib/vz/

# Lihat log Proxmox
cat /var/log/pve/tasks/

# Cek struktur folder konfigurasi (butuh tree)
tree -L 2 /etc/pve/
```

---

## 🎯 Kenapa Ini Penting?

✅ Kamu jadi lebih paham *di balik layar* Proxmox   
✅ Gampang tracing error atau ngecek kenapa VM nggak jalan   
✅ Lebih percaya diri waktu utak-atik Proxmox   
✅ Lebih aman kalau mau backup atau restore manual   

---

## 🧪 Mini Project: “Petakan Rumahmu Sendiri”

Masuk ke server Proxmox kamu via SSH, lalu jalankan:

 ```bash
 tree -L 2 /etc/pve/
 ```

Coba pahami file atau folder apa aja yang muncul, dan cocokkan dengan tabel di atas. Kalau nemu yang belum ngerti, tandai aja dulu, nanti akan kita pelajari seiring jalan. 😎

---

## 🧭 Penutup

Sekarang kamu sudah mulai memahami "tulang dan organ dalam" dari Proxmox. Di level lanjut nanti, kamu akan lebih sering ngoprek file-file ini — jadi sangat bagus kalau kamu sudah mulai nyaman dari sekarang.

📍 **Lanjut ke:** `09_Mengecek_Status_Sistem_dan_Troubleshooting_Awal.md`   
⏱️ Yuk belajar cara *memeriksa kesehatan server* dan mengidentifikasi masalah sejak dini! 🔍💡
