# 💻 08 - Pengantar CLI & SSH

Selamat datang di dunia terminal — tempat di mana para master server bekerja dalam diam.  
CLI (Command Line Interface) dan SSH (Secure Shell) adalah **alat komunikasi utama antara kamu dan server**.  
Yuk kita kuasai bersama! 🚀

---

## 📟 Apa Itu CLI?

CLI (Command Line Interface) adalah cara berinteraksi dengan komputer melalui baris perintah (terminal), **tanpa klik-klik GUI**.

Contoh CLI:
```bash
ls -lah
````

Daripada klik folder satu per satu, di CLI kamu bisa:

* Cek isi folder
* Copy/move file
* Install software
* Kelola jaringan
* ... dan segalanya!

---

## 🧠 Kenapa Harus Belajar CLI?

* 💨 Lebih cepat daripada GUI
* 🧰 Bisa diakses lewat SSH dari mana saja
* 🖥️ CLI adalah "bahasa native" sistem Linux (termasuk Proxmox)

💬 *"Tapi aku takut salah ketik!"*
Tenang, kita akan mulai dari perintah aman dan umum dulu!

---

## 🔐 Apa Itu SSH?

SSH (Secure Shell) adalah protokol untuk **mengakses server dari jarak jauh secara aman**.

Dengan SSH, kamu bisa:

* Remote login ke server Proxmox
* Jalankan perintah seolah-olah kamu duduk langsung di depan server
* Transfer file antar komputer/server

Contoh login SSH:

```bash
ssh root@192.168.1.100
```

---

## 🧰 Perintah Dasar CLI

| Perintah         | Fungsi                            |
| ---------------- | --------------------------------- |
| `pwd`            | Tampilkan folder saat ini         |
| `ls -lah`        | Lihat isi folder (detail)         |
| `cd nama_folder` | Masuk ke folder                   |
| `mkdir`          | Buat folder baru                  |
| `cp`, `mv`, `rm` | Copy, pindah, hapus file/folder   |
| `nano` / `vim`   | Edit file teks                    |
| `apt install`    | Install aplikasi di Debian/Ubuntu |
| `df -h`          | Cek kapasitas disk                |

💡 *Khusus Proxmox*, CLI digunakan untuk kontrol:

* VM
* Storage
* Network
* Backup
* Upgrade system

---

## 🔌 Cara SSH ke Server

### 1. Dari Linux/Mac:

```bash
ssh [user]@[IP-address]
```

### 2. Dari Windows:

Gunakan:

* [x] `PowerShell` → langsung pakai `ssh`
* [x] Aplikasi seperti [PuTTY](https://www.putty.org)

---

## 🔐 Autentikasi SSH

SSH biasanya pakai:

* Username + password
* atau: Public Key (lebih aman)

Contoh membuat key:

```bash
ssh-keygen
ssh-copy-id dwi@192.168.1.100
```

---

## 🧪 Mini Latihan

> 🧩 Coba akses server Proxmox kamu (kalau sudah install) via SSH dari laptop kamu.
> Gunakan perintah:

```bash
ssh root@192.168.1.123
```

Jika berhasil, kamu akan masuk ke shell root Proxmox! 🚀

---

## 🧠 Pertanyaan Reflektif

* Apa manfaat CLI dibanding GUI?
* Kapan kamu perlu akses Proxmox via SSH?
* Apa bedanya login SSH dengan key vs password?

---

📍 Next: [`09_Kenalan_dengan_Proxmox.md`](09_Kenalan_dengan_Proxmox.md) Di bab berikutnya kita akan masuk ke dunia Proxmox itu sendiri — server virtualisasi super keren yang akan jadi medan petualangan utama kita! 🎮🖥️


