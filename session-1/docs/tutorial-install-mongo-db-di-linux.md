# Cara Install MongoDB di Linux Debian

## Step 1: Website MariaDB
Untuk mempermudah pencarian, langsung saja ketik link https://www.mongodb.com/docs/manual/

## Step 2: MongoDB Community
Selanjutnya klik tombol *MongoDB Community* untuk melanjutkan ke tahap menginstall

<img width="576" height="68" alt="image" src="https://github.com/user-attachments/assets/a60abad5-a576-497a-9bab-2b8391e45282" />

## Step 3: Download MongoDB
Setelah kalian klik tombol *MongoDB Community*, kalian akan ditujukan ke pilihan sistem operasi dan distribusi. Karena menggunakan Linux Debian, ikuti langkah instalasi untuk Debian berikut.

<img width="480" height="155" alt="image" src="https://github.com/user-attachments/assets/8379c84f-3c06-44c3-9281-048c9b6e8308" />

Jika sudah, ikuti instruksinya

### Panduan Instalasi MongoDB Community Edition

Ikuti langkah-langkah berikut untuk menginstall MongoDB Community Edition menggunakan package manager `apt`.

#### 1. Import Public Key

##### Install dependensi yang diperlukan:
```bash
sudo apt-get install gnupg curl
```
<img width="577" height="320" alt="image" src="https://github.com/user-attachments/assets/474e458c-e8bd-4d5c-8644-509a98396cf2" />

##### Import MongoDB public GPG key:
```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
  sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
  --dearmor
```

#### 2. Buat List File

##### Untuk Debian 13 (Trixie):
```bash
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] http://repo.mongodb.org/apt/debian trixie/mongodb-org/8.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```
<img width="642" height="307" alt="image" src="https://github.com/user-attachments/assets/c112a910-bb57-4f77-bbb6-7eb2a997dbb8" />

#### Jika mendapatkan pesan error yang sama, jalankan command berikut.

##### Hapus repository MongoDB yang sudah ada
```bash
sudo rm /etc/apt/sources.list.d/mongodb-org-8.0.list
```

##### Tambahkan repository MongoDB
```bash
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] http://repo.mongodb.org/apt/debian bookworm/mongodb-org/8.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```
<img width="578" height="89" alt="image" src="https://github.com/user-attachments/assets/5e3d290d-30f0-439e-b4bd-bcdcf2a7d2a5" />

#### 3. Reload Database Paket

##### Update database paket lokal:
```bash
sudo apt-get update
```
<img width="576" height="160" alt="image" src="https://github.com/user-attachments/assets/d9e84779-0df9-4d6c-a8cc-79bd1cce316f" />

#### 4. Install MongoDB Community Server

##### Install versi stabil terbaru:
```bash
sudo apt-get install -y mongodb-org
```
<img width="520" height="100" alt="image" src="https://github.com/user-attachments/assets/f5e045ce-14aa-4083-ae6e-9b28baf173c5" />

#### 5. Verifikasi Instalasi

##### Jalankan service MongoDB:
```bash
sudo systemctl start mongod
```
<img width="814" height="404" alt="image" src="https://github.com/user-attachments/assets/9e84deff-475a-44c2-a45e-5124110355b2" />

##### Aktifkan auto-start saat boot:
```bash
sudo systemctl enable mongod
```

##### Periksa status service:
```bash
sudo systemctl status mongod
```

##### Test koneksi:
```bash
mongosh
```

### Catatan Penting

- Panduan ini untuk **Debian 13 (Trixie)**
- Untuk versi Debian lain, sesuaikan nama codename pada langkah 2
