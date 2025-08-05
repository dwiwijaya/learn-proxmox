# 🧩 06 - Multi NIC dan Manajemen Interface

Bayangkan kamu punya **lebih dari satu jalur internet atau LAN**, seperti punya dua kaki — satu ke internet, satu ke jaringan internal. Nah, begitulah konsep **Multi NIC (Network Interface Card)** dalam dunia Proxmox! 🦶🦶🌐

---

## 🎯 Tujuan Bab Ini

* Memahami cara kerja multi-NIC di Proxmox
* Menjelaskan perbedaan **NIC fisik vs virtual**
* Belajar mengelola interface agar rapi, stabil, dan terstruktur

---

## 🧠 Apa Itu NIC?

NIC (Network Interface Card) adalah perangkat keras (atau virtual) yang memungkinkan server berkomunikasi dengan jaringan.

Ada dua jenis di Proxmox:

* **NIC Fisik**: Perangkat asli di server (`eno1`, `enp3s0`, dll)
* **NIC Virtual**: Dibuat untuk VM/Container (misal `eth0` di dalam VM)

> 🧠 Satu NIC bisa dibuat jadi beberapa **bridge** atau **bonding interface** tergantung kebutuhan.

---

## 🧱 Kenapa Butuh Multi NIC?

| Skenario                      | Fungsi                                                   |
| ----------------------------- | -------------------------------------------------------- |
| 🧪 Lab terisolasi             | Pisahkan jaringan lab dari internet                      |
| 🌐 Dual WAN                   | Load balancing atau failover antara dua koneksi internet |
| 🔒 Jaringan internal & publik | Pisahkan akses internal dan akses pengguna luar          |
| 📦 Storage terpisah           | Jalur cepat khusus untuk storage (iSCSI, NFS)            |

---

## 🗺️ Contoh Topologi Multi NIC

```
[Proxmox Host]
 ├── eno1 → vmbr0 → Internet (192.168.1.0/24)
 └── eno2 → vmbr1 → Jaringan Internal (10.10.10.0/24)
```

---

## 🛠️ Contoh Konfigurasi di `/etc/network/interfaces`

```bash
# NIC 1 → Internet
auto eno1
iface eno1 inet manual

auto vmbr0
iface vmbr0 inet dhcp
    bridge_ports eno1
    bridge_stp off
    bridge_fd 0

# NIC 2 → Internal Network
auto eno2
iface eno2 inet manual

auto vmbr1
iface vmbr1 inet static
    address 10.10.10.1/24
    bridge_ports eno2
    bridge_stp off
    bridge_fd 0
```

---

## 🔁 NIC Management Tips

| Hal yang Perlu Diperhatikan      | Penjelasan                                                                 |
| -------------------------------- | -------------------------------------------------------------------------- |
| 🌉 Bridge Naming                 | Gunakan nama yang konsisten (`vmbr0`, `vmbr1`, dll)                        |
| 🔀 Jangan saling rebutan gateway | Hanya 1 bridge boleh punya **gateway default**                             |
| 🔍 Cek via CLI                   | Gunakan `ip a` atau `bridge link` untuk melihat status interface           |
| 🔒 Firewall per NIC              | Kamu bisa aktifkan firewall hanya di satu bridge tertentu untuk isolasi VM |

---

## 🔄 Gunakan Multi NIC untuk:

* Pisahkan **VM produksi** dan **VM testing**
* Buat lab jaringan: simulasi WAN, LAN, DMZ
* Isolasi trafik storage (cepat dan aman)
* Konfigurasi VLAN atau Bonding (dibahas selanjutnya!)

---

## 📋 Cek Status Jaringan

```bash
ip a
ip r
brctl show
```

> 🔎 Cek IP masing-masing bridge dan pastikan hanya satu yang menjadi gateway default.

---

## 🎯 Tugas Mandiri

✅ Tambahkan 1 NIC lagi ke server Proxmox kamu (kalau virtual, tambahkan via setting)   
✅ Buat `vmbr1` untuk jaringan internal   
✅ Coba koneksi antara 2 VM melalui `vmbr1` tanpa akses internet   
✅ Cek hasil dengan `ip a`, `ping`, dan `ip r`   

---

📍 Selanjutnya: [`07_Pengenalan_VLAN_dan_8021q.md`](07_Pengenalan_VLAN_dan_8021q.md)
Kita akan masuk ke dunia VLAN! Belajar bagaimana mengatur jaringan yang lebih tertata, efisien, dan scalable! 🎯🔧


