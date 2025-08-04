# 📝 Memahami Lisensi Proxmox — Gratis, Tapi Tetap Kuat!

Halo, calon admin server andal! 🙌  
Salah satu alasan utama banyak orang pakai **Proxmox VE** adalah karena dia **gratis dan open-source** — tapi tetap punya fitur kelas enterprise.

Tapi tunggu dulu...  
Kalau gratis, kok ada yang bilang harus bayar lisensi? 🤔

Yuk kita bahas tuntas biar nggak bingung lagi!

---

## 🧠 Teori Singkat: Jenis Lisensi Proxmox

Proxmox VE punya **2 jenis lisensi utama**:

| Jenis | Untuk Siapa | Fitur Teknis | Akses Support |
|-------|-------------|--------------|----------------|
| 🟢 **Community Edition (Gratis)** | Semua pengguna, open-source | 100% fitur lengkap | Tidak ada support resmi |
| 🔵 **Enterprise Subscription (Berbayar)** | Perusahaan, tim IT production | Sama dengan gratis | Dapat support teknis langsung dari tim Proxmox |

---

## ❓ Jadi, Gratis Tapi Lengkap?

Ya, **benar-benar lengkap!**  
Proxmox VE tidak mengunci fitur penting di versi gratis. Kamu tetap bisa:

✅ Membuat VM dan Container  
✅ Mengatur storage, snapshot, backup  
✅ Menyusun cluster dan HA  
✅ Akses Web UI dan CLI  
✅ Gunakan API dan monitoring  
✅ Full upgrade system pakai `apt`

Tapi ada **1 perbedaan teknis penting**:

---

## 📦 Perbedaan: Source Repository

Proxmox punya 2 jenis repo (sumber update software):

| Repo | Akses | Kualitas | Cara Dapat |
|------|-------|----------|-------------|
| `enterprise` | Hanya untuk lisensi berbayar | Teruji, stabil | Otomatis aktif setelah install |
| `no-subscription` | Gratis untuk semua | Stabil tapi bisa lebih cepat berubah | Harus diaktifkan manual

---

### 🛠️ Cara Ganti ke Repo Gratis

Setelah install, kamu akan dapat pesan seperti:
> “You do not have a valid subscription...”

Itu **normal** kalau kamu pakai versi gratis.

Cukup **ganti source list** dengan repo gratis:

```bash
sudo nano /etc/apt/sources.list.d/pve-enterprise.list
````

Ubah baris yang ada jadi komentar (tambah `#` di depannya), lalu tambahkan repo berikut:

```bash
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
```

Lalu update:

```bash
sudo apt update && sudo apt full-upgrade
```

Voila! 🎉 Kamu siap pakai versi gratis 100% fungsional.

---

## 💡 Kenapa Tetap Ada Versi Berbayar?

Karena Proxmox juga butuh biaya operasional.
Dengan membeli lisensi:

* Kamu bantu **dukungan pengembangan open-source**,
* Dapat **support teknis prioritas**,
* Cocok untuk **tim IT production** yang butuh SLA resmi.

---

## ⚖️ Haruskah Saya Bayar?

Itu tergantung kebutuhanmu:

| Kamu                          | Disarankan?                             |
| ----------------------------- | --------------------------------------- |
| Belajar sendiri / homelab     | ❌ Tidak wajib                           |
| Kantor kecil, budget terbatas | ❌ Tidak wajib, tapi hati-hati backup    |
| Infrastruktur perusahaan      | ✅ Sangat disarankan pakai support resmi |

---

## 🏁 Kesimpulan

> ✅ **Proxmox 100% bisa kamu gunakan secara gratis — tanpa dipangkas fiturnya.**
> Kamu hanya perlu tahu cara pakai repo yang tepat dan terima bahwa kamu tidak dapat dukungan resmi.

Kalau nanti sudah siap dan ingin kontribusi, kamu juga bisa bantu dengan:

* Beli lisensi resmi,
* Donasi ke proyek open-source,
* Atau bantu dokumentasi seperti repo ini! 😄

---

🔗 Selanjutnya: [📂 Struktur Repositori & Penjelasan Folder](Struktur_Repositori.md)


