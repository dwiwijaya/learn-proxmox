# 🔧 07 - Update Repository dan Lisensi CE(N)PH Non-Subscription

Saat kamu pertama kali install Proxmox, kemungkinan besar kamu akan nemu pesan seperti ini:

> 🔴 **"You do not have a valid subscription for this server"**

Tenang, itu **nggak berarti Proxmox kamu rusak atau ilegal**.  
Ini hanya peringatan karena kamu pakai versi **Community Edition (tanpa subscription)**.

---

## 🧠 Apa Itu Repository di Linux?

Bayangkan **repository (repo)** itu seperti toko paket software resmi milik sistem operasi Linux.

📦 Saat kamu ingin:
- Menginstall software
- Update keamanan
- Upgrade sistem

…semuanya dilakukan lewat **package manager**.  
Di Debian (termasuk Proxmox), package manager-nya adalah `apt`.

### 🔍 Istilah Penting:

| Istilah       | Penjelasan                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `apt`         | Alat untuk install/update software di Debian/Ubuntu/Proxmox                 |
| `repository`  | Lokasi server tempat download software/paket                                |
| `sources.list`| File yang menyimpan daftar repo yang digunakan                              |
| `pve-enterprise` | Repo resmi untuk user yang bayar lisensi Proxmox                         |
| `pve-no-subscription` | Repo gratis komunitas, untuk publik/non-lisensi                     |

---

## 🔓 Apa Itu Lisensi Proxmox?

Proxmox menawarkan dua versi:

| Versi                 | Fitur                      | Cocok Untuk             |
|-----------------------|----------------------------|--------------------------|
| **Enterprise**        | Full support + update repo stabil | Production perusahaan besar |
| **Community (No Sub)**| Gratis, semua fitur bisa diakses | Lab, testing, personal, startup |

> ✅ Semua fitur tetap tersedia meskipun kamu tidak punya subscription.

---

## 😵 Masalah Saat Update?

Kalau kamu mencoba update tanpa mengganti repo, kamu akan dapat error seperti ini:

```bash
W: http://enterprise.proxmox.com/debian/pve ... 403 Forbidden
````

Itu karena repo default mengarah ke **enterprise**, yang butuh langganan.

---

## ✅ Solusi: Ubah ke Repository Gratis

### 1. Backup Dulu File Repository:

```bash
cp /etc/apt/sources.list.d/pve-enterprise.list /etc/apt/sources.list.d/pve-enterprise.list.backup
```

### 2. Nonaktifkan Repo Enterprise:

```bash
nano /etc/apt/sources.list.d/pve-enterprise.list
```

Comment isinya jadi seperti ini:

```bash
# deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

### 3. Tambahkan Repo Community:

Edit file `sources.list` utama:

```bash
nano /etc/apt/sources.list
```

Tambahkan baris ini di bagian bawah:

```
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
```

> Ganti `bookworm` sesuai dengan versi Debian kamu (`bullseye`, `buster`, dst)

### 4. Update dan Upgrade:

```bash
apt update && apt full-upgrade -y
```

---

## 🧼 Menghilangkan Peringatan "No Valid Subscription"

Peringatan ini cuma kosmetik, **tidak mempengaruhi fitur**. Tapi kalau kamu risih, bisa di-nonaktifkan dengan patch kecil:

```bash
sed -i.bak "s/data.status !== 'Active'/false/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js
```

Lalu restart WebUI:

```bash
systemctl restart pveproxy
```

> ⚠️ Akan ter-reset saat update Proxmox, jadi ini opsional ya.

---

## 🧠 Bonus: Mengenal Sekilas Tentang CEPH dan Lisensinya

CEPH adalah sistem storage terdistribusi (clustered storage) yang didukung penuh oleh Proxmox.
Kalau kamu menggunakan CEPH di production, disarankan punya lisensi.
Tapi untuk belajar dan testing pribadi? Jalan terus! 💪

---

## 📘 Kesimpulan

| Hal                  | Status Tanpa Lisensi         |
| -------------------- | ---------------------------- |
| Instalasi Proxmox    | ✅ Bisa penuh                 |
| Update sistem        | ✅ Bisa via repo non-sub      |
| Gunakan CEPH         | ✅ Bisa (manual setup)        |
| Support dari Proxmox | ❌ Tidak dapat (kecuali beli) |

---

## 🎯 Tugas Mandiri

✅ Matikan repo enterprise   
✅ Tambahkan repo no-subscription   
✅ Update dan pastikan tidak error   
✅ Opsional: hilangkan warning "no subscription"   

---

📍 Lanjut ke: [`08_Menambahkan_ISO_VM_dan_Template_LXC.md`](08_Menambahkan_ISO_VM_dan_Template_LXC.md)   
Saatnya kamu mulai memasukkan "bahan baku" untuk bikin mesin virtual 💿👨‍💻

