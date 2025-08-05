# 🕵️‍♂️ 09 - Troubleshooting Jaringan VM

Sudah buat VM, sudah disambung ke bridge, tapi... **nggak bisa internet?**
Atau malah **nggak bisa ping antar VM?** 😵
Tenang, ini saatnya kita belajar jadi detektif jaringan!

---

## 🎯 Tujuan Bab Ini

* Mengenali masalah umum jaringan VM
* Menggunakan alat bantu seperti `ping`, `traceroute`, `tcpdump`
* Menelusuri dan memperbaiki koneksi antar VM atau ke internet

---

## 🚨 Masalah Umum

| Gejala                         | Kemungkinan Penyebab                      |
| ------------------------------ | ----------------------------------------- |
| ❌ VM tidak bisa internet       | Gateway salah, DNS salah, NAT tidak aktif |
| ❌ VM tidak bisa ping antar VM  | Isolasi bridge, firewall aktif            |
| ❌ Tidak bisa diakses dari luar | IP salah, belum port forwarding           |
| 🔄 Ping putus-nyambung         | Konflik IP, masalah bonding               |

---

## 🛠️ Alat Bantu Dasar Troubleshooting

### 1. `ping` – Cek Konektivitas

```bash
ping 8.8.8.8
```

* Bisa ping = koneksi dasar OK
* Nggak bisa ping = cek IP, gateway, bridge

> 💡 Gunakan juga `ping` antar VM:
> `ping 192.168.100.10`

---

### 2. `ip a` – Cek IP Address

```bash
ip a
```

Pastikan interface VM kamu (biasanya `eth0`) punya IP yang benar sesuai subnet.

---

### 3. `ip r` – Cek Routing Table

```bash
ip r
```

Pastikan ada **default route** ke gateway:

```
default via 192.168.1.1 dev eth0
```

Kalau tidak ada, maka internet tidak akan bisa diakses.

---

### 4. `cat /etc/resolv.conf` – Cek DNS

Isi file ini seharusnya berisi server DNS, misalnya:

```
nameserver 8.8.8.8
```

> 💡 Tanpa DNS, kamu tidak bisa `ping google.com`, tapi bisa `ping 8.8.8.8`.

---

### 5. `traceroute` – Lacak Jalur

```bash
traceroute google.com
```

Menunjukkan rute yang dilewati sampai ke tujuan.
Kalau macet di tengah, kamu bisa tahu di mana kira-kira masalahnya.

---

### 6. `tcpdump` – Sniffing Paket

```bash
tcpdump -i eth0
```

Lihat langsung lalu lintas jaringan di interface.
Bisa digunakan untuk:

* Melihat apakah paket keluar
* Melihat apakah VM menerima paket masuk

> 🔍 Cocok untuk debugging yang lebih dalam.

---

## 📦 Cek dari Host Proxmox

Jangan lupa: kamu bisa juga cek dari sisi host Proxmox!

### Cek status interface:

```bash
ip link
```

### Cek bridge dan port yang terhubung:

```bash
brctl show
```

> 💡 Pastikan VM kamu terhubung ke bridge yang benar.

---

## 📋 Contoh Skenario & Solusi

### ❌ VM tidak bisa internet

1. Cek apakah bridge punya gateway dan DNS
2. Cek NAT aktif jika menggunakan routed/NAT mode
3. Cek `iptables` atau firewall

### ❌ VM tidak bisa ping VM lain

1. Cek apakah VM berada di bridge yang sama
2. Cek firewall di dalam VM (misalnya `ufw` di Ubuntu)
3. Coba matikan firewall sementara untuk tes:

```bash
ufw disable
```

---

## 🧠 Tips Praktis

* Gunakan satu VM sebagai "test client" untuk ping semua VM lain
* Catat semua IP dan subnet untuk tiap VM
* Buat diagram jaringan kecil untuk memudahkan debug
* Simpan output log dan hasil tes untuk dokumentasi

---

## 🎯 Tugas Mandiri

✅ Ping antar VM
✅ Ping ke internet dari VM
✅ Tes DNS (`ping google.com`)
✅ Gunakan `tcpdump` untuk melihat paket keluar
✅ Ubah salah satu konfigurasi (misal DNS salah) lalu perbaiki

---

📍 Selanjutnya: [`10_Review_Materi_Level_Ini.md`](10_Review_Materi_Level_Ini.md)
Saatnya review semua ilmu jaringan yang sudah kamu pelajari di level ini dan uji pemahamanmu lewat mini quiz! 🧠💪



Kalau kamu siap, kita langsung gas ke sesi review & kuis! 🎓📘
