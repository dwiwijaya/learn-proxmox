# 🧩 #3 - Pengantar KVM vs LXC

Oke, sobat petualang! 🧙‍♂️  
Setelah mengenal apa itu virtualisasi, sekarang kita akan membahas **dua pendekatan utama virtualisasi** yang digunakan di Proxmox:  
👉 **KVM (Kernel-based Virtual Machine)** dan **LXC (Linux Containers)**.

Keduanya sama-sama bisa digunakan untuk menjalankan sistem lain di atas sistem utama. Tapi… mereka punya cara kerja dan keunggulan yang berbeda.

---

## 🏰 Analogi Sederhana: Rumah vs Kamar

Bayangkan kamu punya sebuah gedung besar (server fisik).  
Lalu kamu ingin menyewakan ruang di dalamnya:

- **KVM** seperti **membangun rumah kecil di dalam gedung itu**, lengkap dengan dapur, kamar mandi, listrik, bahkan pagar sendiri. Artinya, dia **mandiri dan terisolasi total**.
- **LXC** seperti **menyewakan kamar** di dalam gedung. Tetap ada sekat dan privasi, tapi **berbagi sumber daya bersama** (listrik, air, dll).

---

## 🧠 Apa Itu KVM?

**KVM (Kernel-based Virtual Machine)** adalah teknologi **full virtualization**.

🛠 Artinya:
- Menjalankan **sistem operasi lengkap** seperti Windows, Ubuntu, CentOS, dll.
- Setiap VM punya kernel-nya sendiri.
- Lebih fleksibel, tapi **lebih berat** karena butuh semua komponen virtual sendiri.

🎯 Cocok untuk:
- Menjalankan berbagai OS (Linux, Windows).
- Testing, simulasi server produksi.
- Aplikasi yang butuh isolasi tinggi.

---

## 📦 Apa Itu LXC?

**LXC (Linux Containers)** adalah teknologi **container-based virtualization**.

🛠 Artinya:
- Lebih ringan dan cepat, karena **berbagi kernel** dengan host Linux.
- Lebih hemat RAM & CPU.
- Bisa langsung menjalankan Ubuntu, Debian, Alpine, dsb dalam bentuk container.

🎯 Cocok untuk:
- Hosting banyak service kecil (web server, database, dsb).
- DevOps, CI/CD pipelines.
- Server ringan dan efisien.

---

## ⚖️ Perbandingan Cepat

| Fitur          | KVM                         | LXC                             |
|----------------|------------------------------|----------------------------------|
| OS             | Bisa Linux & Windows         | Hanya Linux                     |
| Kernel         | Terpisah (mandiri)           | Berbagi dengan host             |
| Isolasi        | Sangat kuat                  | Cukup kuat                      |
| Performa       | Lebih berat                  | Lebih ringan                    |
| Manajemen      | Seperti PC biasa             | Seperti proses aplikasi         |

---

## 💡 Kapan Pakai KVM, Kapan LXC?

🧭 Gunakan **KVM** jika:
- Butuh OS berbeda dari host (misal host-nya Linux tapi ingin jalankan Windows).
- Butuh isolasi kuat (misal server klien).
- Aplikasi resource-heavy.

🌱 Gunakan **LXC** jika:
- Ingin hemat resource.
- Hanya butuh Linux saja.
- Menjalankan banyak service kecil seperti web app, API, dsb.

---

🎯 Siap lanjut ke pengenalan Proxmox itu sendiri?

🔗 Lanjut ke [#4 - Mengenal Proxmox VE.md](./#4%20-%20Mengenal%20Proxmox%20VE.md)
