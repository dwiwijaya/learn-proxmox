# 📦 04 - Membuat LXC Container di Proxmox

Setelah berhasil membuat Virtual Machine, sekarang kita akan coba cara virtualisasi lain yang lebih ringan dan efisien: **LXC Container**! 🚀

---

## 🎯 Tujuan Bab Ini

- Memahami apa itu container dan bagaimana cara kerjanya
- Membuat LXC container pertama di Proxmox
- Mengetahui kelebihan dan batasan container dibanding VM

---

## 🧠 Apa Itu Container (LXC)?

Container adalah unit virtualisasi yang **lebih ringan** daripada VM.  
Alih-alih menjalankan sistem operasi lengkap seperti VM, container berbagi kernel dengan host, tapi tetap berjalan secara terisolasi.

> ⚙️ **LXC (Linux Container)** adalah teknologi container native Linux yang dipakai oleh Proxmox.

---

### 🧃 Analogi: VM vs Container

Bayangkan kamu ingin menjalankan banyak aplikasi.

- **VM** seperti rumah lengkap, tiap rumah punya lahan sendiri, dapur, listrik, bahkan saluran air sendiri.
- **Container** seperti apartemen — lebih hemat ruang, satu gedung (kernel) bisa menampung banyak unit (aplikasi terisolasi), tapi tetap bisa hidup mandiri.

---

## 🏁 Persiapan Sebelum Membuat Container

Sebelum mulai, pastikan kamu sudah:

✅ **Download template LXC** terlebih dahulu.  
Template ini seperti blueprint OS yang akan digunakan oleh container.

Bisa didownload lewat antarmuka Proxmox:

1. Masuk ke menu **`local`** storage  
2. Klik tab **CT Templates**  
3. Klik **Templates** → pilih salah satu (misal `debian-12-standard`) → klik **Download**

---

## 🧪 Langkah-Langkah Membuat LXC Container

### 1️⃣ Klik Tombol **Create CT**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Proxmox-Create-Template.png)
Buka antarmuka Proxmox ➡️ klik node ➡️ pilih **Create CT**.

---

### 2️⃣ Tab: **General**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Proxmox-Container-Details.png)
| Field    | Penjelasan                          |
|----------|--------------------------------------|
| Node     | Server tempat container akan dijalankan |
| CT ID    | Nomor unik container (otomatis)     |
| Hostname | Nama container (misal: `lxc-debian`) |
| Password | Password untuk login ke dalam container |

---

### 3️⃣ Tab: **Template**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Choose-Fedora-Container-Template.png)
- Pilih template yang sudah kamu download tadi (misal `debian-12-standard_*.tar.zst`)

📝 Kalau belum ada, balik dulu ke langkah sebelumnya untuk mendownloadnya.

---

### 4️⃣ Tab: **Root Disk**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Set-Disk-for-Container-Image.png)
| Opsi       | Penjelasan                        |
|------------|-----------------------------------|
| Storage    | Di mana container disimpan        |
| Disk Size  | Ukuran root (misal 8 GB, 16 GB)   |

Karena container ringan, kamu bisa alokasikan ruang lebih kecil dari VM.

---

### 5️⃣ Tab: **CPU**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Set-CPU-for-Container-Image.png)
- **Cores**: Alokasikan core sesuai kebutuhan (1–2 cukup untuk testing)

---

### 6️⃣ Tab: **Memory**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Set-Memory-for-Container-Image.png)
- **RAM**: 512 MiB – 2048 MiB, tergantung kebutuhan
- Aktifkan ballooning jika ingin

---

### 7️⃣ Tab: **Network**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Set-Network-for-Container-Image.png)
- Pilih bridge `vmbr0`
- Model: `virtio` atau `default`

Container juga bisa dapat IP seperti VM biasa dan terhubung ke jaringan.

---

### 8️⃣ Tab: **DNS**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Network-DNS-Settings.png)
- Biarkan default atau sesuaikan dengan DNS server lokal

---

### 9️⃣ Tab: **Confirm**
![Set](https://www.tecmint.com/wp-content/uploads/2024/01/Proxmox-Container-Settings.png)
- Klik **Finish**, dan container akan langsung dibuat!

---

## 🚀 Menjalankan & Mengakses Container

Setelah container dibuat:

1. Klik kanan pada container → **Start**
2. Klik **Console** untuk mulai menggunakan

Jika OS mendukung SSH dan sudah diaktifkan, kamu juga bisa remote via `ssh` seperti server biasa.

---

## ✅ Kelebihan dan Batasan LXC

| Aspek      | LXC Container                     | Virtual Machine (KVM)             |
|------------|----------------------------------|-----------------------------------|
| Performa   | Lebih cepat & ringan             | Lebih berat                       |
| Isolasi    | Kurang dari VM                   | Lebih kuat                        |
| OS Support | Hanya Linux                      | Linux, Windows, BSD, dll          |
| Resource   | Sangat hemat RAM & disk          | Butuh alokasi lebih besar         |

> 🧠 Gunakan **LXC** jika kamu butuh banyak server Linux ringan, misalnya untuk microservice, lab, atau testing jaringan.

---

## 🧪 Tips Penggunaan

- LXC cocok untuk web server ringan (nginx, apache)
- Cocok juga untuk lab jaringan
- Tidak cocok untuk OS non-Linux (misalnya Windows)

---

## 🎯 Tugas Mandiri

✅ Download minimal 1 LXC template (misal: Debian, Alpine)  
✅ Buat 1 container ringan  
✅ Coba akses via Console, dan install tool dasar seperti `htop`, `ping`, dll

---

## 🔗 Selanjutnya: [`05_Manajemen_VM_dan_Container.md`](05_Manajemen_VM_dan_Container.md)

Setelah punya VM dan Container, sekarang saatnya belajar cara **mengelolanya**!  
Mulai dari **start/stop, rename, resize, hingga konversi antar jenis virtualisasi** 🛠️🧠

Siap jadi master manajemen? Yuk lanjut! 🚀
