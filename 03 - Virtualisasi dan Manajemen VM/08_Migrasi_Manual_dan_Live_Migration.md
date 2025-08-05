# 🔄 08 - Migrasi Manual dan Live Migration

Bayangin kamu lagi jalan-jalan naik kereta, dan tiba-tiba kereta harus diganti... tapi kamu **gak turun**.  
Kamu pindah kereta **tanpa berhenti jalan**.  
Itulah yang disebut **Live Migration** dalam dunia virtualisasi! 🧠🚆

---

## 🎯 Tujuan Bab Ini

- Memahami konsep migrasi VM dan Container antar node
- Menjalankan migrasi manual (offline)
- Menjalankan Live Migration (online, tanpa downtime)
- Mengetahui syarat-syarat agar migrasi berhasil

---

## 🧠 Apa Itu Migrasi VM?

**Migrasi** berarti memindahkan VM atau CT dari satu node ke node lain, dalam satu cluster Proxmox.

Jenis migrasi:

| Jenis          | Penjelasan                                |
|----------------|--------------------------------------------|
| 🛑 Manual Migration | VM dimatikan dulu, baru dipindahkan         |
| 🚀 Live Migration   | VM dipindahkan **tanpa dimatikan**, tetap jalan |

> 📦 Fitur ini hanya bisa digunakan di **cluster Proxmox**, bukan single node.

---

## 🤔 Kenapa Perlu Migrasi?

- 🔧 Maintenance node (misal mau reboot atau update)
- ⚡ Load balancing (node terlalu berat)
- 🛡️ High Availability: jika satu node mati, VM bisa dipindah ke node lain

---

## 📋 Syarat Migrasi Berhasil

| Syarat                       | Keterangan                                      |
|-----------------------------|-------------------------------------------------|
| ✅ Cluster aktif             | Harus ada lebih dari 1 node dan saling terhubung |
| ✅ Shared storage (untuk live) | VM harus pakai penyimpanan yang bisa diakses semua node (cth: NFS, Ceph) |
| ✅ CPU compatibility         | CPU antar node harus mirip/kompatibel          |
| ✅ VM tidak pakai hardware passthrough | Live migration tidak bisa jika VM pakai GPU passthrough, dll |

---

## 🧪 Cara Migrasi Manual (Offline)

1. **Matikan VM/CT terlebih dahulu**
2. Klik kanan → **Migrate**
3. Pilih target node
4. Klik **Migrate**

💡 Cocok untuk migrasi yang tidak butuh uptime tinggi

---

## 🚀 Cara Live Migration

1. Pastikan:
   - VM **dalam keadaan nyala**
   - Gunakan **shared storage**
2. Klik kanan VM → **Migrate**
3. Pilih target node
4. Klik **Migrate**

🧠 Proxmox akan mulai mentransfer memory & state VM ke node tujuan **tanpa mematikan VM**.

> Waktu migrasi tergantung ukuran RAM & kecepatan jaringan antar node.

---

## 🎯 Monitoring Proses Migrasi

- Di web GUI: akan muncul status progress migrasi
- Di CLI:
```bash
# Melihat status task migrasi
qm migrate <vmid> <target-node> --online
````

Untuk container:

```bash
pct migrate <ctid> <target-node> --online
```

---

## ⚠️ Tips Anti-Gagal Migrasi

* Pastikan nama storage **sama** di semua node
* Tes koneksi antar node dengan `ping` dan `ssh`
* Jangan migrasi saat ada proses berat di VM (misal backup)

---

## 📦 Studi Kasus Migrasi

| Situasi                        | Solusi                                   |
| ------------------------------ | ---------------------------------------- |
| Node A terlalu sibuk           | Migrasi VM berat ke Node B               |
| Mau reboot Node A              | Migrasi semua VM ke Node lain            |
| Pindah storage lokal ke shared | Backup → Restore ke shared, lalu migrasi |
| VM tidak bisa live migrate     | Matikan VM, lakukan migrasi manual       |

---

## 🎯 Tugas Mandiri

✅ Buat 2 node dalam cluster (jika belum)
✅ Jalankan 1 VM di Node A
✅ Coba migrasi manual (matikan dulu)
✅ Coba migrasi live (dalam keadaan menyala, storage shared)

---

## 🔗 Selanjutnya: [`09_Snapshot_VM_dan_Container.md`](09_Snapshot_VM_dan_Container.md)

Sebelum melakukan perubahan besar atau eksperimen aneh, kamu pasti ingin bisa “balik ke kondisi semula” kalau gagal...
Di bab selanjutnya, kita akan belajar fitur keren bernama **Snapshot** — seperti tombol undo di dunia virtualisasi! 🕹️⏪

Yuk lanjut! 🎯

