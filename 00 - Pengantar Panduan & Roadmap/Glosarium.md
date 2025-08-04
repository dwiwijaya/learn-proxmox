# 📖 Glosarium Istilah Proxmox & Virtualisasi

Halo penjelajah teknologi! 🚀  
Berikut ini adalah daftar istilah penting yang akan sering kamu temui selama belajar Proxmox dan virtualisasi. Jangan khawatir kalau belum hafal semua — kamu bisa balik ke sini kapan aja kayak buka kamus.

---

## A

**API (Application Programming Interface)**  
📡 Jalur komunikasi antara software. Di Proxmox, kamu bisa pakai API untuk mengatur VM secara otomatis dari kode.

---

## B

**Backup**  
💾 Cadangan data VM/Container agar bisa dikembalikan kalau ada kerusakan.

**Bridge Network (vmbr)**  
🌉 Jaringan virtual di Proxmox yang menghubungkan VM dengan dunia luar melalui NIC fisik.

---

## C

**Cluster**  
🔗 Kumpulan beberapa node (server) Proxmox yang digabungkan agar bisa saling dukung dan berbagi resource.

**CLI (Command Line Interface)**  
🖥️ Terminal/console tempat kamu mengetik perintah manual, biasanya via SSH.

**Container (LXC)**  
📦 Lingkungan ringan untuk menjalankan aplikasi, lebih cepat dan hemat resource dibanding VM penuh.

**Corosync**  
🧠 Sistem komunikasi antar node dalam cluster Proxmox. Digunakan untuk memastikan siapa aktif dan siapa mati.

---

## D

**Debian**  
🐧 Distro Linux yang menjadi dasar sistem operasi Proxmox.

**Datacenter**  
🏢 Panel utama di Proxmox WebUI yang menjadi induk dari semua node dan VM.

---

## F

**Failover**  
🛡️ Proses otomatis pindah VM dari node yang mati ke node lain (fitur High Availability).

---

## G

**GUI (Graphical User Interface)**  
🖱️ Antarmuka berbasis klik seperti WebUI Proxmox yang kita buka di browser.

---

## H

**HA (High Availability)**  
💪 Sistem agar VM tetap jalan walau ada node yang mati, melalui proses failover otomatis.

**Hostname**  
🏷️ Nama unik untuk mengidentifikasi server dalam jaringan.

---

## I

**ISO File**  
📀 File image dari OS (seperti Ubuntu, Debian) yang bisa digunakan untuk install VM.

**IP Address**  
🌐 Alamat unik setiap perangkat di jaringan.

---

## K

**Kernel**  
🧬 Inti sistem operasi. Proxmox pakai kernel Linux untuk mengatur hardware dan software.

**KVM (Kernel-based Virtual Machine)**  
🖥️ Teknologi virtualisasi Proxmox untuk membuat VM penuh.

---

## L

**LXC (Linux Containers)**  
📦 Sistem container ringan bawaan Proxmox, berbeda dengan Docker tapi serupa konsepnya.

**LVM (Logical Volume Manager)**  
🗂️ Sistem manajemen disk yang memungkinkan resize dan alokasi dinamis storage.

---

## M

**Migration**  
🚚 Proses memindahkan VM dari satu node ke node lain. Bisa manual atau otomatis (live migration).

---

## N

**NAT (Network Address Translation)**  
🌐 Teknik jaringan untuk “menyembunyikan” banyak VM di balik 1 IP publik.

**NIC (Network Interface Card)**  
🧩 Perangkat jaringan (real maupun virtual) di server.

**Node**  
🧱 Satu server Proxmox dalam cluster. Bisa standalone atau jadi bagian dari cluster.

---

## P

**PVE (Proxmox VE)**  
💻 Singkatan dari Proxmox Virtual Environment — sistem utama yang kita pelajari di panduan ini.

**P2V (Physical to Virtual)**  
🔄 Proses migrasi server fisik menjadi VM di Proxmox.

---

## Q

**QEMU**  
🔧 Emulator mesin virtual yang dipakai Proxmox untuk menjalankan VM.

**Quorum**  
📊 Mekanisme voting dalam cluster untuk menentukan siapa yang berhak ambil keputusan saat ada node yang offline.

---

## R

**Restore**  
🔁 Mengembalikan backup menjadi VM aktif lagi.

**Role**  
🛡️ Akses level user di Proxmox (admin, viewer, dll).

---

## S

**Snapshot**  
📸 Potret kondisi VM/Container saat itu — bisa dikembalikan kalau ada kesalahan.

**SSH (Secure Shell)**  
🔐 Cara aman untuk remote login ke server melalui terminal.

---

## T

**Template**  
📦 Image siap pakai untuk membuat VM atau container dengan cepat.

---

## U

**Uptime**  
⏱️ Waktu sejak server/VM menyala tanpa mati/reboot.

---

## V

**VM (Virtual Machine)**  
🖥️ Komputer virtual penuh dengan OS sendiri yang berjalan di atas server fisik.

**VirtIO**  
🚀 Driver virtualisasi high-performance bawaan Proxmox, untuk disk & network.

---

## Z

**ZFS**  
🗃️ Filesystem modern dengan fitur seperti snapshot, deduplication, dan mirroring. Proxmox bisa install langsung pakai ZFS.

---

## 🧠 Tips!

- Jangan buru-buru menghafal semua.  
- Cukup tahu dulu, nanti makin sering praktik bakal hafal sendiri. 😉

---

Kalau ada istilah yang kamu rasa membingungkan, atau perlu ditambahkan ke sini, langsung tambahkan ya! Atau buka issue/PR kalau kamu forking repo ini.

Semoga kamus kecil ini membantumu! 📘✨
