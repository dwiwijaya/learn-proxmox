# 🧠 02 - Pengenalan Virtualisasi

Selamat datang di gerbang dunia virtual! 🌐  
Di sinilah petualangan Proxmox sebenarnya dimulai.

---

## 🤖 Apa Itu Virtualisasi?

> Virtualisasi adalah proses membuat versi virtual dari sesuatu — biasanya komputer, server, sistem operasi, storage, atau jaringan.

Dengan virtualisasi, kamu bisa:
- Menjalankan **beberapa komputer virtual** dalam 1 mesin fisik
- Menghemat biaya dan ruang
- Meningkatkan efisiensi penggunaan hardware

---

## 💡 Analogi Sederhana

Bayangkan kamu punya rumah (komputer fisik), lalu kamu bagi rumah itu menjadi:
- Kamar A untuk server database
- Kamar B untuk web server
- Kamar C untuk testing

Semua kamar ini tinggal di **rumah yang sama**, tapi **berjalan seperti rumah terpisah**.

Itulah virtualisasi. Satu mesin fisik → banyak mesin virtual di dalamnya.

---

## 🧱 Manfaat Virtualisasi

| Manfaat | Penjelasan |
|---------|------------|
| 💰 Hemat Biaya | Tidak perlu beli banyak server fisik |
| ⚙️ Efisiensi Hardware | CPU dan RAM bisa dibagi lebih optimal |
| 🔁 Mudah Dikelola | Bisa backup, restore, pindah-pindah |
| 🔒 Isolasi Aman | VM satu tidak mempengaruhi yang lain |
| 🧪 Cocok untuk Lab / Testing | Bisa bikin dan hapus mesin virtual dengan cepat |

---

## ⚙️ Komponen Utama dalam Virtualisasi

1. **Host Machine**  
   Komputer fisik tempat semua VM berjalan (tempat Proxmox di-install)

2. **Guest Machine**  
   Mesin virtual (VM) yang berjalan di atas host — bisa Windows, Linux, dll

3. **Hypervisor**  
   Software yang memungkinkan virtualisasi terjadi  
   (Kita bahas detailnya di file berikutnya)

---

## 📦 Jenis Virtualisasi

| Jenis | Penjelasan | Contoh |
|------|-------------|--------|
| Virtualisasi Server | Jalankan banyak OS dalam 1 server | Proxmox, VMware ESXi |
| Virtualisasi OS | Jalankan aplikasi dalam container | Docker, LXC |
| Virtualisasi Storage | Gabungkan banyak storage menjadi satu pool | ZFS, Ceph |
| Virtualisasi Jaringan | Buat jaringan virtual untuk VM | Linux Bridge, OVS |

---

## 🚩 Virtualisasi dalam Dunia Nyata

Tanpa virtualisasi:
- Kamu butuh 5 server fisik untuk 5 aplikasi

Dengan virtualisasi:
- Cukup 1 server fisik → 5 VM → masing-masing jalanin aplikasinya

Itulah kenapa data center modern dan cloud (seperti AWS, Azure, GCP) **semua berbasis virtualisasi**.

---

## 🧠 Pertanyaan Reflektif

- Apa manfaat utama virtualisasi dalam hal biaya dan efisiensi?
- Apa perbedaan host dan guest?
- Apakah kita bisa menjalankan Windows di atas Linux lewat virtualisasi?

---

📍 Selanjutnya kita akan bahas:  
👉 [`03_Tipe_Hypervisor.md`](03_Tipe_Hypervisor.md)  
Ayo lanjut, biar makin dalam pahamnya! 🚀
