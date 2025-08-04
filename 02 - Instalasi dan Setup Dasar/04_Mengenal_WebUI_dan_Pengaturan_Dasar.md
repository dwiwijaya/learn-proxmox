# 🎛️ 04 - Mengenal WebUI dan Pengaturan Dasar

Setelah berhasil install dan update, sekarang kita jalan-jalan dulu ke dalam WebUI Proxmox.  
Kita akan pelajari bagian-bagian penting, apa fungsinya, dan konfigurasi dasar yang perlu kamu tahu.

---

## 🎯 Tujuan Bab Ini

- Mengenal tampilan dan struktur WebUI Proxmox
- Menjelaskan fungsi utama: node, VM, storage, dsb
- Menyesuaikan beberapa pengaturan dasar

---

## 🔍 Struktur Antarmuka WebUI

Saat login ke WebUI (`https://<ip>:8006`), kamu akan lihat 2 panel utama:

### Kiri - **Tree View**
Hierarki sistem kamu:
```

Datacenter
└── node1 (hostname)
├── Summary
├── Shell
├── VM
├── LXC
├── Storage
├── Network
└── System

````

### Kanan - **Detail View**
Konten dari menu yang kamu klik. Misal klik “Storage” → tampil info disk, ISO, backup, dsb.

---

## 🧱 Komponen Penting WebUI

| Komponen       | Fungsi                                                         |
|----------------|----------------------------------------------------------------|
| **Datacenter** | Pengaturan global (user, permission, cluster, dsb)            |
| **Node**       | Server fisik tempat VM berjalan                                |
| **Shell**      | Akses terminal langsung ke node (seperti SSH langsung)        |
| **VM**         | Virtual Machines (KVM-based), untuk OS seperti Linux/Windows  |
| **LXC**        | Lightweight container, cocok untuk service ringan              |
| **Storage**    | Disk lokal, NFS, ZFS, dll                                      |
| **Network**    | Konfigurasi bridge, IP, VLAN, dsb                              |
| **System**     | Info sistem: waktu, log, service, dsb                          |

---

## ⚙️ Pengaturan Dasar yang Perlu Dicek

### 1. **Hostname & FQDN**

Pastikan hostname sudah benar dan punya format FQDN (Fully Qualified Domain Name), misalnya:

```bash
pve1.localdomain
````

Cek/edit di:

* WebUI → Node → System → Network
* Atau CLI: `/etc/hosts` dan `/etc/hostname`

---

### 2. **Upload ISO**

Untuk bisa install VM (seperti Debian, Ubuntu, dsb), kita perlu upload file `.iso` ke storage:

1. Klik `Node` → `Storage` (contoh: `local`)
2. Pilih tab `Content`
3. Klik `Upload` → pilih `ISO Image` → unggah ISO kamu

---

### 3. **Cek Storage & Network**

* **Storage** → Pastikan kamu punya cukup ruang & tahu letak ISO/vm-disk disimpan
* **Network** → Lihat bridge seperti `vmbr0`, pastikan IP & gateway sesuai

---

## 🧪 Eksplorasi Mandiri

🧭 Coba klik-klik beberapa fitur:

* Lihat summary node
* Lihat log sistem
* Klik tab Network → cek IP dan bridge
* Upload 1 ISO ke storage

---

## 💡 Tips Navigasi

* Gunakan fitur “Search” di kanan atas kalau bingung cari fitur
* Klik kanan pada node atau VM untuk shortcut menu
* Bookmark WebUI kamu di browser (biar nggak lupa 😄)

---

## 🎯 Tugas Mandiri

✅ Pahami struktur WebUI   
✅ Upload 1 ISO image ke storage   
✅ Cek konfigurasi network & storage   
✅ Pastikan hostname dan timezone sesuai   

---

📍 Lanjut ke: [`05_Membuat_VM_Pertamamu.md`](05_Membuat_VM_Pertamamu.md)   
Yuk bikin VM pertamamu di Proxmox, beneran seru nih! 🛠️🧑‍💻

