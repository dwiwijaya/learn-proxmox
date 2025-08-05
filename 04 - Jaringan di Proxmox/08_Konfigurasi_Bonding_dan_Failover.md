# 🪢 08 - Konfigurasi Bonding dan Failover

Pernah kepikiran, "Gimana caranya supaya kalau satu kabel LAN rusak, jaringan tetep jalan?"
Atau "Bisa nggak sih gabungin beberapa NIC jadi satu koneksi super cepat?"
Jawabannya: **Bisa banget! Namanya network bonding.** 😎

---

## 🎯 Tujuan Bab Ini

* Memahami konsep bonding & failover
* Mengetahui mode bonding (LACP, active-backup, dst.)
* Konfigurasi bonding interface di Proxmox

---

## 🧠 Apa Itu Bonding?

**Network bonding** adalah teknik menggabungkan beberapa interface fisik (NIC) menjadi satu interface logis (virtual).
Tujuannya:

* 🔄 **Redundansi (failover):** kalau satu kabel mati, koneksi tetap aman
* ⚡ **Load Balancing:** distribusi trafik ke beberapa NIC untuk performa lebih tinggi

> 🔧 Mirip seperti menjadikan 2 jalur tol menjadi satu jalan besar: bisa lebih cepat **dan** tetap bisa jalan kalau salah satu ditutup 🚗🚗🚧

---

## 🧪 Mode Bonding yang Umum

| Mode               | Fungsi Utama        | Cocok Untuk              |
| ------------------ | ------------------- | ------------------------ |
| **active-backup**  | Failover            | Server produksi (simpel) |
| **balance-rr**     | Load balancing      | Butuh switch support     |
| **802.3ad (LACP)** | Load balancing + HA | Switch managed + LACP    |
| **broadcast**      | Kirim semua jalur   | Testing/eksperimen       |

> 🧠 **Paling umum:** `active-backup` untuk simpel dan aman, atau `802.3ad` untuk performa tinggi (butuh switch managed).

---

## ⚙️ Contoh Konfigurasi Bonding di Proxmox

Misal kamu punya 2 NIC: `eno1` dan `eno2`, dan mau bonding active-backup.

### Edit `/etc/network/interfaces`:

```bash
auto bond0
iface bond0 inet manual
    bond-slaves eno1 eno2
    bond-miimon 100
    bond-mode active-backup

auto vmbr0
iface vmbr0 inet static
    address 192.168.1.10/24
    gateway 192.168.1.1
    bridge_ports bond0
    bridge_stp off
    bridge_fd 0
```

### Restart jaringan:

```bash
ifreload -a
```

---

## 🔍 Cek Status Bonding

Gunakan:

```bash
cat /proc/net/bonding/bond0
```

Output akan menunjukkan:

* Interface aktif
* Mode bonding
* Status link NIC

---

## 🔌 Switch Perlu Disetting?

| Mode          | Butuh Switch Support? |
| ------------- | --------------------- |
| active-backup | ❌ Tidak               |
| 802.3ad       | ✅ Ya, dengan LACP     |

> Kalau pakai switch **managed**, aktifkan LACP di port-port ke Proxmox.

---

## 🧠 Tips Praktis

* **Naming:** Gunakan nama `bond0`, `bond1`, dll.
* **Proxmox GUI:** Bisa juga buat bonding dari GUI → Datacenter → Network → Create → Linux Bond.
* **Test Failover:** Cabut salah satu kabel → pastikan masih bisa ping.

---

## 🎯 Tugas Mandiri

✅ Buat bonding 2 NIC di Proxmox dengan mode `active-backup`
✅ Pasangkan ke bridge `vmbr0`
✅ Coba tes failover: ping dari luar, lalu **cabut salah satu kabel**
✅ Cek status bonding dengan `cat /proc/net/bonding/bond0`

---

📍 Selanjutnya: [`09_Troubleshooting_Jaringan_VM.md`](09_Troubleshooting_Jaringan_VM.md)
Kita akan belajar cara menjadi detektif jaringan! 🔍💻 Siap melacak masalah koneksi VM dengan alat-alat ampuh!

