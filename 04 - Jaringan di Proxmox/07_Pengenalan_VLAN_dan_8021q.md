# 🧷 07 - Pengenalan VLAN dan 802.1Q

Bayangkan kamu punya satu kabel jaringan, tapi bisa membawakan **beberapa jalur (network)** yang berbeda secara virtual.
Yup, itulah si **VLAN (Virtual LAN)** — seperti membuat banyak "ruangan" dalam satu gedung kantor hanya dengan satu jalur listrik! ⚡🏢

---

## 🎯 Tujuan Bab Ini

* Memahami konsep dasar VLAN
* Mengenal standar **802.1Q** yang dipakai di Proxmox
* Belajar membuat interface VLAN untuk VM/Container

---

## 🧠 Apa Itu VLAN?

**VLAN** memungkinkan kamu membagi satu jaringan fisik menjadi beberapa jaringan virtual (logical).

Misalnya:

| VLAN ID | Nama VLAN      | Fungsi             |
| ------- | -------------- | ------------------ |
| 10      | Staff LAN      | Untuk karyawan     |
| 20      | Guest LAN      | Untuk tamu         |
| 30      | Management LAN | Akses admin/server |

---

## 📦 Keuntungan VLAN

| Keuntungan          | Penjelasan                            |
| ------------------- | ------------------------------------- |
| 🔐 Keamanan         | Tiap VLAN bisa dipisahkan trafiknya   |
| 📊 Skalabilitas     | Mudah atur banyak jaringan di 1 kabel |
| 🛠️ Manajemen Mudah | Routing antar VLAN lebih terkontrol   |
| 💰 Efisiensi Biaya  | Tidak perlu banyak switch/port fisik  |

---

## 🎯 VLAN & Proxmox: Siapa ngapain?

| Komponen        | Peran                                    |
| --------------- | ---------------------------------------- |
| 🖥 Proxmox Host | Mengatur interface VLAN (802.1q tagging) |
| 📦 VM/CT        | Bisa dikasih VLAN ID tertentu            |
| 🌉 Bridge       | Bisa dilewatkan VLAN-tagged traffic      |
| 🔌 Switch       | Harus support VLAN (802.1Q/trunk mode)   |

---

## 🧪 Konsep 802.1Q

802.1Q adalah standar untuk menambahkan **tag VLAN** ke setiap frame ethernet.
Frame akan membawa info `VLAN ID`, jadi switch/router tahu itu milik jaringan mana.

```
[Frame Ethernet]
 ├── Header Ethernet
 ├── 802.1Q Tag (VLAN ID)
 └── Payload Data
```

---

## 🔧 Contoh Konfigurasi VLAN di Proxmox

Misal kamu punya NIC `eno1` dan ingin:

* VLAN 10 untuk **VM staff**
* VLAN 20 untuk **VM tamu**

### Konfigurasi `/etc/network/interfaces`:

```bash
auto eno1
iface eno1 inet manual

auto vmbr0
iface vmbr0 inet manual
    bridge_ports eno1
    bridge_stp off
    bridge_fd 0
```

---

### Saat buat VM → Tambahkan VLAN ID di GUI

```
Network Device → VLAN Tag: 10
```

Atau via CLI:

```bash
qm set 101 -net0 virtio=XX:XX:XX:XX:XX:XX,bridge=vmbr0,tag=10
```

---

## 💡 Tips VLAN di Switch

Jika kamu pakai switch fisik:

* Aktifkan **Trunk mode** di port ke Proxmox
* Tambahkan **allowed VLAN** sesuai kebutuhan
* VLAN default biasanya 1 (pastikan tidak konflik)

---

## 📋 Periksa VLAN Tag dari Proxmox

```bash
bridge vlan show
```

Contoh hasil:

```
port    vlan ids
vmbr0   10 PVID Egress Untagged
        20
```

---

## 🚨 Catatan Penting

| Hal                                                     | Penjelasan |
| ------------------------------------------------------- | ---------- |
| 🧱 VM tetap pakai IP sesuai subnet VLAN-nya             |            |
| 🔌 Switch harus support 802.1Q                          |            |
| 🔀 VLAN tidak otomatis bisa saling ping (perlu routing) |            |

---

## 🎯 Tugas Mandiri

✅ Coba buat 2 VLAN (misal 10 dan 20)
✅ Assign ke 2 VM berbeda
✅ Pasang IP dari subnet berbeda (misal `192.168.10.0/24` dan `192.168.20.0/24`)
✅ Tes apakah bisa saling ping (harusnya **tidak bisa** tanpa routing)
✅ Cek hasil `bridge vlan show`

---

📍 Selanjutnya: [`08_Konfigurasi_Bonding_dan_Failover.md`](08_Konfigurasi_Bonding_dan_Failover.md)
Kita akan menyatukan banyak NIC jadi satu “super NIC” demi performa dan keandalan! 💪🌐

