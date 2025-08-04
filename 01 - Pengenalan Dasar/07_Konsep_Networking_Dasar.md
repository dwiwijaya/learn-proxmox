# 🌐 07 - Konsep Networking Dasar

Kalau komputer ibarat manusia, maka **jaringan (networking)** itu seperti sistem komunikasi — mereka bisa ngobrol, kirim file, atau bahkan *remote control* satu sama lain!

Tapi sebelum kita pakai jaringan di Proxmox, kita perlu paham dulu dasar-dasarnya. Yuk mulai dari nol 🔍

---

## 📡 Apa Itu Jaringan Komputer?

Jaringan komputer adalah **hubungan antar perangkat** (PC, laptop, server, printer, dsb) yang memungkinkan mereka saling bertukar data.

📦 Contoh:
- Mengakses Google lewat browser
- File sharing antar komputer
- Remote ke server via SSH

---

## 🧠 Konsep Penting dalam Jaringan

### 1. **IP Address (Alamat IP)**

IP adalah **alamat rumah** komputer dalam jaringan.

Contoh: `192.168.1.10`

- IP Private: digunakan di dalam jaringan lokal (LAN)
- IP Public: bisa diakses dari internet

🔧 IP bisa bersifat:
- **Static**: tetap (diset manual)
- **Dynamic**: berubah-ubah (dari DHCP)

---

### 2. **Subnet Mask**

Subnet mask menentukan **seberapa besar jaringan kita**.

Contoh:  
`255.255.255.0` → artinya kita bisa punya 254 IP dalam jaringan.

Analogi: kalau IP address itu nomor rumah, subnet mask itu kode pos yang menunjukkan area kompleksnya.

---

### 3. **Gateway**

Gateway adalah **pintu keluar jaringan lokal** ke internet.

Biasanya ini adalah IP router/modem kamu.

Contoh:
```bash
Gateway: 192.168.1.1
````

---

### 4. **DNS (Domain Name System)**

DNS mengubah alamat situs (seperti `openai.com`) menjadi IP (seperti `104.22.66.190`)

Analogi: DNS itu kayak "buku telepon" internet 📖

Contoh DNS server:

* Google: `8.8.8.8`
* Cloudflare: `1.1.1.1`

---

## 📶 DHCP - Dynamic Host Configuration Protocol

DHCP secara otomatis memberikan:

* IP Address
* Subnet Mask
* Gateway
* DNS

Kalau gak ada DHCP? Kita harus atur **static IP** manual.

---

## 🧰 Perintah Jaringan Umum di Linux

| Perintah               | Fungsi                                |
| ---------------------- | ------------------------------------- |
| `ip a`                 | Lihat IP address                      |
| `ip r`                 | Lihat routing (gateway dsb)           |
| `ping 8.8.8.8`         | Tes koneksi ke IP                     |
| `ping google.com`      | Tes koneksi DNS                       |
| `nmtui` / `nmtui-edit` | GUI text untuk atur IP (RedHat-based) |
| `ifconfig` (lama)      | Lihat IP (pakai `net-tools`)          |

---

## 🧱 Topologi Jaringan Dasar

* **LAN**: Local Area Network → jaringan lokal (satu gedung)
* **WAN**: Wide Area Network → jaringan antar kota/negara
* **Switch**: Hub penghubung antar device dalam LAN
* **Router**: Penghubung antara jaringan LAN ke WAN (internet)

---

## 📦 Jaringan di Proxmox

Di Proxmox, kamu bisa bikin banyak jenis jaringan virtual:

* **Linux Bridge**: default, mirip switch virtual
* **VLAN**: segmentasi jaringan (1 fisik → banyak virtual)
* **Bonding**: gabungkan 2+ interface untuk failover/load balance
* **NAT**: jaringan VM bisa akses internet via host

💡 Kita akan bahas ini lebih lanjut saat membahas instalasi Proxmox!

---

## 🧠 Pertanyaan Reflektif

* Apa bedanya IP private & IP public?
* Kenapa penting tahu DNS & gateway?
* Kapan harus pakai static IP?

---

📍 Lanjut ke: [`08_Konsep_Storage_Dasar.md`](08_Konsep_Storage_Dasar.md)
Di bab selanjutnya kita bahas tentang jenis-jenis storage yang akan kamu gunakan di Proxmox, termasuk RAID dan ZFS! 💾

