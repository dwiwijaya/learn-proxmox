# 🌍 05 - Koneksi Internet untuk VM

Setelah VM atau Container kamu berhasil dibuat, saatnya bikin mereka **terhubung ke internet!**
Gampang? Bisa iya. Tapi kalau belum ngerti cara kerjanya, bisa bikin kamu garuk-garuk kepala 😅

---

## 🎯 Tujuan Bab Ini

* Memahami bagaimana Proxmox menghubungkan VM ke internet
* Menjelaskan peran **Bridge**, **NAT**, dan **gateway**
* Memberikan panduan koneksi internet via **bridged** dan **NAT**

---

## 🧠 Teori Dasar: Jalan Menuju Internet

Agar VM bisa terhubung ke internet, perlu 3 syarat utama:

| Syarat       | Penjelasan                                                  |
| ------------ | ----------------------------------------------------------- |
| IP Address   | VM harus punya IP, baik dari DHCP atau static               |
| Gateway      | Arah ke luar jaringan lokal (biasanya IP router atau modem) |
| Akses ke DNS | Supaya bisa mengakses domain (misal: google.com → 8.8.8.8)  |

Dan supaya lalu lintas dari VM bisa keluar, dibutuhkan interface virtual (bridge) yang terhubung ke jaringan luar.

---

## 🛣️ Dua Jalur Menuju Internet

Proxmox punya dua pendekatan utama:

### 1. 🌉 **Bridged Networking (Direct Access)**

VM langsung berada di jaringan yang sama dengan host Proxmox dan perangkat lain.
Ibaratnya, VM kamu **nyambung langsung ke switch/modem** seperti PC biasa.

#### ⚙️ Cara Kerja:

* VM pakai **bridge** (misalnya `vmbr0`) yang sudah terhubung ke NIC fisik
* Dapat IP dari DHCP server jaringan utama (misal router)
* Gateway dan DNS disediakan otomatis

#### ✅ Kelebihan:

* VM bisa langsung komunikasi ke perangkat jaringan lain
* Cocok untuk server produksi

#### ⚠️ Kekurangan:

* Butuh setup bridge yang benar
* Kadang IP terbatas dari DHCP modem/router

---

### 2. 🔁 **NAT (Network Address Translation)**

VM masuk ke jaringan lokal buatan, lalu lalu lintasnya diteruskan keluar oleh host Proxmox (seperti router mini).

#### ⚙️ Cara Kerja:

* VM terhubung ke bridge **tanpa NIC fisik** (isolated bridge)
* Proxmox jadi router: memberikan IP ke VM + meneruskan internet via `iptables` dan `masquerade`
* Perlu setup NAT manual

#### ✅ Kelebihan:

* Aman untuk lab/testing
* Nggak ganggu jaringan utama

#### ⚠️ Kekurangan:

* Tidak bisa langsung diakses dari luar (kecuali port forwarding)
* Lebih rumit setup-nya

---

## 🛠️ Contoh Setup 1: Bridged Networking (Paling Umum)

1. Pastikan kamu punya bridge seperti `vmbr0` yang terhubung ke NIC (misal `eno1`)
2. Saat bikin VM, pada tab **Network**:

   * **Bridge**: pilih `vmbr0`
   * **Model**: VirtIO (cepat dan optimal)
3. Jalankan VM dan pastikan dapat IP dari DHCP (otomatis)
4. Coba ping:

   ```bash
   ping 8.8.8.8
   ping google.com
   ```

> 🧠 Biasanya modem rumah atau DHCP server akan otomatis memberikan IP, gateway, dan DNS

---

## 🧪 Contoh Setup 2: NAT (Jaringan Isolasi + Internet)

1. Buat bridge baru (misal `vmbr1`) **tanpa NIC fisik**
2. Beri IP statis:

   ```bash
   auto vmbr1
   iface vmbr1 inet static
       address 192.168.100.1/24
       bridge_ports none
       bridge_stp off
       bridge_fd 0
   ```
3. Setup DHCP + NAT di host Proxmox (bisa pakai dnsmasq/iptables)
4. VM dapat IP dari `192.168.100.0/24` lalu internet via NAT

> 📦 Ini cocok untuk lab isolated + tetap bisa akses internet

---

## 🧩 Tips Troubleshooting

| Gejala                         | Kemungkinan Masalah           |
| ------------------------------ | ----------------------------- |
| Tidak dapat IP                 | Cek DHCP server, bridge salah |
| Bisa ping IP tapi tidak domain | DNS belum dikonfigurasi       |
| Sama sekali tidak bisa konek   | Salah bridge atau firewall    |

---

## 🎯 Tugas Mandiri

✅ Coba buat 1 VM dengan koneksi ke `vmbr0`, pastikan bisa ping ke internet   
✅ (Opsional) Buat jaringan NAT sendiri menggunakan bridge isolated   
✅ Catat IP dan gateway yang dipakai VM   

---

📍 Selanjutnya: [`06_Multi_NIC_dan_Manajemen_Interface.md`](06_Multi_NIC_dan_Manajemen_Interface.md)
Kita akan belajar bagaimana Proxmox menangani **lebih dari satu kartu jaringan (NIC)** dan bagaimana mengelolanya dengan bijak! 🎛️🌐

