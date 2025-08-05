# 🧾 10 - Review Materi Level Ini

Selamat, kamu sudah menyelesaikan seluruh **Level 3: Virtualisasi dan Manajemen VM**! 🎉  
Kamu sekarang sudah bisa menciptakan, mengelola, dan melindungi VM dan Container layaknya **admin sungguhan**! 🧙‍♂️💻

Sekarang saatnya kita **merangkum** apa yang sudah kamu pelajari, dan menguji pemahaman lewat kuis mini 🎯

---

## 🧭 Ringkasan Materi

| Bab | Topik Utama | Inti Pembahasan |
|-----|-------------|------------------|
| `01_KVM_vs_LXC.md` | Dasar Virtualisasi | Perbedaan VM (KVM) dan Container (LXC) |
| `02_Import_ISO_dan_Template.md` | Persiapan OS | Cara import file ISO dan template LXC |
| `03_Membuat_VM_Baru.md` | Buat VM | Langkah-langkah bikin VM dari ISO |
| `04_Membuat_LXC_Container.md` | Buat Container | Membuat LXC container dari template |
| `05_Manajemen_VM_dan_Container.md` | Operasi Dasar | Start, stop, rename, konversi VM/CT |
| `06_Clone_dan_Template_VM.md` | Kloning & Template | Duplikasi VM, buat template reusable |
| `07_Monitoring_VM.md` | Pemantauan | Cek performa VM/CT dari GUI & CLI |
| `08_Migrasi_Manual_dan_Live_Migration.md` | Migrasi VM | Pindah VM antar node, live/manual |
| `09_Snapshot_VM_dan_Container.md` | Snapshot | Ambil snapshot, restore & manajemen |

---

## ❓ Kuis Mini Level 3

Yuk tes pemahamanmu! Jawaban bisa kamu cek sendiri (open book boleh kok 😄).

### 1. Apa perbedaan utama antara VM (KVM) dan Container (LXC)?  
🔲 VM lebih ringan dari container  
🔲 Container punya kernel sendiri  
✅ VM sepenuhnya terisolasi, Container berbagi kernel host

---

### 2. Kapan sebaiknya kita menggunakan **snapshot**?

🔲 Setelah sistem crash  
✅ Sebelum melakukan update besar  
🔲 Setiap hari

---

### 3. Perintah CLI untuk membuat snapshot LXC adalah...  
✅ `pct snapshot <ctid> <nama>`  
🔲 `lxc snapshot`  
🔲 `qm snapshot`

---

### 4. Fitur yang memungkinkan migrasi VM tanpa downtime disebut...  
✅ Live Migration  
🔲 Cold Migration  
🔲 Snapshot Restore

---

### 5. Bagaimana cara melihat penggunaan CPU/RAM VM via CLI?  
✅ `qm monitor <vmid>`  
🔲 `pct restart <ctid>`  
🔲 `pve-status`

---

## 🧙 Tips Level Mahir

Setelah ini kamu bisa mulai:

✅ Menyiapkan jaringan lanjutan (VLAN, bonding)  
✅ Mengatur storage eksternal (ZFS, NFS, iSCSI)  
✅ Belajar clustering & High Availability

> 📚 Level 4 dan seterusnya akan membahas jaringan, storage, cluster, dan backup! 🔥

---

## 🧩 Tantangan Opsional

💡 **Simulasikan Lab Virtualisasi Kecil:**

- Buat 2 VM Linux (misal Debian & Ubuntu)
- Buat 1 container LXC ringan (misal Alpine)
- Setup jaringan NAT atau bridged agar bisa ping-an
- Monitor performa, ambil snapshot, lalu eksperimen bebas

---

## 🚀 Selanjutnya: [`04_Jaringan_di_Proxmox`](../04_Jaringan_di_Proxmox)

Virtualisasi tanpa jaringan itu seperti rumah tanpa listrik! ⚡  
Di level selanjutnya, kita akan menyelami dunia jaringan:  
Bridge, NAT, VLAN, Bonding, dan semua konfigurasi yang bikin VM kamu bisa terkoneksi dengan dunia luar 🌐

Ayo lanjut ke Level 4: **Jaringan di Proxmox**! 🔧🛜
