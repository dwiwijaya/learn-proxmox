# 🔐 04 - Membuat Jaringan Terisolasi Antar VM

Siap menjelajahi jaringan privat? 🎩✨  
Di bab ini, kita akan membuat **jaringan internal** antar VM di Proxmox, alias **jaringan yang benar-benar terisolasi** — tidak terhubung ke internet, tapi sangat cocok untuk simulasi dan lab testing.

---

## 🎯 Tujuan Bab Ini

- Memahami konsep jaringan internal (isolated LAN)
- Membuat bridge tanpa akses ke dunia luar
- Menghubungkan beberapa VM ke jaringan privat
- Melatih kemampuan simulasi server lokal

---

## 🧠 Apa Itu Jaringan Terisolasi?

Jaringan ini **tidak punya akses ke internet**, dan tidak terhubung ke NIC fisik manapun.  
Biasanya digunakan untuk:

- Simulasi server & client lokal
- Pengujian DNS, DHCP, webserver internal
- Lab mini tanpa risiko bocor ke jaringan publik

> 🎓 Anggap saja seperti kamu bikin LAN sendiri di kamar, tanpa colok ke router.

---

## 🏗️ Arsitektur Sederhana

```

\[ VM1 ]──┐
├── \[ vmbr1 ] ── (tidak terhubung ke NIC fisik)
\[ VM2 ]──┘

````

Semua VM yang terhubung ke `vmbr1` bisa saling berkomunikasi, tapi tidak bisa keluar ke internet.

---

## 🧰 Langkah-langkah Membuatnya

### 1. Buat Bridge Baru (Jika Belum Ada)

Lewat Web GUI:

- Buka: **Datacenter > Node > System > Network**
- Klik **Create > Linux Bridge**
- Masukkan:
  - **Name**: `vmbr1`
  - **Bridge ports**: kosongkan
  - **IPv4/CIDR**: `10.10.10.1/24`
  - **Gateway**: kosongkan
- Klik **OK**, lalu **Apply Configuration**

> ✅ Ini akan membuat jaringan virtual terisolasi, tidak keluar ke mana-mana.

---

### 2. Buat 2 VM untuk Eksperimen

Misalnya:
- `VM-A` (Debian/Ubuntu)
- `VM-B` (Debian/Ubuntu)

Hubungkan keduanya ke **bridge `vmbr1`** saat proses pembuatan VM (atau edit VM > Hardware > Network).

---

### 3. Atur IP Statis Manual

Karena tidak ada DHCP di jaringan ini, kamu perlu set IP manual.

Contoh di VM-A:
```bash
sudo ip addr add 10.10.10.11/24 dev eth0
sudo ip link set eth0 up
````

Di VM-B:

```bash
sudo ip addr add 10.10.10.12/24 dev eth0
sudo ip link set eth0 up
```

---

### 4. Uji Koneksi

Coba ping antar VM:

```bash
ping 10.10.10.12  # dari VM-A ke VM-B
```

Jika berhasil: ✅ Jaringan internal kamu sudah jalan!

---

## 🔐 Kapan Pakai Jaringan Ini?

| Use Case                   | Alasan                                             |
| -------------------------- | -------------------------------------------------- |
| Belajar Client-Server      | Aman, tidak ganggu jaringan kantor                 |
| Simulasi DNS, DHCP, VPN    | Bisa dicoba tanpa takut bentrok dengan sistem lain |
| Lab mini Linux atau Docker | VM saling terkoneksi, tapi tetap tertutup          |

---

## 💡 Tips Tambahan

* Mau kasih internet ke jaringan ini? Tambahkan VM router atau NAT VM sendiri
* Bisa juga tambahkan DHCP server (misal pakai `dnsmasq` atau `isc-dhcp-server`)
* Simulasi topologi jaringan jadi lebih fleksibel dan aman

---

## 🎯 Tugas Mandiri

✅ Buat bridge baru (`vmbr1`) tanpa NIC fisik
✅ Buat dua VM dan hubungkan ke `vmbr1`
✅ Set IP manual dan uji koneksi antar VM
✅ (Opsional) Pasang DHCP server lokal di salah satu VM

---

📍 Selanjutnya: [`05_Instalasi_OS_di_VM.md`](05_Instalasi_OS_di_VM.md)
Kita akan belajar meng-install sistem operasi di dalam VM — seperti install Linux atau Windows di dalam dunia virtual. Let's go deeper! 🧱💻


