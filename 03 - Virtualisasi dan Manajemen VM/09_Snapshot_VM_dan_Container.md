# 📸 09 - Snapshot VM dan Container

Pernah utak-atik sistem, lalu rusak dan nyesel?  
Andai ada tombol “undo”...  
**Nah, Snapshot adalah tombol undo-nya VM dan Container di Proxmox!** 🧙‍♂️⏪

---

## 🎯 Tujuan Bab Ini

- Memahami apa itu snapshot
- Mengetahui kapan harus pakai snapshot
- Membuat dan mengelola snapshot
- Restore dari snapshot saat terjadi kesalahan

---

## 🧠 Apa Itu Snapshot?

Snapshot adalah **cuplikan kondisi sistem VM/CT saat itu**, termasuk:

- Status disk
- RAM (jika diset)
- Konfigurasi VM/CT

Dengan snapshot, kamu bisa:

- 🚀 Coba update sistem tanpa takut gagal
- 🧪 Uji konfigurasi server
- 🔄 Rollback cepat saat error

---

## 📦 Jenis Snapshot di Proxmox

| Jenis            | Penjelasan                              |
|------------------|------------------------------------------|
| 📁 Disk Snapshot | Snapshot hanya kondisi disk (default)   |
| 🧠 RAM Snapshot  | Termasuk status RAM (kondisi berjalan)   |
| ⚠️ Live Snapshot | Snapshot saat VM masih aktif (bisa dilakukan tergantung storage) |

> 🧠 Tidak semua jenis storage support snapshot. Biasanya hanya ZFS, LVM-thin, Ceph, dan Btrfs.

---

## 💡 Kapan Perlu Snapshot?

| Situasi                             | Snapshot? |
|-------------------------------------|-----------|
| 🚀 Sebelum update OS                | ✅        |
| 🧪 Mau coba konfigurasi firewall    | ✅        |
| 💻 Baru install software eksperimen | ✅        |
| ⚠️ VM sudah stabil dan jarang berubah | ❌        |

---

## 🛠️ Cara Membuat Snapshot

### Via Web GUI

1. Pilih VM atau CT
2. Tab **Snapshots**
3. Klik **Take Snapshot**
4. Isi:
   - Nama snapshot
   - Centang "Include RAM" (jika perlu)
   - Optional: Deskripsi

🧠 Jika centang RAM, snapshot bisa lebih besar ukurannya.

---

### Via CLI

#### Untuk VM:
```bash
qm snapshot <vmid> <snapshot-name> --description "Snapshot sebelum update"
````

Contoh:

```bash
qm snapshot 100 sebelum-update --description "VM stabil sebelum upgrade ke Debian 13"
```

#### Untuk CT:

```bash
pct snapshot <ctid> <snapshot-name>
```

---

## 🔁 Cara Restore Snapshot

### Web GUI:

1. Pilih snapshot
2. Klik **Restore**
3. Konfirmasi

> ❗ VM akan dimatikan saat restore snapshot.

---

### CLI:

#### VM:

```bash
qm rollback <vmid> <snapshot-name>
```

#### CT:

```bash
pct rollback <ctid> <snapshot-name>
```

---

## 🧼 Menghapus Snapshot

Setelah yakin sistem stabil dan snapshot tak diperlukan lagi:

```bash
qm delsnapshot <vmid> <snapshot-name>
pct delsnapshot <ctid> <snapshot-name>
```

> ⚠️ Snapshot menempati ruang disk, jangan lupa bersihkan yang sudah tidak dipakai.

---

## ⚠️ Tips Snapshot

* Jangan terlalu sering ambil snapshot tanpa dihapus → bisa bikin disk penuh
* Jangan andalkan snapshot sebagai **backup**! Snapshot hanya cocok untuk rollback jangka pendek
* Idealnya: ambil snapshot sebelum perubahan besar

---

## 🧠 Analogi: Save Game vs Backup

| Fitur         | Snapshot             | Backup                               |
| ------------- | -------------------- | ------------------------------------ |
| Tujuan        | Rollback cepat       | Restore total jika terjadi kerusakan |
| Kecepatan     | Cepat                | Lebih lambat                         |
| Fleksibilitas | Terbatas             | Bisa dipindah, arsip jangka panjang  |
| Penyimpanan   | Bergantung pada host | Bisa di luar host (NFS, USB, cloud)  |

> 🎮 Snapshot = “Save game”
> 🗄️ Backup = “Salin seluruh harddisk ke tempat aman”

---

## 🎯 Tugas Mandiri

✅ Coba ambil snapshot 1 VM / CT
✅ Lakukan perubahan (misal: ubah konfigurasi / install app)
✅ Restore snapshot & lihat hasilnya
✅ Tes juga via CLI

---

## 📍 Selanjutnya: [`10_Review_Materi_Level_Ini.md`](10_Review_Materi_Level_Ini.md)

Kamu sudah hampir selesai menaklukkan Level 3! 🏁
Di bab penutup ini, kita akan review semua hal penting: dari membuat VM hingga migrasi dan snapshot.
Siap menguji pemahamanmu lewat kuis mini? 💡🎓
