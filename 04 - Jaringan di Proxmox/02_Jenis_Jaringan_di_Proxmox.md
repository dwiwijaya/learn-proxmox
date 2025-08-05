# 🧭 02 - Jenis-Jenis Jaringan di Proxmox

Sudah siap menjelajah lebih dalam? 🔍  
Sekarang kita akan bahas berbagai **mode jaringan** yang tersedia di Proxmox. Setiap mode punya karakteristik, kelebihan, dan waktu penggunaan yang tepat. Kalau salah pilih, bisa-bisa VM kamu nyasar nggak bisa internetan 😅

---

## 🎯 Tujuan Bab Ini

- Mengenali berbagai **jenis jaringan** yang tersedia di Proxmox
- Memahami **kapan** dan **kenapa** harus memilih mode tertentu
- Menjadi bekal untuk setup VM, container, dan cluster ke depannya

---

## 📦 Mode Jaringan yang Tersedia di Proxmox

| Mode | Nama Umum | Internet | Host Access | Inter-VM | Cocok Untuk |
|------|-----------|----------|-------------|----------|--------------|
| `Bridged` | Jembatan ke LAN | ✅ | ✅ | ✅ | Produksi & lab serius |
| `NAT` | Terjemahan IP | ✅ | ❌ | ✅ | VM test dengan internet |
| `Host-only` | VM ↔ Host | ❌ | ✅ | ✅ | Lab offline |
| `Isolated` | Internal-only | ❌ | ❌ | ✅ | Simulasi topologi terpisah |
| `Routed` | Routing manual | ✅ | ⚠️ Advanced | ✅ | Advanced topologi LAN |
| `VLAN` | Jaringan virtual terpisah | ✅ | ✅ | ✅ | Segmentasi jaringan besar |

---

## 🌉 1. Bridged (Jaringan Fisik)

Mode **bridged** adalah default di Proxmox (`vmbr0`).  
VM akan terlihat seolah-olah seperti **komputer fisik di jaringan yang sama** dengan host.

### ✅ Kelebihan:
- VM dapat IP dari DHCP LAN (seperti komputer biasa)
- Bisa diakses dari perangkat lain di jaringan
- Ideal untuk Proxmox di jaringan produksi

### 🛠️ Contoh:  
- VM kamu punya IP `192.168.1.50` seperti laptop lain di rumah
- Bisa SSH ke VM dari komputer mana saja di jaringan lokal

---

## 🌐 2. NAT (Network Address Translation)

Mode ini **menyembunyikan IP VM** di balik IP host, mirip seperti cara WiFi rumah bekerja.

### ✅ Kelebihan:
- Tidak butuh IP publik atau DHCP server
- VM tetap bisa akses internet

### ⚠️ Kekurangan:
- VM tidak bisa diakses dari luar langsung
- Butuh port forwarding kalau mau akses VM dari luar

### 📌 Cocok untuk:
- Testing ringan
- VM yang hanya butuh internet, tidak perlu diakses

---

## 🖥️ 3. Host-only

Mode ini menghubungkan VM hanya ke **host Proxmox**, tapi **tidak ke internet**.

### ✅ Cocok untuk:
- Transfer file antar VM ↔ host
- Private network untuk monitoring

---

## 🔒 4. Isolated Network

Mode ini menciptakan jaringan **yang hanya digunakan antar VM**, tanpa koneksi ke host atau internet.

### 🔧 Cocok untuk:
- Simulasi LAN internal
- Belajar konsep firewall, router, DNS lokal

---

## 🚦 5. Routed Network

Mode ini lebih **advanced**, VM akan punya IP sendiri dan **routing diatur manual**.

### Cocok untuk:
- Cluster dengan IP segment berbeda
- Bikin lab dengan router virtual

### ⚠️ Hanya disarankan jika kamu sudah paham routing & subnet

---

## 🏷️ 6. VLAN (802.1q)

VLAN memungkinkan kamu membuat banyak jaringan **dalam satu kabel/NIC fisik**.  
Ideal untuk:

- Lab kompleks
- Isolasi trafik antar VM
- Cluster dengan segmentasi jaringan

> Akan dibahas lebih rinci di bab `07_Pengenalan_VLAN_dan_8021q.md`

---

## 🔑 Tips Memilih Mode Jaringan

| Tujuan Kamu | Gunakan Mode |
|-------------|--------------|
| VM harus bisa diakses dari luar | Bridged |
| VM hanya perlu internet (testing) | NAT |
| Belajar jaringan LAN internal | Isolated / Host-only |
| Setup Proxmox Cluster | Bridged + VLAN/Routed |
| Simulasi banyak subnet | VLAN / Routed |

---

## 💡 Analogi Singkat

- **Bridged** = VM seperti tetangga satu komplek, semua bisa saling panggil
- **NAT** = VM seperti anak kosan, bisa telpon keluar tapi nggak bisa ditelpon langsung
- **Host-only** = VM seperti ngobrol di dalam kamar bareng host
- **Isolated** = VM seperti bikin ruangan khusus, tidak ada pintu keluar
- **Routed/VLAN** = Seperti bikin perumahan dengan banyak blok yang bisa diatur aksesnya

---

## 🎯 Tugas Mandiri

✅ Coba buat beberapa VM dengan mode jaringan berbeda  
✅ Bandingkan hasilnya: apakah bisa ping host? internet? antar VM?  
✅ Catat hasilnya sebagai mini-lab 💻

---

📍 Selanjutnya: [`03_Konfigurasi_Bridge_dan_Interface.md`](03_Konfigurasi_Bridge_dan_Interface.md)  
Kita akan mulai praktik: membuat dan mengedit konfigurasi `vmbr` di Proxmox! ⚙️🛜
