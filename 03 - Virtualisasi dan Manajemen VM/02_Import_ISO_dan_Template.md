# 💿 02 - Menambahkan ISO VM dan Template LXC ke Proxmox

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

| Istilah          | Penjelasan Singkat                                                                                  |
| ---------------- | --------------------------------------------------------------------------------------------------- |
| **ISO File**     | File image dari sistem operasi (Windows, Ubuntu, Debian, dsb) yang digunakan untuk install VM (KVM) |
| **LXC Template** | File berisi OS ringan siap pakai untuk membuat container LXC dengan cepat                           |

---

## 🗃️ Pilih Storage yang Tepat: local vs local-lvm

Saat kamu upload file di Proxmox, kamu akan diminta pilih storage — biasanya muncul dua:

| Storage     | Tipe                         | Kegunaan                                       | Bisa Upload ISO? | Bisa Akses dari Terminal?                      |
| ----------- | ---------------------------- | ---------------------------------------------- | ---------------- | ---------------------------------------------- |
| `local`     | Directory-based              | Disimpan sebagai file biasa (di `/var/lib/vz`) | ✅ Ya             | ✅ Ya                                           |
| `local-lvm` | LVM (Logical Volume Manager) | Volume block untuk VM/CT                       | ❌ Tidak          | ❌ Tidak (tidak langsung terlihat sebagai file) |

📌 **Kesimpulan:**

* Gunakan `local` untuk menyimpan file ISO atau template LXC.
* Gunakan `local-lvm` untuk menyimpan disk VM atau container yang butuh performa lebih tinggi.

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
```

## ✅ Checklist Sebelum Lanjut

| Hal yang Dicek                              | Sudah? |
| ------------------------------------------- | ------ |
| Sudah upload minimal 1 ISO OS untuk VM      | ☑️     |
| Sudah download minimal 1 LXC template       | ☑️     |
| Sudah tahu perbedaan `local` vs `local-lvm` | ☑️     |
| Tahu lokasi file ISO dan template           | ☑️     |

---

## 📌 Catatan Penting

* Gunakan **storage `local`** untuk menyimpan ISO dan template
* **`local-lvm` tidak bisa digunakan** untuk menyimpan file `.iso` atau `.tar.gz`
* Kamu **harus upload ISO** dulu sebelum membuat VM
* Kamu **harus download template LXC** dulu sebelum membuat container

---

## 📍 Lanjut ke: [`03_Membuat_VM_Baru.md`](03_Membuat_VM_Baru.md)
Siapkan tanganmu, karena selanjutnya kita akan benar-benar membangun VM pertama dari nol! 💻⚙️
Gaskeun!




