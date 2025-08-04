# 🌐 05 - Konfigurasi Jaringan LAN dan Bridge

Jaringan adalah *urat nadi* server. Tanpa jaringan yang benar, VM-mu akan seperti pulau terisolasi.  
Di bab ini, kita akan bahas konsep bridge, konfigurasi IP, dan bagaimana menghubungkan VM ke LAN-mu.

---

## 🎯 Tujuan Bab Ini

- Memahami konsep bridge di Proxmox
- Mengkonfigurasi IP static untuk node
- Menyiapkan bridge untuk VM/LXC
- Cek koneksi internet dan komunikasi lokal

---

## 🌉 Apa itu Bridge?

Bridge di Proxmox itu ibarat colokan listrik cabang (extension).  
Dengan bridge, kamu membuat "jembatan" antara:

- **NIC fisik** server (misal: `enp3s0`)
- dan **mesin virtual/container**

Jadi VM bisa ikut numpang lewat ke jaringan yang sama dengan host.

---

## 🧠 Analogi Sederhana

Bayangkan:
- **NIC fisik** = satu kabel LAN ke router
- **Bridge (vmbr0)** = terminal/colokan tambahan
- **VM** = perangkat lain yang ingin ikut internetan

Dengan bridge, semua bisa pakai jaringan yang sama!

---

## 🧱 Struktur Umum Jaringan Proxmox

File konfigurasi:  
```bash
/etc/network/interfaces
````

Contoh isi (static IP):

```bash
auto lo
iface lo inet loopback

auto enp3s0
iface enp3s0 inet manual

auto vmbr0
iface vmbr0 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1
    bridge-ports enp3s0
    bridge-stp off
    bridge-fd 0
```

> 📝 **Keterangan:**
>
> * `enp3s0` adalah NIC utama, dijadikan *manual* (tidak langsung pakai IP)
> * `vmbr0` adalah jembatan (bridge) yang pakai IP dan gateway
> * Semua lalu lintas akan lewat `vmbr0`, termasuk VM nanti

---

## 🔧 Cara Konfigurasi IP Static (jika belum)

> ⚠️ **Jangan ubah file ini sembarangan via CLI kalau belum paham**.
> Lebih aman ubah via WebUI:

1. WebUI → Node → System → Network
2. Edit `vmbr0`:

   * IP Address: `192.168.1.x`
   * Gateway: `192.168.1.1` (atau sesuai jaringanmu)
3. Klik **Apply Configuration**
4. Kalau perlu, **Reboot node**

---

## 🌐 Cek Koneksi Internet & DNS

### Tes koneksi lokal:

```bash
ping 192.168.1.1
```

### Tes ke luar (public):

```bash
ping 8.8.8.8
```

### Tes DNS:

```bash
ping google.com
```

> Jika gagal DNS, cek isi file `/etc/resolv.conf`
> Pastikan ada:

```bash
nameserver 8.8.8.8
```

---

## 🧪 Tes dari VM (nanti)

Kalau bridge `vmbr0` sudah benar, maka VM/Container yang dibuat nanti dan dihubungkan ke bridge itu akan langsung dapat akses LAN/internet—baik via DHCP atau IP static (tergantung setup).

---

## 🧭 Tugas Mandiri

✅ Cek dan pahami struktur jaringan Proxmox   
✅ Pastikan `vmbr0` mengarah ke NIC fisik   
✅ Tes koneksi keluar dan DNS   
✅ Coba reboot dan pastikan setting tetap jalan   

---

📍 Lanjut ke: [`06_Menambah_Disk_dan_Setting_Storage.md`](06_Menambah_Disk_dan_Setting_Storage.md)   
Yuk kita kasih "gudang penyimpanan" tambahan ke server kamu! 📦💾


