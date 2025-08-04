# 🥊 04 - Perbedaan VM vs Container

Selamat datang di arena pertempuran virtual! ⚔️  
Di dunia Proxmox, kamu akan sering berurusan dengan dua jenis entitas: **Virtual Machine (VM)** dan **Container (LXC)**.

Nah, kita bahas perbedaan mereka yuk — supaya kamu bisa memilih yang tepat di setiap situasi.

---

## 💡 Apa Itu Virtual Machine (VM)?

> VM adalah komputer virtual lengkap yang menjalankan sistem operasi sendiri (guest OS) di atas hypervisor.

### 🔧 Ciri-ciri VM:
- Punya kernel dan OS sendiri
- Isolasi penuh dari host
- Lebih fleksibel (bisa Windows, Linux, dsb)
- Performa sedikit lebih berat karena virtualisasi penuh

> ⚙️ Contoh: Kamu bikin VM Ubuntu 22.04 dan install Apache di dalamnya.

---

## 📦 Apa Itu Container (LXC)?

> Container adalah lingkungan virtual ringan yang berbagi kernel dengan host, tapi terisolasi secara user space.

### 🔧 Ciri-ciri Container:
- **Berbagi kernel** dengan host (biasanya Linux)
- Sangat ringan dan cepat
- Lebih efisien dalam penggunaan resource
- Cocok untuk aplikasi Linux yang spesifik

> ⚙️ Contoh: Kamu bikin LXC container Debian dan langsung deploy NGINX.

---

## 🧠 Analogi Sederhana

Bayangkan kamu tinggal di sebuah gedung apartemen 🏢

- **VM** = Setiap unit apartemen punya dapur, toilet, listrik sendiri (penuh, mandiri)
- **Container** = Kamu tinggal di satu unit kos bareng, tapi tetap punya ruang pribadi (berbagi fasilitas, tapi tetap terpisah)

---

## ⚖️ Perbandingan VM vs Container

| Fitur | VM | Container (LXC) |
|-------|----|-----------------|
| Kernel | Terpisah | Berbagi dengan host |
| OS | Bisa OS apapun | Harus Linux |
| Isolasi | Lebih kuat | Cukup kuat (tapi berbagi kernel) |
| Kecepatan | Lebih lambat | Super cepat |
| Overhead | Lebih besar | Ringan |
| Use Case | Windows/Linux VM, aplikasi kompleks | App ringan, microservice, dev/test |
| Backup | Snapshot & backup penuh | Snapshot & backup cepat juga |

---

## 💬 Kapan Pilih VM?

- Butuh OS non-Linux (misal: Windows Server)
- Perlu isolasi penuh (misal: tenant berbeda)
- Jalankan aplikasi yang membutuhkan kernel spesifik

## 💬 Kapan Pilih Container?

- Aplikasi ringan berbasis Linux
- Butuh performa tinggi dengan overhead rendah
- Banyak instance kecil (misal: microservice, dev environments)

---

## 📍 Di Proxmox...

> Proxmox mendukung **dua-duanya** — kamu bisa campur antara VM dan LXC Container sesuai kebutuhan!

Contohnya:
- 🔒 VM → Untuk server Windows + database penting
- 🚀 LXC → Untuk web app ringan, proxy, monitoring tool

---

## 🧠 Pertanyaan Reflektif

- Mengapa LXC lebih ringan dibanding VM?
- Apakah mungkin menjalankan Windows dalam container?
- Kapan kamu memilih VM, bukan container?

---

🎯 Ayo lanjut ke materi berikutnya:
👉 [`05_Linux_dan_Dasar_Dasarnya.md`](05_Linux_dan_Dasar_Dasarnya.md)

Karena baik VM maupun LXC di Proxmox banyak yang pakai Linux, kamu perlu mengenalnya lebih dalam dulu! 🐧
