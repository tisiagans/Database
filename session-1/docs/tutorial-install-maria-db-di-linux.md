# Cara Install MariaDB di Linux Debian

## Step 1: Website MariaDB
Untuk mempermudah pencarian, langsung saja ketik link https://mariadb.com/docs/server
<img width="866" height="259" alt="image" src="https://github.com/user-attachments/assets/198d90f7-e86e-41bc-ac42-345504b07fb7" />

## Step 2: Quickstart Guides
Selanjutnya klik tombol *Quickstart Guides* lalu klik tombol *Installing MariaDB Server Guide* untuk mendapatkan perintah mengunduh MariaDB.
<img width="692" height="62" alt="image" src="https://github.com/user-attachments/assets/90b0da94-cbd2-4a70-b82b-157e9438fba8" />

<img width="344" height="62" alt="image" src="https://github.com/user-attachments/assets/75a8a339-5509-41a3-b767-d46dbd4f7d4f" />

## Step 3: Download MariaDB
Untuk mendownlaod MariaDB, sesuaikan distribusi Linux kalian, seperti Debian, Mint, atau Arch.
<img width="670" height="269" alt="image" src="https://github.com/user-attachments/assets/3b3894b1-0c0a-4a58-a78a-adae4215d765" />

Cara install MariaDB ke Linux, ikuti command yang tertera pada dokumentasi resmi. Panduan ini menggunakan contoh Linux Debian.

### Panduan Install MariaDB Server

#### 1. Perbarui Daftar Paket

Sebelum melakukan install, praktik yang baik adalah memperbarui indeks paket terlebih dahulu.

##### Untuk Debian/Ubuntu:
```bash
sudo apt update
```
<img width="442" height="76" alt="image" src="https://github.com/user-attachments/assets/836c39c8-f26e-4497-881d-c4e289052f1d" />

Jika mendapatkan pesan error yang sama, jalankan command dengan hak akses root (gunakan sudo) seperti contoh berikut:
```bash
su root
```
<img width="756" height="224" alt="image" src="https://github.com/user-attachments/assets/772e26dd-1e7f-4763-aa30-e4faff0075a2" />

#### 2. Install MariaDB Server

Install paket MariaDB server dan client.

##### Untuk Debian/Ubuntu:
```bash
sudo apt install mariadb-server mariadb-client
```
<img width="766" height="390" alt="image" src="https://github.com/user-attachments/assets/d73362e3-25df-4119-ba61-25368010f3ce" />

#### 3. Amankan Install

Setelah install, jalankan script keamanan untuk mengatur password root, menghapus user anonim, dan menonaktifkan login root dari jarak jauh.

```bash
sudo mariadb-secure-installation
```

Ikuti petunjuk untuk mengonfigurasi pengaturan keamanan Anda.

#### 4. Jalankan dan Verifikasi Service

MariaDB biasanya akan otomatis berjalan setelah install. Anda dapat memeriksa statusnya dan menjalankannya secara manual jika diperlukan.

##### Periksa status:
```bash
sudo systemctl status mariadb
```
<img width="788" height="246" alt="image" src="https://github.com/user-attachments/assets/5bb83723-a967-4854-91b0-5eb5b50df05f" />

##### Jalankan service (jika belum berjalan):
```bash
sudo systemctl start mariadb
```

##### Verifikasi Install dengan menghubungkan sebagai root:
```bash
mariadb -u root -p
```

Masukkan password root yang telah Anda atur selama proses secure installation.

#### Perintah Tambahan

##### Enable auto-start saat boot:
```bash
sudo systemctl enable mariadb
```

##### Restart service:
```bash
sudo systemctl restart mariadb
```

##### Stop service:
```bash
sudo systemctl stop mariadb
```
