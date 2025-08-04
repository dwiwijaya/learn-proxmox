# 🧰 01 - Mempersiapkan Hardware dan Virtualisasi

Sebelum kita install Proxmox, kita harus pastikan bahwa "panggungnya" sudah siap!  
Entah kamu mau install di **server fisik** atau hanya mencoba di **virtualisasi nested** (di dalam VM), semuanya harus siap dulu.

---

## 🎯 Tujuan Bab Ini

- Menentukan di mana Proxmox akan di-install
- Memastikan perangkat mendukung virtualisasi
- Memahami mode testing: bare-metal vs nested

---

## 💻 Opsi Lingkungan Instalasi

| Lingkungan   | Cocok Untuk        | Kelebihan                           | Kekurangan                           |
|--------------|--------------------|-------------------------------------|--------------------------------------|
| 💿 **Bare Metal** | Produksi / Lab serius | Performa maksimal, real network     | Perlu hardware fisik, risiko lebih tinggi |
| 💻 **Nested Virtualization** | Testing / Belajar  | Aman, fleksibel, cepat disetup      | Performa lebih lambat, kompleksitas ekstra |

> 🧠 **Nested** = install Proxmox di dalam VM (misal pakai VirtualBox, VMware, QEMU, dll)

---

## ✅ Cek Dukungan Virtualisasi

Proxmox butuh dukungan CPU untuk virtualisasi hardware:

### Di Linux:
```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
````

> Jika hasilnya > 0, artinya CPU kamu mendukung KVM (virtualisasi hardware) ✅

### Di BIOS/UEFI:

Aktifkan fitur berikut:

* **Intel VT-x** atau **AMD-V**
* **VT-d** (untuk IOMMU / PCI passthrough)
* Nonaktifkan **Secure Boot** (kadang ganggu instalasi Linux)

---

## 📋 Spesifikasi Minimum Proxmox (saran)

| Komponen | Minimum    | Disarankan           |
| -------- | ---------- | -------------------- |
| CPU      | Dual-core  | Quad-core atau lebih |
| RAM      | 2 GB       | 8 GB atau lebih      |
| Disk     | 32 GB SSD  | 128 GB SSD/NVMe      |
| NIC      | 1 Gbps LAN | 1 Gbps LAN           |

> Kalau kamu mau testing ringan, bahkan laptop dengan 8 GB RAM sudah cukup untuk coba nested Proxmox dengan 1-2 VM kecil.

---

## 🧪 Tips Setup Nested (contoh VirtualBox)

1. Buat VM baru dengan tipe **Debian (64-bit)**
2. Alokasikan RAM minimal **4 GB**, dan disk minimal **32 GB**
3. Aktifkan:

   * `Enable VT-x/AMD-V`
   * `Enable Nested Paging`
   * Network Adapter: **Bridged Adapter** (untuk testing jaringan real)
4. Attach ISO Proxmox saat boot
5. Jalankan installer 🚀

---

## 🧠 Perbedaan Testing vs Produksi

| Kriteria   | Testing (Nested)            | Produksi (Bare Metal)     |
| ---------- | --------------------------- | ------------------------- |
| Tujuan     | Belajar & eksperimen        | Dipakai nyata (server)    |
| Stabilitas | Cukup baik                  | Harus sangat stabil       |
| Resiko     | Aman kalau error            | Error bisa ganggu sistem  |
| Performa   | Cukup untuk simulasi ringan | Optimal untuk beban kerja |

---

## 📦 Simulasi Topologi Mini (Optional)

Ingin coba lab kecil?
Kamu bisa siapkan:

* 🖥 VM Proxmox (host)
* 💻 Beberapa VM di dalamnya (VM Debian, Ubuntu, dll)
* 🌐 Mode jaringan: Bridged agar bisa saling ping

---

## 🎯 Tugas Mandiri

✅ Tentukan apakah kamu mau pakai bare-metal atau nested
✅ Cek apakah CPU kamu support virtualisasi
✅ Siapkan ISO Proxmox (nanti dijelaskan di bab 2)

---

📍 Selanjutnya: [`02_Instalasi_Proxmox_dari_ISO.md`](02_Instalasi_Proxmox_dari_ISO.md)
Kita akan masuk ke proses instalasi Proxmox VE sesungguhnya! ⚙️🔥


