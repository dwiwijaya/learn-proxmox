# 🌐 #2 - Apa Itu Virtualisasi?

Yuk, sekarang kita masuk ke dunia sihirnya dunia IT: **Virtualisasi!**  
Kalau sebelumnya kamu belajar tentang dunia nyata komputer, sekarang kita mulai bermain dengan **dunia bayangan yang bisa dikendalikan penuh**. 🪄✨

---

## 🤔 Apa Itu Virtualisasi?

Virtualisasi adalah proses menciptakan versi virtual dari sesuatu yang biasanya fisik — seperti server, storage, atau sistem operasi.

Bayangkan kamu punya **1 komputer fisik** (bare metal), tapi di dalamnya bisa berjalan **beberapa komputer digital (VM atau container)** — masing-masing punya sistem operasi dan aplikasinya sendiri!

> 🎩 Ibaratnya seperti rumah kos 3 lantai yang disewakan jadi banyak kamar kecil — satu rumah, banyak penghuni, hemat biaya!

---

## 🧠 Mengapa Virtualisasi Penting?

- 💸 **Efisiensi Biaya**: Nggak perlu beli banyak perangkat keras
- 🚀 **Pemanfaatan Maksimal**: Komputer bisa digunakan penuh tanpa mubazir
- 🔁 **Mudah Diatur**: Bisa cloning, backup, restore dengan cepat
- 🧪 **Lingkungan Uji Coba**: Coba-coba OS, software, tanpa merusak sistem utama
- 🧳 **Portabilitas**: VM bisa dipindah antar server dengan mudah

---

## 🧱 Jenis-Jenis Virtualisasi

| Jenis | Penjelasan | Contoh |
|------|------------|--------|
| **Virtualisasi OS (VM)** | Menjalankan sistem operasi utuh dalam mesin virtual | Windows di dalam Linux |
| **Containerization (CT)** | Menjalankan aplikasi di dalam “wadah ringan” | Docker, LXC |
| **Storage Virtualization** | Menggabungkan beberapa storage jadi satu virtual | RAID, ZFS Pool |
| **Network Virtualization** | Buat jaringan virtual di atas fisik | VLAN, SDN |

---

## 🛠️ Virtual Machine (VM) vs Container (CT)

| Fitur | VM (KVM) | Container (LXC) |
|-------|---------|-----------------|
| Berat | Lebih berat (butuh OS lengkap) | Ringan |
| Isolasi | Lebih terisolasi | Berbagi kernel |
| Kinerja | Sedikit lebih lambat | Lebih cepat |
| Contoh | Windows/Linux Virtual | Web App dalam container |

> ⚖️ Gunakan **VM** untuk sistem full (misal: Windows, Ubuntu Server), dan gunakan **CT** untuk aplikasi ringan seperti web server, database, dll.

---

## 🎮 Analogi Simpel

> Kamu punya **1 konsol game** (komputer fisik), tapi bisa main banyak game berbeda dengan **memory card masing-masing** (VM/CT).  
> Game-nya bisa kamu pause, backup, bahkan dikopi ke konsol lain! 🎮🔁

---

## 🛡️ Hypervisor: Dalang di Balik Layar

Hypervisor adalah software yang memungkinkan virtualisasi terjadi. Ada dua jenis:

- 🧱 **Type 1 (Bare Metal)** — langsung berjalan di atas hardware  
  → Contoh: Proxmox, VMware ESXi
- 🧰 **Type 2 (Hosted)** — berjalan di atas OS  
  → Contoh: VirtualBox, VMware Workstation

**Proxmox VE** adalah **Type 1 Hypervisor** — artinya dia langsung “memerintah” hardware, tanpa lapisan OS pengganggu.

---

## 🧭 Rangkuman

- Virtualisasi = Membuat "komputer dalam komputer"
- VM & CT adalah dua cara umum menjalankan sistem/aplikasi virtual
- Hypervisor adalah alat utama untuk mewujudkan virtualisasi
- Proxmox = Hypervisor hebat, gratis, open source

---

🎯 Siap lanjut ke pengenalan Proxmox itu sendiri?

🔗 Lanjut ke [#3 - Mengenal Proxmox VE.md](./#3%20-%20Mengenal%20Proxmox%20VE.md)
