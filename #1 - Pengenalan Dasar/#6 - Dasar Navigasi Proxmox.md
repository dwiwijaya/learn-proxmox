# 🧭 #6 - Dasar Navigasi Proxmox

Selamat datang di dashboard Proxmox VE! 🎉  
Ibaratnya ini adalah **ruang kendali utama**, tempat kamu bisa memantau, mengatur, dan mengontrol semua virtualisasi yang kamu buat.

Sama seperti kamu belajar naik sepeda 🚲 — di sini kamu akan mulai kenalan dengan tombol-tombol penting dulu, biar nanti nggak bingung!

---

## 🖼️ Tampilan Antarmuka Proxmox

![Tampilan Dashboard Proxmox](https://contabo.com/blog/wp-content/uploads/2019/11/webinterface_start_marked-1024x513.png)

Mari kita jelaskan bagian-bagian pentingnya dari gambar di atas:

### 🔹 A - Struktur Navigasi Server
Ini adalah panel kiri tempat kamu bisa melihat:
- **Datacenter**: Level paling atas, berisi semua node/server.
- **Node (vmid20904)**: Server fisik Proxmox kamu. Klik ini untuk melihat atau mengatur detailnya.
- **Local (Storage)**: Media penyimpanan lokal untuk ISO, disk VM/CT, template, backup, dll.

### 🔹 B - Menu Fitur Utama
Setelah kamu klik node, akan muncul berbagai tab/menu:
- **Summary**: Ringkasan status node.
- **Ceph**: Untuk konfigurasi storage cluster (opsional).
- **Options, Storage, Backup**: Pengaturan penyimpanan & cadangan.
- **Replication, Permissions, Firewall**: Pengaturan lanjutan.
- **HA**: High Availability, untuk cluster dengan failover otomatis.

### 🔹 C - Health & Status Panel
Panel utama di tengah menunjukkan:
- Status node: Online/Offline
- Jumlah VM & Container aktif
- Resource usage (CPU, RAM, Storage)

### 🔹 D - Task Log Panel
Panel bawah menampilkan log semua aktivitas seperti:
- Pembuatan VM
- Proses backup
- Reboot atau shutdown
- Error atau proses yang sedang berjalan

---

## 🔐 Login & Akses Web UI

Kamu bisa login ke Proxmox dengan browser:  
`https://<ip-server>:8006`

Gunakan user: `root@pam` dan password server kamu.

---

## ⚠️ Tentang Subscription Warning

> "No valid subscription"

Tenang! 😌 Ini cuma peringatan kalau kamu tidak menggunakan versi enterprise (berbayar).  
Untuk belajar dan setup pribadi, **versi komunitas 100% bisa dipakai** tanpa kendala.

---

## 🎉 Penutup

Sekarang kamu sudah:
✅ Kenal dengan struktur antarmuka Proxmox  
✅ Tahu di mana pengaturan penting berada  
✅ Bisa memantau resource dan melihat aktivitas sistem

---

🎯 Yuk lanjut belajar cara bikin VM dan Container!

🔗 Lanjut ke [#7 - Membuat VM dan Container.md](./#7%20-%20Membuat%20VM%20dan%20Container.md)
