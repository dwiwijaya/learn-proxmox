# 🧭 05 - Manajemen VM dan Container

Selamat! Sekarang kamu sudah punya **VM dan Container pertama** di Proxmox 🎉  
Tapi petualangan belum selesai... Justru sekarang kamu masuk ke fase baru: **mengelola** mereka!

---

## 🎯 Tujuan Bab Ini

- Mengenal operasi dasar VM dan Container di Proxmox
- Menjalankan, menghentikan, dan menghapus VM/CT dengan aman
- Melakukan rename, update config, dan mengelola resource ringan

---

## 🧠 Apa Itu Manajemen VM/CT?

Setelah membuat VM atau Container, kamu perlu tahu cara **mengendalikannya**.  
Mulai dari start, stop, reboot, sampai atur resource seperti CPU, RAM, dan disk.

> 🎮 Anggap saja kamu adalah "Game Master" dan VM/CT adalah karaktermu. Kamu bisa hidupkan, hibernasi, ganti kostum (resource), bahkan hapus kalau sudah tidak dipakai.

---

## 🧪 Operasi Dasar VM/Container

Kamu bisa klik kanan pada VM/CT atau pilih melalui toolbar atas. Berikut ini fungsi-fungsi dasarnya:   
![](https://forum.proxmox.com/data/attachments/88/88475-6fc6e0ace9b03ac47ae66adcb413a076.jpg?hash=ZwnZ1ZrwVJ)   
### ▶️ Start

- Menyalakan VM/CT
- Seperti tombol power di komputer 💻

### ⏹ Stop

- Mematikan paksa VM/CT (seperti mencabut listrik)
- Gunakan **Shutdown** dulu kalau memungkinkan!

### 🔁 Reboot

- Restart sistem (mirip tekan tombol restart di PC)

### 💤 Shutdown

- Mematikan VM/CT dengan aman (butuh OS support)
- Gunakan ini daripada langsung Stop

---

## ✏️ Rename VM/CT

Sayangnya, **Proxmox tidak punya fitur rename langsung**.  
Kalau ingin rename, kamu harus:

1. **Stop VM/CT**
2. **Clone ke ID baru dengan nama baru**
3. Hapus VM/CT lama (opsional)

> 🛑 Pastikan semua data penting sudah dipindah atau backup dulu sebelum hapus ya!

---

## ⚙️ Edit Konfigurasi

Klik nama VM/CT → buka tab **Hardware**. Di sini kamu bisa:

| Komponen | Fungsi                            |
|----------|-----------------------------------|
| CPU      | Ubah jumlah core                  |
| Memory   | Ubah alokasi RAM                  |
| Disk     | Resize (untuk `qcow2` atau LVM)   |
| Network  | Tambah, hapus, atau edit NIC      |

> 📦 Kamu bisa resize disk hanya jika VM dimatikan dan storage mendukung resize (misal `qcow2`).

---

## 🧼 Menghapus VM/Container

Jika kamu ingin membersihkan node:

1. **Stop dulu** VM/CT-nya
2. Klik kanan → **Remove**
3. Proxmox akan menghapus semua file terkait

> 🧠 Jangan lupa backup dulu kalau datanya penting!

---

## 🖥 CLI Command Tambahan (Opsional)

Buat kamu yang mulai nyaman pakai terminal, ini beberapa perintah CLI:

```bash
# List semua VM dan CT
qm list
pct list

# Menyalakan VM/CT
qm start <vmid>
pct start <ctid>

# Mematikan
qm stop <vmid>
pct stop <ctid>

# Reboot
qm reboot <vmid>
pct reboot <ctid>

# Menghapus
qm destroy <vmid>
pct destroy <ctid>
````

> `qm` = untuk Virtual Machine
> `pct` = untuk Container

---

## 💡 Tips Manajemen Harian

* Gunakan **tags** (label warna) untuk menandai VM penting, dev, test, dsb
* Tandai container kecil untuk service tertentu (misal: `web-nginx`, `db-test`)
* Backup dulu sebelum resize, clone, atau remove

---

## 📌 Studi Kasus Mini

| Kebutuhan                         | Solusi Proxmox                 |
| --------------------------------- | ------------------------------ |
| VM lambat                         | Tambah core atau RAM           |
| Nama VM tidak jelas               | Clone ke nama baru, hapus lama |
| Container butuh lebih banyak disk | Resize disk container          |
| Banyak VM test menumpuk           | Remove yang tidak dipakai      |

---

## 🎯 Tugas Mandiri

✅ Coba **start-stop-reboot** VM dan Container
✅ Coba resize RAM atau CPU (ubah dari tab Hardware)
✅ Hapus satu container test yang tidak terpakai

---

## 🔗 Selanjutnya: [`06_Clone_dan_Template_VM.md`](06_Clone_dan_Template_VM.md)

Mau bikin banyak VM/CT serupa tanpa install ulang satu per satu?
Di bab selanjutnya, kita akan belajar **Clone dan Template** — rahasia hemat waktu para sysadmin! 🔁🧪

Yuk lanjut petualangannya! ⚡

