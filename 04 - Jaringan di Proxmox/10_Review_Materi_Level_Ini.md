# 🧠 10 - Review Materi Level Ini

Selamat! Kamu sudah menyelesaikan **Level 4: Jaringan di Proxmox**! 🎉
Sekarang saatnya kita **menyegarkan kembali ingatan**, **merangkum inti tiap bab**, dan **menguji pemahamanmu lewat mini quiz**. Biar ilmunya makin awet! 🧪✨

---

## 🗺️ Rangkuman Materi

| No | Topik                          | Inti Pembahasan                             |
| -- | ------------------------------ | ------------------------------------------- |
| 01 | Konsep Jaringan Virtual        | Bridging, NAT, vswitch, virtual NIC         |
| 02 | Jenis Jaringan di Proxmox      | Bridged, NAT, host-only, routed             |
| 03 | Konfigurasi Bridge & Interface | vmbr0, vmbr1, `/etc/network/interfaces`     |
| 04 | Jaringan Terisolasi            | LAN internal-only untuk lab                 |
| 05 | Internet untuk VM              | NAT, bridge ke router, gateway, DNS         |
| 06 | Multi-NIC & Interface          | Banyak NIC, WAN/LAN, mapping interface      |
| 07 | VLAN & 802.1q                  | Tagging VLAN, aktivasi di Proxmox           |
| 08 | Bonding & Failover             | LACP, active-backup untuk HA jaringan       |
| 09 | Troubleshooting                | Ping, traceroute, tcpdump, analisis koneksi |

---

## 🧪 Mini Quiz Level 4

> Jawablah dengan jujur, boleh sambil nyontek catatanmu. 😄
> Tandai mana yang kamu paham, mana yang perlu diulang.

### 1. Apa perbedaan `bridged` dan `NAT` di jaringan virtual?

✅ Paham
🔁 Belum yakin

---

### 2. Di file apa konfigurasi jaringan utama Proxmox disimpan?

✅ Paham
🔁 Belum yakin

---

### 3. Sebutkan langkah agar VM bisa akses internet melalui NAT.

✅ Paham
🔁 Belum yakin

---

### 4. Apa fungsi dari VLAN tag di Proxmox?

✅ Paham
🔁 Belum yakin

---

### 5. Apa yang dilakukan perintah `tcpdump -i eth0`?

✅ Paham
🔁 Belum yakin

---

### 6. Kamu diberi kasus: “VM tidak bisa ping gateway.”

Apa saja langkah troubleshooting yang kamu lakukan?

✅ Paham
🔁 Belum yakin

---

## 🧰 Tips Penutup

🧠 Jaringan adalah pondasi semua layanan virtual. Jangan buru-buru, pahami pelan-pelan.
🔌 Selalu mulai troubleshooting dari dasar: IP → gateway → DNS → firewall.
💻 Punya lab mini sangat membantu eksplorasi jaringan lebih dalam!

---

## 🧭 Arah Selanjutnya

Selamat, kamu sudah menaklukkan jaringan! 🎉
Kini saatnya melangkah ke tantangan berikutnya: **Level 5 – Storage di Proxmox**.

Di sana kamu akan belajar tentang:

* Cara kerja storage virtual
* Pool, volume, disk image
* ZFS, LVM, dan storage eksternal
* Mount ISO, disk share, dan snapshot storage

📍 Next stop: [`01_Konsep_Dasar_Storage.md`](../05_Storage/01_Konsep_Dasar_Storage.md)
Siap menjelajah dunia penyimpanan virtual? 💾🌐


