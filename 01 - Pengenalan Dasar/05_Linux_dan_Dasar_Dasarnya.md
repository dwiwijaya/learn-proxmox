# 🐧 05 - Linux & Dasar-Dasarnya

Selamat datang di dunia open-source paling berpengaruh dalam sejarah teknologi! 🔥  
Sebelum kamu bisa mengendalikan server Proxmox seperti seorang master, kamu harus akrab dulu dengan Linux.

---

## 📖 Apa Itu Linux?

> Linux adalah sistem operasi open-source berbasis Unix yang ringan, aman, dan banyak digunakan di server.

Linux adalah OS yang:
- Gratis dan terbuka
- Sangat stabil
- Digunakan di server, superkomputer, Android, dan Proxmox!

---

## 🧠 Struktur Dasar Sistem Linux

| Folder | Isi Umum |
|--------|----------|
| `/` | Root (akar sistem) |
| `/home` | Folder user biasa |
| `/etc` | Konfigurasi sistem |
| `/var` | Log dan file yang berubah |
| `/bin` | Binary / perintah dasar |
| `/usr` | Aplikasi & library pengguna |
| `/dev` | Perangkat (disk, USB, dll) |
| `/proc` | Info sistem real-time |

> 📂 Semua yang ada di Linux adalah *file* — bahkan disk & proses!

---

## 🧑‍💻 Perintah Dasar Linux

| Perintah | Fungsi |
|----------|--------|
| `ls` | Lihat isi folder |
| `cd` | Pindah folder |
| `pwd` | Lihat lokasi sekarang |
| `mkdir` | Buat folder |
| `rm` | Hapus file/folder |
| `cp` / `mv` | Salin / pindah file |
| `touch` | Buat file kosong |
| `nano` / `vim` | Edit file |
| `cat` / `less` | Lihat isi file |
| `top` / `htop` | Monitor resource |

---

## 🧙‍♂️ User: Root vs Non-root

- **root** = superuser (akses penuh, bisa ngapa-ngapain)
- **user biasa** = terbatas, harus pakai `sudo` kalau mau akses sistem

> ⚠️ Jangan sembarangan pakai `root`, bisa rusak sistem.

---

## 🧰 Package Manager (Pengelola Aplikasi)

Linux tidak pakai installer seperti Windows.  
Pakai **package manager** untuk install/uninstall:

| OS | Package Manager |
|----|-----------------|
| Debian/Ubuntu | `apt` |
| CentOS/RHEL | `yum` / `dnf` |
| Arch | `pacman` |

Contoh install aplikasi:
```bash
sudo apt update
sudo apt install htop
````

---

## 🧠 File Permission (Hak Akses)

Linux mengatur akses file dengan:

* **Owner** (pemilik)
* **Group** (kelompok)
* **Other** (umum)

Setiap file punya permission: `r` (read), `w` (write), `x` (execute)

Contoh:

```bash
chmod +x script.sh     # beri hak eksekusi
chown user:group file  # ubah kepemilikan
```

---

## 🎯 Kenapa Linux Penting di Proxmox?

* Proxmox dibangun di atas **Debian Linux**
* VM dan container biasanya pakai **Linux OS** (Ubuntu, Debian, Alpine)
* CLI management, script backup, auto deploy → semua pakai command Linux

---

## 🧠 Pertanyaan Reflektif

* Kenapa Linux populer di server?
* Apa perbedaan `root` dan `sudo`?
* Bagaimana cara melihat isi folder `/etc`?

---

📍 Selanjutnya kita akan bahas:
👉 [`06_Konsep_Storage_Dasar.md`](06_Konsep_Storage_Dasar.md)
Yuk kita gali gimana Proxmox menyimpan semua VM, container, backup, dan snapshot! 💾


