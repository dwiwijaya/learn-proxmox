# 🧠 03 - Tipe Hypervisor

Selamat datang di level berikutnya! 🧗‍♂️  
Setelah tahu apa itu virtualisasi, sekarang kita kenalan dengan teknologi yang membuat semuanya mungkin: **Hypervisor**!

---

## 💡 Apa Itu Hypervisor?

> Hypervisor adalah perangkat lunak (software) yang memungkinkan satu komputer fisik (host) menjalankan beberapa mesin virtual (guest) secara bersamaan.

Hypervisor inilah yang mengatur pembagian sumber daya seperti CPU, RAM, storage, dan jaringan antara mesin fisik dan VM.

---

## 🧠 Analogi

Bayangkan kamu adalah seorang manajer restoran 🍽️

- Kamu punya satu dapur besar (server fisik)
- Hypervisor adalah kepala koki 👨‍🍳 yang mengatur siapa dapat kompor, bahan, panci, dll
- Masing-masing juru masak (VM) dapat bagian dapurnya, tapi semua diatur oleh si kepala koki

---

## 🧱 Jenis-Jenis Hypervisor

### 🥇 Type 1 - **Bare Metal Hypervisor**
- Diinstal langsung di atas hardware (tanpa OS)
- Stabil, cepat, cocok untuk server produksi
- Contoh: Proxmox VE, VMware ESXi, Microsoft Hyper-V, XenServer

> ✅ Kelebihan:
> - Performa tinggi
> - Lebih aman (karena OS umum tidak terlibat)
> - Cocok untuk data center & cluster besar

> ❌ Kekurangan:
> - Biasanya butuh hardware server yang mumpuni
> - Tidak semua user familiar CLI (kalau tidak ada GUI)

---

### 🥈 Type 2 - **Hosted Hypervisor**
- Diinstal di atas OS biasa (misalnya di Windows/macOS/Linux)
- Cocok untuk testing atau belajar
- Contoh: VirtualBox, VMware Workstation, Parallels

> ✅ Kelebihan:
> - Mudah dipakai (cukup install seperti aplikasi biasa)
> - Cocok untuk development & belajar

> ❌ Kekurangan:
> - Performa lebih lambat karena dibungkus OS
> - Tidak cocok untuk kebutuhan skala besar atau production

---

## 🧩 Perbandingan Singkat

| Fitur | Type 1 (Bare Metal) | Type 2 (Hosted) |
|-------|---------------------|-----------------|
| Lokasi Instalasi | Langsung di hardware | Di atas OS |
| Performa | Tinggi | Lebih rendah |
| Stabilitas | Sangat stabil | Kurang stabil |
| Cocok untuk | Server & data center | Belajar & testing |
| Contoh | Proxmox, ESXi | VirtualBox, VMware Workstation |

---

## 🧠 Di Mana Proxmox Masuk?

💥 Proxmox VE adalah **Type 1 Hypervisor**, karena:

- Diinstal langsung ke hardware
- Berbasis Linux (Debian)
- Bisa diakses lewat GUI & CLI
- Cocok untuk clustering, backup, container, dsb.

Proxmox adalah pilihan populer karena **gratis, open-source, powerful**, dan fiturnya komplit banget untuk kelas enterprise. 🔥

---

## 🧠 Pertanyaan Reflektif

- Kenapa Type 1 lebih cocok untuk production dibanding Type 2?
- Apa kelebihan Proxmox dibanding VirtualBox?
- Bisa nggak install Proxmox di laptop biasa?

---

📍 Selanjutnya kita akan bahas perbedaan penting:
👉 [`04_VM_vs_Container.md`](04_VM_vs_Container.md)

Kita akan ulik: kapan lebih baik pakai VM, kapan pakai Container! 🚀
