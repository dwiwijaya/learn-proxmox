# 📦 #7 - Membuat VM dan Container di Proxmox

Selamat! Sekarang kamu sudah sampai pada tahap membuat sistem baru dalam dunia virtual 🖥️✨  
Kita akan belajar dua hal penting:

1. 🖥️ **Virtual Machine (VM)**: Ibarat rumah sendiri, lengkap dengan perabotan dan sekatnya.
2. 📦 **Container (LXC)**: Seperti kos-kosan efisien—berbagi tembok, tapi tetap bisa hidup mandiri.

---

## 🔧 Persiapan Awal

Sebelum membuat VM atau LXC, pastikan kamu sudah:

- Mengunggah **ISO file** OS yang akan diinstal (untuk VM)
- Mengaktifkan fitur **Container** jika ingin membuat LXC
- Punya cukup resource (RAM, storage)

### Cara upload ISO:
![Tampilan Node](https://contabo.com/blog/wp-content/uploads/2019/11/upload_ISO_marked.png.webp)
1. Klik node kamu → `local` (storage)
2. Pilih tab **Content** > `Upload`
3. Pilih file `.iso` dari komputermu

---

## 🖥️ Membuat Virtual Machine

1. Klik tombol **Create VM** (kanan atas)   
   ![Tampilan Node](https://contabo.com/blog/wp-content/uploads/2019/11/pve_create_VM.png.webp)
3. Masukkan **ID dan Nama VM**   
   ![Tampilan Node](https://contabo.com/blog/wp-content/uploads/2023/08/pve_new_1.png.webp)
4. Pilih **ISO image** (misal: Centos Server)    
   ![Tampilan Node](https://contabo.com/blog/wp-content/uploads/2023/08/pve_new_2.png.webp)
6. Atur:    
   ![Tampilan Node](https://contabo.com/blog/wp-content/uploads/2019/11/pve_new_8.png.webp)
   - Disk: ukuran & storage
   - CPU: core & soket
   - RAM: jumlah memori   

8. Pilih jaringan (default: `vmbr0`)
9. Klik Finish ✅


VM siap digunakan!  
Klik kanan → `Start`, lalu buka konsolnya untuk instal OS.

---

## 📦 Membuat Container (LXC)

1. Klik **Create CT**
2. Masukkan:
   - ID dan hostname
   - Password user root
3. Pilih template OS (harus diunduh dulu dari menu **CT Templates**)
4. Atur resource seperti RAM, CPU, dan storage
5. Finish!  

Container lebih ringan dan lebih cepat dari VM—cocok untuk microservice atau dev server.

---

## ❓ VM vs LXC, Pilih Mana?

| Fitur         | VM                         | LXC (Container)             |
|---------------|----------------------------|-----------------------------|
| Isolasi       | Full (sendiri-sendiri)     | Ringan, berbagi kernel      |
| OS            | Bisa install bebas         | Harus pakai Linux           |
| Resource      | Lebih boros                | Lebih hemat                 |
| Kecepatan     | Lebih lambat sedikit       | Sangat cepat                |

Kalau kamu butuh fleksibilitas penuh (misal install Windows), pakai VM.  
Kalau mau hemat dan cepat (misal buat Nginx atau database), LXC jadi pilihan 🌟

---

🎯 Siap lanjut ke langkah berikutnya? Kita akan membahas **manajemen storage** di Proxmox!

🔗 Lanjut ke [#8 - Manajemen Storage di Proxmox.md](./#8%20-%20Manajemen%20Storage%20di%20Proxmox.md)
