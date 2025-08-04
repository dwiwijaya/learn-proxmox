# 💿 08 - Menambahkan ISO VM dan Template LXC ke Proxmox

Sebelum kita bisa bikin Virtual Machine (VM) atau Container (LXC), kita butuh bahan mentahnya dulu.

- Untuk VM: kita butuh **ISO file** (seperti CD installer)
- Untuk LXC: kita butuh **Template Container** (.tar.gz)

Bayangkan ini kayak kamu mau masak, kamu butuh bahan utamanya dulu sebelum bisa ngulek bumbunya 🍳✨

---

## 🧱 Apa Itu ISO File?

File **`.iso`** adalah image dari installer sistem operasi, contohnya:

- Ubuntu Server: `ubuntu-22.04-live-server-amd64.iso`
- Debian: `debian-12.5.0-amd64-netinst.iso`
- Windows: `Win10_22H2_English_x64.iso`

> ISO adalah file bootable yang akan digunakan untuk menginstall OS ke VM.

---

## 📦 Apa Itu Template LXC?

Proxmox juga mendukung **LXC Container** — lebih ringan dari VM.  
Untuk menjalankannya, kita butuh **template LXC**, seperti:

- `debian-12-standard_20240611_amd64.tar.zst`
- `ubuntu-22.04-standard_20240701_amd64.tar.zst`
- `alpine-3.19-default_20240512_amd64.tar.xz`

> Ini adalah sistem operasi mini, tanpa kernel sendiri, dan berjalan langsung di atas host.

---

## 📂 Di Mana Tempat Simpan ISO & Template?

| Jenis File  | Lokasi Default di Proxmox                 |
|-------------|--------------------------------------------|
| ISO         | `/var/lib/vz/template/iso/`               |
| LXC Template| `/var/lib/vz/template/cache/`             |

> 📁 Kamu bisa akses ini dari WebUI juga, jadi nggak harus lewat terminal.

---

## 🧰 Cara Upload ISO dari WebUI
![Upload ISO Images](https://www.tecmint.com/wp-content/uploads/2023/12/Proxmox-ISO-Image.png)
1. Buka **WebUI Proxmox**
2. Klik menu `Datacenter` → pilih node kamu → masuk ke tab `local`
3. Klik tab **"ISO Images"**
4. Klik tombol **Upload**
5. Pilih file `.iso` dari komputer kamu
6. Tunggu proses selesai ⏳

> 💡 Kamu juga bisa drag & drop langsung ke WebUI!

---

## 📡 Download Template LXC Otomatis
![Download Template LXC](https://www.tecmint.com/wp-content/uploads/2024/01/Proxmox-CT-Templates.png)
Kalau kamu ingin download langsung dari Proxmox:

1. Klik `local` → tab **CT Templates**
2. Klik tombol **Templates**
3. Pilih OS yang ingin kamu install
4. Klik Download

> Proxmox akan simpan template itu ke `/var/lib/vz/template/cache/`

---

## 🧠 Tips Memilih ISO / Template

| Kebutuhan                        | Saran ISO / Template                      |
|----------------------------------|-------------------------------------------|
| Belajar Linux dasar              | Ubuntu Server, Debian Minimal             |
| Server ringan                    | Alpine, Debian Minimal                    |
| LXC cepat & hemat resource       | Ubuntu LXC, Debian LXC                    |
| Testing aplikasi GUI             | Ubuntu Desktop ISO (butuh VM, bukan LXC)  |
| Belajar hosting / web server     | Debian + Nginx / Apache via LXC           |
| Full OS seperti Windows          | Gunakan ISO Windows (dalam VM)            |

---

## 🧪 Cek Via CLI (Opsional)

Kalau kamu penasaran, kamu bisa cek daftar ISO & template di server pakai perintah:

```bash
# Cek file ISO
ls /var/lib/vz/template/iso/

# Cek file template LXC
ls /var/lib/vz/template/cache/
