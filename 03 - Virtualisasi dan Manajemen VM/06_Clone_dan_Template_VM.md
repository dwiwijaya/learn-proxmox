# ♻️ 06 - Clone dan Template VM/Container

Bayangin kamu udah punya satu VM atau container yang isinya udah lengkap: OS, aplikasi, konfigurasi, semua siap.  
Tapi... kamu butuh 5 VM serupa lagi. Masa mau install ulang satu-satu? 😩

Tenang! Proxmox punya fitur **Clone dan Template** yang akan menyelamatkan waktumu! 🕒⚙️

---

## 🎯 Tujuan Bab Ini

- Memahami perbedaan clone dan template
- Mampu membuat clone dari VM atau container
- Membuat template reusable untuk deploy instan

---

## 🧠 Apa Itu Clone?

**Clone** adalah salinan utuh dari sebuah VM atau Container.  
Setelah clone, kamu punya dua sistem identik yang bisa dijalankan secara terpisah.

Ada dua jenis cloning:

| Jenis Clone | Penjelasan | Cocok Untuk |
|-------------|------------|-------------|
| 🔁 **Full Clone** | Duplikasi 100% file disk | Independen, lebih berat |
| 🔗 **Linked Clone** | Berbagi disk dari source | Hemat space, lebih cepat |

> 🧠 Linked clone hanya bisa dibuat dari VM/CT **yang dalam keadaan template**, bukan yang masih aktif.

---

## 🧠 Apa Itu Template?

Template adalah VM atau CT yang disimpan sebagai **“master image”**.  
Template tidak bisa dijalankan langsung, tapi bisa digunakan untuk membuat clone berkali-kali.

> 🎨 Anggap saja template seperti **cetakan kue**. Kamu bisa pakai cetakan yang sama buat bikin banyak kue dengan bentuk dan rasa yang sama 🍰

---

## 🛠️ Cara Mengubah VM/CT Menjadi Template

### Untuk Virtual Machine (VM)

1. Matikan VM
   ![](https://www.tecmint.com/wp-content/uploads/2024/01/Shutdown-VM-in-Proxmox.png)
3. Klik kanan VM → **Convert to Template**   
   <img width="453" height="214" alt="image" src="https://github.com/user-attachments/assets/1fad3081-4aff-43c6-afa4-e791f007942a" />
4. VM akan berubah ikon menjadi template dan tidak bisa dijalankan

---

## 🧪 Cara Melakukan Clone

### Clone VM (Full atau Linked)
1. Klik kanan template → **Clone**   
   ![](https://www.tecmint.com/wp-content/uploads/2024/01/Create-Clone-of-VM-Template.png)
3. Pilih:
   - ID dan Name VM baru
   - Target storage
   - Clone type: Full / Linked   
    <img width="690" height="284" alt="image" src="https://github.com/user-attachments/assets/2a40bc50-97ac-437c-9e75-ef9962059831" />


4. Klik **Clone**

### Clone Container (CT)

1. Klik kanan container → **Clone**
2. Masukkan:
   - CT ID baru
   - Nama CT baru
   - Storage

3. Klik **Clone**

> 📝 Untuk container, cloning bisa langsung dari container aktif, **tidak perlu diubah jadi template dulu**.

---

## 📸 Contoh Penggunaan Template

Misalnya kamu bikin template `debian-base` yang isinya:

- OS Debian 12
- Sudah terinstall: nginx, fail2ban, docker
- Sudah dikonfigurasi IP statik, DNS, dan repo lokal

Sekarang, kamu tinggal **clone dari template ini** dan punya server siap pakai hanya dalam hitungan detik! ⚡

---

## 📂 Lokasi Template di Disk

| Jenis     | Ekstensi File             |
|-----------|---------------------------|
| VM        | Disimpan seperti VM biasa |
| LXC       | `.tar.zst` (CT Template)  |

Untuk LXC, template bisa dilihat di menu **Storage > CT Templates**

---

## ⚖️ Clone vs Template

| Fitur         | Clone                   | Template                    |
|---------------|-------------------------|-----------------------------|
| Bisa dijalankan langsung | ✅ Ya          | ❌ Tidak                    |
| Bisa diclone ulang       | ✅ Ya          | ✅ Ya                       |
| Bisa diubah konfigurasi  | ✅ Ya          | ✅ Saat sebelum/clone       |
| Ideal untuk              | Duplikasi cepat | Cetakan sistem dasar       |

---

## 💡 Tips Produksi

- Simpan template untuk tiap role: `web-template`, `db-template`, `proxy-template`
- Gunakan **linked clone** untuk lab/testing
- Gunakan **full clone** untuk produksi agar lebih stabil dan independen
- Jangan lupa update sistem & patch template secara berkala

---

## 🎯 Tugas Mandiri

✅ Buat 1 VM dasar lalu ubah menjadi template  
✅ Coba buat clone dari template tersebut  
✅ Jalankan hasil clone dan cek apakah semua berjalan normal  
✅ Bandingkan hasil clone full vs linked dari sisi waktu & disk usage

---

## 🔗 Selanjutnya: [`07_Monitoring_VM.md`](07_Monitoring_VM.md)

Sudah banyak VM & Container? Saatnya belajar **memantau performa mereka** 📊  
Di bab berikutnya, kita akan lihat bagaimana cara monitoring CPU, RAM, disk I/O, dan network usage — biar sistemmu tetap optimal! 🧠📈

Yuk lanjut! 🚀
