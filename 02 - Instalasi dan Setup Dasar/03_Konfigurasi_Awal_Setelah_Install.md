# ⚙️ 03 - Konfigurasi Awal Setelah Install

Yes! Proxmox VE-mu sudah berhasil diinstall 🎉  
Sekarang saatnya kita rapikan beberapa hal penting agar kamu bisa mulai dengan nyaman dan aman.

---

## 🎯 Tujuan Bab Ini

- Login ke WebUI dan CLI
- Nonaktifkan subscription warning (tanpa bajakan ya!)
- Update sistem dan repo
- Sinkronisasi waktu (NTP)
- Menambahkan user (opsional)

---

## 🔑 Login ke WebUI

1. Akses `https://<IP-Proxmox>:8006`
2. Login pakai:
   - **Username**: `root`
   - **Password**: yang kamu buat saat install
   - **Realm**: `Linux PAM`

> ❗ Abaikan warning SSL di awal, itu normal karena sertifikatnya self-signed.

---

## ⚠️ Nonaktifkan "No Valid Subscription" Warning

Secara default, Proxmox akan menampilkan popup karena kita belum pakai **Proxmox Subscription**.

Tenang, kita tetap bisa pakai fitur lengkap Proxmox **gratis dan legal** via *Community Repository*.

### Nonaktifkan popup via WebUI (Proxmox 8+)

1. Masuk WebUI
2. Klik **Datacenter** → **Subscription**
3. Klik: **Disable subscription notification**

✅ Popup hilang, tidak perlu edit JS lagi!

---

## 🔁 Update Repository ke Community Edition

Secara default, Proxmox pakai repo *enterprise* (butuh subscription).  
Kita perlu ubah ke versi community (gratis):

### Edit file repo:
```bash
sudo nano /etc/apt/sources.list.d/pve-enterprise.list
````

Ubah:

```bash
deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

Menjadi:

```bash
# deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

### Tambahkan repo community:

```bash
echo "deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription" | sudo tee /etc/apt/sources.list.d/pve-install-repo.list
```

### Update sistem:

```bash
sudo apt update
sudo apt full-upgrade -y
```

---

## ⏰ Sinkronisasi Waktu (NTP)

Pastikan waktu server akurat.

### Cek status:

```bash
timedatectl status
```

### Atur timezone (jika perlu):

```bash
sudo timedatectl set-timezone Asia/Jakarta
```

### Install NTP (jika belum):

```bash
sudo apt install systemd-timesyncd -y
```

---

## 👥 Menambahkan User Akses (Opsional)

Kamu bisa buat user tambahan jika ingin akses WebUI tanpa pakai root.

### Contoh:

```bash
sudo adduser devops
```

Lalu atur role dan permission via WebUI:

* **Datacenter → Permissions → Add**
* Pilih user, role (misal: PVEAdmin), dan path (`/` untuk full akses)

---

## 🎯 Tugas Mandiri

✅ Nonaktifkan subscription warning   
✅ Ganti repo ke community edition   
✅ Lakukan update sistem   
✅ Cek waktu dan sinkronisasi timezone   
✅ Tambah user kalau perlu   

---

📍 Lanjut ke: [`04_Mengenal_WebUI_dan_Pengaturan_Dasar.md`](04_Mengenal_WebUI_dan_Pengaturan_Dasar.md)   
Kita akan keliling dulu di dalam WebUI dan bahas fitur-fitur utama Proxmox 🎛️✨

