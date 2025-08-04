# 🛠️ 09 - Buat VM dan Container Pertamamu

Akhirnya kita sampai di tahap yang paling *praktikal*! 🎉  
Kita akan membuat dua hal penting:

1. Virtual Machine (VM) berbasis ISO
2. Container (LXC) berbasis template
---

## 🧠 Sekilas Perbedaan: VM vs LXC

| Aspek         | VM (Virtual Machine)                     | LXC (Container)                          |
|---------------|-------------------------------------------|-------------------------------------------|
| Kernel        | Punya kernel sendiri (lebih berat)       | Pakai kernel host (lebih ringan)         |
| Performa      | Lebih lambat, tapi fleksibel             | Cepat & efisien, tapi terbatas           |
| OS            | Bisa Windows/Linux                       | Umumnya Linux saja                       |
| Use-case      | Full OS, software kompleks               | Web app, API server, automation ringan   |

---

## 🎯 Tujuan Bab Ini

- Membuat VM dari ISO
- Pahami opsi penting seperti disk format, BIOS/UEFI, dan network bridge
- Install OS seperti Ubuntu / Debian
- Jalankan dan akses VM

---

## 🧱 Apa Itu VM? (dan Kenapa Penting)

VM (Virtual Machine) itu semacam “komputer palsu” yang dibuat dalam server Proxmox.  
Dia punya CPU, RAM, disk, dan jaringan sendiri — tapi semuanya virtual.

> 💡 **Analogi**: Seperti ngejalanin beberapa laptop di dalam 1 laptop besar.

---

## 📋 Syarat Sebelum Membuat VM

- Sudah upload ISO OS (Ubuntu, Debian, dll) ke storage
- Sudah paham storage `local` vs `local-lvm`
- Jaringan sudah oke (default: `vmbr0` = jembatan ke LAN)

---

## 🧙‍♂️ Langkah Buat VM + Penjelasannya

Saat klik **Create VM**, kamu akan diminta mengisi 8 langkah.  
Yuk kita bahas satu per satu plus penjelasan (📚).

---

### ✨ Step 1: General
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Name.png)
| Opsi        | Penjelasan Singkat                                |
|-------------|----------------------------------------------------|
| **Node**    | Nama server fisik (misal: `pve1`)                  |
| **VM ID**   | ID unik VM, auto boleh                             |
| **Name**    | Nama VM kamu, misalnya `vm-ubuntu-server`          |

---

### 💿 Step 2: OS
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Choose-Fedora-ISO-File.png)
| Opsi         | Penjelasan                                                   |
|--------------|---------------------------------------------------------------|
| **ISO Image**| File ISO OS yang mau kamu install (misalnya `ubuntu-24.iso`) |
| **Guest OS** | Pilih tipe OS, misalnya: Linux → Ubuntu                      |

---

### 💻 Step 3: System
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Keep-Default-System-Settings.png)
| Opsi        | Penjelasan                                                                 |
|-------------|-----------------------------------------------------------------------------|
| **BIOS**    | `SeaBIOS` = BIOS lama (legacy)                                              |
|             |  `OVMF (UEFI)` = BIOS modern, wajib kalau OS pakai UEFI                     |
| **Machine** | Tipe virtualisasi, default saja (`i440fx`/`q35`)                            |
| **Graphic** | VGA default OK (kalau pakai GUI OS)                                        |
| **SCSI Controller** | Pengontrol disk virtual, pilih `VirtIO SCSI` kalau OS support      |

> 💡 **Analogi BIOS/UEFI**:
> - BIOS = "rumah jadul", cocok buat OS lama
> - UEFI = "rumah modern", support fitur baru seperti boot lebih cepat

---

### 💾 Step 4: Hard Disk
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Disk-Size.png)
| Opsi        | Penjelasan                                                                 |
|-------------|-----------------------------------------------------------------------------|
| **Storage** | Pilih `local` (file biasa) atau `local-lvm` (lebih cepat, pakai LVM block) |
| **Format**  | `raw`: performa bagus, sederhana<br>`qcow2`: support snapshot, fleksibel   |
| **Size**    | Minimal 8 GB (tergantung kebutuhan OS)                                     |

> 📦 **Perbedaan `local` vs `local-lvm`:**
> - `local`: simpan file VM sebagai `.qcow2` atau `.raw` di `/var/lib/vz`  
> - `local-lvm`: simpan VM sebagai *volume block*, performa tinggi tapi tidak bisa diakses langsung dari file manager

---

### 🧠 Step 5 & 6: CPU & Memory
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-CPU-Settings.png)
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Memory-Settings.png)
| Opsi        | Penjelasan                        |
|-------------|------------------------------------|
| **Sockets** |Jumlah prosesor fisik               |
| **Cores**   | Jumlah core CPU virtual            |
| **Memory**  | RAM virtual, sesuaikan kebutuhan   |

Misalnya: 1 sockets + 2 core + 2048 MB RAM cukup buat Ubuntu Server

---

### 🌐 Step 7: Network
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Set-VM-Network-Settings.png)
| Opsi        | Penjelasan                                                               |
|-------------|---------------------------------------------------------------------------|
| **Bridge**  | Gunakan `vmbr0` (jembatan ke LAN, biar VM bisa dapet IP dari router)     |
| **Model**   | `virtio` = cepat & efisien, `Intel E1000` = lebih kompatibel (untuk OS lama) |

> 🌉 **Analogi**:
> - `vmbr0` = seperti “colokan LAN” virtual buat VM kamu  
> - Kalau VM nyolok ke vmbr0, dia bisa dapet IP dari jaringan rumah/kantor langsung

---

### ✅ Step 8: Confirm
![alttext](https://www.tecmint.com/wp-content/uploads/2023/12/Confirm-VM-Settings.png)
Klik **Finish** → Proxmox akan membuat VM

---

## 🚀 Jalankan dan Install OS

1. Klik VM → **Start**
2. Klik **Console** → akan muncul layar instalasi dari ISO
3. Ikuti proses instalasi seperti install OS di PC biasa

---

## 🧠 Tips Akses & Network

- Setelah install OS, login ke dalam VM
- Cek IP-nya pakai:
  ```bash
  ip a
  ````

* VM harusnya dapat IP dari router via DHCP

Kalau belum dapat IP:

* Pastikan `vmbr0` tersambung ke port LAN
* Atur IP manual di dalam OS (statis)

---

## 🎯 Tugas Mandiri

✅ Buat 1 VM baru   
✅ Pilih ISO dan setting disk/BIOS dengan paham   
✅ Install OS di dalam VM   
✅ Cek koneksi internet di VM   

---

📍 Lanjut ke: [`06_Konsep_Storage_Dasar.md`](06_Konsep_Storage_Dasar.md)   
Di bab selanjutnya, kita akan bongkar tuntas dunia storage: disk, partisi, RAID, ZFS, dan lainnya! 💾🔍

