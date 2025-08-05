# 📊 07 - Monitoring VM dan Container di Proxmox

Punya banyak VM dan Container itu keren... tapi gimana cara tahu mereka jalan lancar atau diam-diam bikin server ngos-ngosan? 🤯

Di bab ini, kita akan belajar cara **memantau performa** VM/CT: mulai dari CPU, RAM, Disk, sampai Network.  
Supaya kamu jadi admin yang sigap dan gak panik saat resource tiba-tiba penuh! 😎🛡️

---

## 🎯 Tujuan Bab Ini

- Mengenal fitur monitoring bawaan Proxmox
- Melihat statistik penggunaan resource VM dan CT
- Belajar membaca grafik & mengambil keputusan dari data
- Mengetahui tool CLI dan eksternal untuk monitoring lanjutan

---

## 🧠 Kenapa Monitoring Itu Penting?

Monitoring itu seperti **dashboard mobil**.  
Tanpa itu, kamu gak tahu kapan bensin habis, mesin panas, atau ban bocor.

> 🚗 Tanpa monitoring, kamu seperti nyetir mobil dengan mata tertutup!

Dengan monitoring, kamu bisa:
- Deteksi performa lambat sebelum jadi masalah besar
- Tahu kapan harus upgrade resource
- Cegah VM/CT nge-lag karena kehabisan RAM/CPU

---

## 📍 Lokasi Monitoring di Proxmox GUI

Setiap VM dan CT punya tab bernama **“Summary”** yang menampilkan grafik real-time:   
<img width="1280" height="1024" alt="image" src="https://github.com/user-attachments/assets/ed806112-e9a2-4e7e-ab56-5d2ee46644f7" />

### Statistik yang Ditampilkan:

| Komponen | Penjelasan |
|----------|------------|
| 🧠 CPU     | Penggunaan core oleh VM/CT (dalam %) |
| 📦 Memory  | Total dan penggunaan RAM |
| 💽 Disk I/O | Kecepatan baca/tulis disk |
| 🌐 Network | Lalu lintas jaringan masuk dan keluar |

> Semua data ini ditampilkan dalam bentuk grafik per menit, jam, hari, bahkan bulan.

---

## 🔎 Contoh Situasi Monitoring

| Gejala | Penyebab Kemungkinan | Tindakan |
|--------|----------------------|----------|
| CPU usage 100% terus | Proses berat di dalam VM | Cek pakai `top` atau `htop` di VM |
| RAM penuh | Beban terlalu besar | Tambah RAM atau optimasi aplikasi |
| Disk I/O tinggi | Backup berjalan / proses berat | Jadwalkan backup di luar jam sibuk |
| Network spike | Update, download, atau serangan | Cek proses dalam VM dan firewall |

---

## 🛠 Tool CLI untuk Monitoring

Kamu bisa pakai terminal Proxmox untuk cek resource juga!

### Cek resource di node host:
```bash
top
htop
iotop
iftop
````

### Cek resource VM/CT dari Proxmox CLI:

```bash
# Cek list VM + status singkat
qm list
pct list

# Info detail VM
qm status <vmid> --verbose

# Info detail CT
pct status <ctid>
```

> Kamu juga bisa akses langsung ke dalam VM/CT dan jalankan `htop`, `free -m`, `df -h`, dll.

---

## 📥 Monitoring Lebih Lanjut (Opsional)

Kalau butuh monitoring tingkat lanjut, kamu bisa integrasikan Proxmox dengan tools eksternal seperti:

| Tool                    | Kelebihan                           |
| ----------------------- | ----------------------------------- |
| 🔍 Zabbix               | Monitoring enterprise, notifikasi   |
| 📈 Grafana + Prometheus | Dashboard custom dan powerful       |
| 🧭 Netdata              | Realtime, ringan, visual interaktif |

Tapi untuk belajar dasar, fitur bawaan Proxmox sudah sangat cukup! 🙌

---

## 📦 Tips Pemantauan Sehari-hari

* Cek **Summary tab** tiap kali VM/CT terasa lambat
* Gunakan warna grafik untuk tahu tren (warna merah = warning!)
* Cek node host juga, bukan cuma VM-nya!
* Aktifkan notifikasi email (jika perlu) agar dapat alert otomatis

---

## 🎯 Tugas Mandiri

✅ Cek statistik dari minimal 1 VM dan 1 Container
✅ Bandingkan pemakaian CPU dan RAM mereka
✅ Gunakan `htop` dalam VM untuk melihat proses paling berat
✅ Coba `iotop` dan `iftop` di Proxmox host untuk melihat disk dan jaringan

---

## 🔗 Selanjutnya: [`08_Migrasi_Manual_dan_Live_Migration.md`](08_Migrasi_Manual_dan_Live_Migration.md)

Sudah siap upgrade ke level sysadmin sejati? 💼
Di bab selanjutnya kita akan bahas **migrasi VM antar node**, baik secara manual maupun live — biar server kamu fleksibel dan selalu siap gagal node! 🔄🧠

Yuk lanjut! ⚡

