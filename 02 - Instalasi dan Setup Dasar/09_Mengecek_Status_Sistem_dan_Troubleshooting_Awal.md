# 09 - Mengecek Status Sistem dan Troubleshooting 🚨🛠️

Halo, Pejuang Server! 🌟
Setelah server Proxmox-mu berdiri tegak, saatnya kita belajar **memantau kesehatannya** dan siap **menghadapi masalah umum** yang bisa muncul. Tenang, ini bukan sesi horor. Ini sesi jadi **dokter buat server** kamu! 🧑‍⚕️🖥️

---

## 📊 1. Mengecek Status Sistem Umum

Mari kita mulai dari hal paling dasar: **apakah server kita sehat-sehat aja?**

### 🔧 Cek CPU, RAM, dan Beban Sistem

Gunakan perintah ini di terminal Proxmox:

```bash
top
```

Atau versi ringkas:

```bash
htop
```

Kalau belum ada, install dulu:

```bash
apt install htop
```

> `htop` = versi visual dari `top`, lebih enak dilihat. 🎨

**Penjelasan**:

* **%CPU**: seberapa sibuk prosesor kamu
* **%MEM**: seberapa banyak RAM yang terpakai
* **Load Average**: angka beban dalam 1m / 5m / 15m.
  Contoh: `1.00` berarti 1 CPU penuh dipakai.

> ⚖️ *Analoginya:* Load Average itu seperti antrean pelanggan di kasir. Kalau kasir 1 (CPU 1), load 1.00 = pas. Load 2.00 = mulai antre. Load 0.50 = masih santai.

---

## 📦 2. Cek Ruang Penyimpanan Disk

Jangan sampai kehabisan ruang! Bisa bikin Proxmox error lho 😵

```bash
df -h
```

Penjelasan:

* `Filesystem`: nama partisi
* `Size`: ukuran total
* `Used`: yang sudah terpakai
* `Avail`: sisa ruang
* `Mounted on`: di mana dia dipasang (`/`, `/boot`, dll)

Contoh output:

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       224G   15G  198G   7% /
```

---

## 🔍 3. Cek Struktur Disk (lsblk)

Gunakan `lsblk` untuk melihat disk dan partisinya:

```bash
lsblk
```

Contoh:

```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0 223.6G  0 disk 
├─sda1   8:1    0     1M  0 part 
├─sda2   8:2    0   513M  0 part /boot/efi
└─sda3   8:3    0 223.1G  0 part /
sdb      8:16   0 111.8G  0 disk 
└─sdb1   8:17   0  50.8G  0 part 
```

Penjelasan:

* `sda`, `sdb` = urutan disk (pertama, kedua, dst)
* `sda1`, `sda2`, ... = partisi di disk tersebut
* `MOUNTPOINTS` = lokasi pemasangan (biasanya `/` adalah root)

> 🧠 Tips: Kalau kamu tambah disk baru nanti, dia biasanya muncul sebagai `sdc`, `sdd`, dst.

---

## 🌐 4. Cek Koneksi Jaringan

```bash
ip a
```

Cek apakah IP address sudah terpasang di `vmbr0`.

Ping ke gateway atau ke Google:

```bash
ping 8.8.8.8
```

> Kalau bisa ping 8.8.8.8 tapi gak bisa `google.com`, berarti DNS bermasalah.

---

## 🪵 5. Lihat Log Sistem

Log adalah **buku harian** server kamu. Cek di sini kalau ada error:

```bash
journalctl -xe
```

Atau:

```bash
dmesg
```

Kalau pakai WebUI, buka menu:
`Datacenter > node_name > Logs`

---

## ⚠️ 6. Troubleshooting Awal: Hal-hal Umum

| Gejala                 | Kemungkinan Masalah             | Solusi Awal                    |
| ---------------------- | ------------------------------- | ------------------------------ |
| Tidak bisa akses WebUI | IP salah? Port mati?            | Cek `ip a`, service `pveproxy` |
| VM tidak mau nyala     | Storage penuh? Resource kurang? | Cek `df -h`, RAM, CPU          |
| Tidak bisa SSH         | SSH service mati? IP berubah?   | `systemctl restart ssh`        |
| Tidak bisa internet    | Gateway / DNS salah             | Cek `/etc/network/interfaces`  |

---

## 🛑 7. Restart Service Proxmox

Kalau error aneh-aneh, coba restart:

```bash
systemctl restart pvedaemon
systemctl restart pveproxy
systemctl restart pvestatd
```

Atau reboot total:

```bash
reboot
```
---

## 📦 Bonus: Tools yang Bisa Kamu Install

| Tool     | Fungsi                                |
| -------- | ------------------------------------- |
| `htop`   | Monitor resource secara interaktif    |
| `iotop`  | Monitor aktivitas disk                |
| `nmon`   | Monitor server real-time (lengkap)    |
| `vnstat` | Statistik trafik jaringan             |
| `ncdu`   | Melihat penggunaan space dengan mudah |

Install:

```bash
apt install htop iotop nmon vnstat ncdu
```

---
## 🧘 Penutup: Jangan Takut Log, Takut Gak Cek 😅

Troubleshooting bukan tentang panik, tapi tentang tahu **apa yang harus dicek dan kenapa**. Proxmox itu transparan banget — kamu bisa lacak hampir semua masalah kalau tahu log-nya dan cara bacanya.

---

## ✅ Kesimpulan

Kamu sekarang udah bisa:

* Cek kondisi sistem seperti CPU, RAM, dan disk
* Tes koneksi jaringan dan IP
* Membaca struktur disk dengan `lsblk`
* Melihat log dan me-restart service penting
* Melakukan troubleshooting awal

> Ini adalah skill dasar seorang SysAdmin 💼💪 — dan kamu sudah punya fondasinya!

---

📍 **Lanjut ke: 10\_Review\_Materi\_Level\_Ini.md**
Yuk kita rekap perjalanan di Level 2 ini dan uji pemahamanmu lewat mini quiz! 🧠💡

---

Kalau kamu butuh aku buatkan juga `10_Review_Materi_Level_Ini.md`, tinggal bilang aja, Dwi! 🚀
