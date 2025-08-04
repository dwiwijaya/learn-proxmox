# 🧱 01 - KVM vs LXC: Pahami Perbedaan VM dan Container

🚀 Sekarang kita naik level ke tahap yang seru banget — saatnya mainan langsung dengan VM dan Container!   
Sebelum kamu mulai bikin-bikin virtual machine (VM) atau container, kita perlu paham dulu: **apa sih bedanya VM dan Container di Proxmox?** Kapan pakai yang mana? Kenapa ada 2 jenis? 🤔

---

## 🧠 Apa Itu KVM dan LXC?

| Teknologi | Singkatan | Digunakan untuk… |
|----------|-----------|------------------|
| **KVM**  | Kernel-based Virtual Machine | Menjalankan **virtual machine** (VM) seperti sistem komputer utuh |
| **LXC**  | Linux Container              | Menjalankan **container ringan** berbasis Linux |

---

## 🖥️ KVM (Virtual Machine)

KVM itu seperti **menyewa satu rumah lengkap** 🏠.  
Kamu dapat sistem operasi (OS) sendiri, kernel sendiri, dan semua resource-nya terisolasi. Bisa jalankan Windows, Linux, BSD, dan OS lainnya.

**Kelebihan KVM:**
- Bisa jalankan OS apapun (Windows, Linux, BSD)
- Isolasi penuh (lebih aman)
- Cocok buat kebutuhan berat: database, server production, dll

**Kekurangan KVM:**
- Lebih berat, karena setiap VM jalankan OS sendiri
- Waktu boot lebih lama
- Konsumsi RAM & CPU lebih besar

---

## 🐳 LXC (Linux Container)

LXC itu seperti **tinggal di apartemen satu gedung** 🏢.  
Kamu pakai ruang sendiri (container), tapi tetap pakai fondasi yang sama (kernel Linux dari host). Jadi lebih ringan dan cepat!

**Kelebihan LXC:**
- Super ringan dan cepat 🚀
- Startup hampir instan
- Cocok buat microservices, dev environment, lab ringan

**Kekurangan LXC:**
- Hanya bisa jalanin Linux (nggak bisa Windows)
- Isolasi tidak sekuat KVM
- Lebih sensitif terhadap update sistem host

---

## ⚖️ Tabel Perbandingan

| Aspek             | KVM (VM)                             | LXC (Container)                     |
|-------------------|--------------------------------------|-------------------------------------|
| OS yang Didukung  | Linux, Windows, BSD, dll             | Hanya Linux                         |
| Isolasi           | Penuh (via hypervisor)               | Sebagian (berbagi kernel)           |
| Resource          | Lebih berat (dedicated OS)           | Sangat ringan                       |
| Keamanan          | Lebih aman (karena isolasi penuh)    | Lebih rentan (berbagi kernel)       |
| Use Case Umum     | Server production, legacy apps       | Lab dev, app ringan, microservices  |
| Boot Time         | Lebih lambat                         | Hampir instan                       |

---

## 🎒 Analogi Simpel: Rumah vs Apartemen

- **KVM = Rumah pribadi** 🏠  
  Kamu bebas atur semuanya, tapi harus bayar semua tagihan dan perawatan sendiri.  
  Aman, tapi mahal dan berat.

- **LXC = Apartemen di gedung bersama** 🏢  
  Lebih hemat dan praktis. Tapi kalau lift rusak, semua orang kena imbasnya. 😄

---

## 🔍 Kapan Gunakan KVM?

✅ Kalau kamu butuh:
- Menjalankan OS non-Linux (misal: Windows Server)
- Isolasi penuh demi keamanan
- Workload berat (database, production app)

## 🔍 Kapan Gunakan LXC?

✅ Kalau kamu butuh:
- Cepat dan ringan (hanya butuh OS Linux)
- Dev/test environment
- Jalankan app ringan, web server, atau script

---

## 🧪 Mini Quiz Ringan

1. Apa kelebihan utama LXC dibanding KVM?
2. Apakah kamu bisa install Windows di LXC?
3. Mana yang cocok untuk menjalankan database besar?

---

## 📦 Kesimpulan

Baik KVM maupun LXC punya tempatnya masing-masing.  
Yang penting kamu **tahu kapan harus pakai yang mana**, dan jangan takut untuk eksperimen! 🔍

Di materi selanjutnya, kita akan langsung **praktek bikin VM dari ISO**. Siap-siap, kamu akan merasa seperti **membangun komputer virtual dari awal**! 💻✨

---

📍 Lanjut ke: `02_Membuat_VM_Baru.md`  
Yuk kita rakit virtual machine pertamamu! 🛠️🖥️
