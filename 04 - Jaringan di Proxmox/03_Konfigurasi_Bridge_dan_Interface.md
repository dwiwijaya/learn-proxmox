# 🌉 03 - Konfigurasi Bridge dan Interface di Proxmox

Selamat datang di dunia jaringan virtual! 🌐✨  
Di bab ini, kita akan belajar tentang **Bridge (vmbr)** di Proxmox — jembatan penting agar VM kamu bisa berkomunikasi dengan dunia luar (atau antar sesama VM).

---

## 🎯 Tujuan Bab Ini

- Mengenal konsep **bridge** di Proxmox (`vmbr0`, `vmbr1`, dst)
- Belajar membuat dan mengelola bridge lewat **GUI**
- Opsional: edit konfigurasi bridge secara manual via CLI
- Menyiapkan bridge tambahan untuk VM internal

---

## 🧠 Apa Itu Bridge (`vmbr`)?

Bayangkan kamu punya beberapa VM di dalam server Proxmox.  
Agar mereka bisa "nyambung" ke jaringan luar atau saling ngobrol, kamu butuh **switch virtual** — itulah **bridge**.

> Bridge = jembatan antara NIC fisik (seperti `enp3s0`) dan dunia virtual (VM/CT)

### 🎯 Contoh:
- `vmbr0` → default bridge (biasanya terhubung ke NIC fisik)
- `vmbr1` → bridge tambahan (bisa untuk jaringan internal antar VM)

---

## 🖥️ Membuat Bridge Lewat Web GUI (Recommended)

Ini cara termudah, cocok buat semua level!

### Langkah-langkah:

1. Buka Web GUI Proxmox (https://<ip-kamu>:8006)
2. Masuk ke:  
   **Datacenter > <Nama Node> > System > Network**
3. Klik tombol **Create > Linux Bridge**
4. Isi parameter:
   - **Name**: `vmbr1`
   - **Bridge ports**: kosongkan (jika tanpa NIC fisik)
   - **IPv4/CIDR**: `10.10.10.1/24` (contoh internal LAN)
   - **Gateway**: kosongkan jika tidak keluar internet
5. Klik **OK**
6. Klik tombol **Apply Configuration** untuk mengaktifkan

> ⚠️ Hati-hati! Klik ini bisa memutus koneksi jika kamu sedang remote. Pastikan punya akses fisik/console jika salah setting.

---

## 🔧 Contoh Penggunaan

| Jenis Bridge | Fungsi                  | Terhubung ke       |
|--------------|--------------------------|---------------------|
| `vmbr0`      | Akses internet umum      | `enp3s0` (NIC fisik)|
| `vmbr1`      | LAN internal antar VM    | (tanpa NIC fisik)   |
| `vmbr2`      | VLAN atau VLAN-aware LAN | `enp4s0`            |

---

## 🛠️ (Opsional) Konfigurasi Bridge Manual via CLI

Jika kamu ingin lebih fleksibel atau bekerja via SSH/console:

### 1. Buka file konfigurasi:

```bash
nano /etc/network/interfaces
````

### 2. Contoh isi file:

```ini
auto lo
iface lo inet loopback

iface enp3s0 inet manual

auto vmbr0
iface vmbr0 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1
    bridge-ports enp3s0
    bridge-stp off
    bridge-fd 0

auto vmbr1
iface vmbr1 inet static
    address 10.10.10.1/24
    bridge-ports none
    bridge-stp off
    bridge-fd 0
```

### 3. Terapkan perubahan:

```bash
systemctl restart networking
# atau reboot jika ragu
```

---

## 🧪 Eksperimen Mini

| Tujuan              | Langkah                           |
| ------------------- | --------------------------------- |
| Buat VM internal    | Hubungkan ke `vmbr1`              |
| Coba ping antar VM  | Pastikan mereka saling terkoneksi |
| Ubah bridge default | Tes koneksi internet via `vmbr0`  |
| Tambah 2 bridge     | Simulasi jaringan dengan 2 subnet |

---

## 🧠 Tips dari Mentor

* Gunakan Web GUI untuk awal, CLI jika sudah mantap
* Simpan backup konfigurasi sebelum ubah (copy `/etc/network/interfaces`)
* Bridge bisa dihubungkan ke NIC fisik atau tidak, tergantung kebutuhan
* Selalu pastikan kamu punya akses lokal sebelum klik **Apply Configuration** di GUI

---

## 🎯 Tugas Mandiri

✅ Buat 1 bridge baru (`vmbr1`) lewat GUI
✅ Coba hubungkan 2 VM ke bridge tersebut dan tes ping
✅ (Opsional) Ubah file `/etc/network/interfaces` dan pelajari strukturnya

---

📍 Selanjutnya: [`04_Membuat_Jaringan_Terisolasi.md`](04_Membuat_Jaringan_Terisolasi.md)
Kita akan membuat lab mini dengan jaringan internal antar VM saja. Tanpa internet, bebas gangguan! 🔐🧪

