# Cara Integrasi VS Code Dengan GitHub 

## Step 1: Install VS Code
Pertama-tama sebelum mengintegrasikan VS Code dengan GitHub, kita terlebih dahulu mendownload VS Code di website resminya, yaitu code.visualstudio.com/docs/setup/linux (untuk Linux).
Untuk menu lain selain Linux, bisa dilihat pada websitenya

<img width="145" height="384" alt="image" src="https://github.com/user-attachments/assets/22fe9a1d-da2f-44a6-a989-7a16f4394167" />

## Step 2: Command Untuk Download dan Install VS Code di Linux Debian
Selanjutnya klik *"Download and install Visual Studio Code for your Linux distribution"*
<img width="617" height="110" alt="image" src="https://github.com/user-attachments/assets/7549abe4-67f5-4cf0-86c4-28e2dadf581f" />

### Panduan Instalasi Visual Studio Code untuk Debian/Ubuntu

#### 1. Instalasi Menggunakan Paket .deb (Cara Termudah)

Cara termudah untuk menginstal Visual Studio Code di distribusi berbasis Debian/Ubuntu adalah dengan mengunduh dan menginstal paket .deb (64-bit), baik melalui pusat perangkat lunak grafis jika tersedia, atau melalui command line dengan:

```bash
sudo apt install ./<file>.deb

# Jika Anda menggunakan distribusi Linux yang lebih lama, jalankan perintah ini:
# sudo dpkg -i <file>.deb
# sudo apt-get install -f # Instalasi dependensi
```
<img width="677" height="207" alt="image" src="https://github.com/user-attachments/assets/36d4a745-9a04-481d-a5ed-4c77c3ca6b09" />

Jika kedua command tidak bekerja, coba command terakhir seperti gambar di atas

> **Catatan:**
> Binary lainnya juga tersedia di halaman unduh VS Code.
> Ketika Anda menginstal paket .deb, sistem akan meminta untuk menginstal repositori apt dan signing key untuk mengaktifkan pembaruan otomatis menggunakan package manager sistem.

#### 2. Instalasi Otomatis Repositori APT

Untuk menginstal repositori apt dan signing key secara otomatis, seperti pada terminal non-interaktif, jalankan perintah berikut terlebih dahulu:

```bash
echo "code code/add-microsoft-repo boolean true" | sudo debconf-set-selections
```
<img width="642" height="31" alt="image" src="https://github.com/user-attachments/assets/d9a5cc1f-eb60-49b4-b6e7-b4d4dac662b4" />

#### 3. Instalasi Manual Repositori APT

##### 3.1 Instalasi Signing Key

Jalankan script berikut untuk menginstal signing key:

```bash
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -D -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/microsoft.gpg
rm -f microsoft.gpg
```
<img width="643" height="208" alt="image" src="https://github.com/user-attachments/assets/3b7fc3e1-ea05-43e4-88d1-721d060f36f7" />

##### 3.2 Membuat File Repositori

Buat file `/etc/apt/sources.list.d/vscode.sources` dengan konten berikut untuk menambahkan referensi ke repositori paket upstream:

```text
Types: deb
URIs: https://packages.microsoft.com/repos/code
Suites: stable
Components: main
Architectures: amd64,arm64,armhf
Signed-By: /usr/share/keyrings/microsoft.gpg
```
<img width="636" height="150" alt="image" src="https://github.com/user-attachments/assets/132f1002-d11f-4c82-895c-44e4e6b455f4" />

##### 3.3 Update dan Instalasi

Terakhir, perbarui cache paket dan instal paket:

```bash
sudo apt install apt-transport-https
sudo apt update
sudo apt install code # atau code-insiders
```
<img width="452" height="171" alt="image" src="https://github.com/user-attachments/assets/88e0ade6-5546-4d9c-8e5e-0cc0ac513de6" />

<img width="638" height="384" alt="image" src="https://github.com/user-attachments/assets/315413da-291c-49ee-ab68-f174f3d04d6f" />

#### Selesai!

Visual Studio Code sekarang sudah terinstal di sistem Anda dan siap digunakan. Anda dapat menjalankannya dari menu aplikasi atau dengan mengetik `code` di terminal.

## Step 3: Integrasikan VS Code dengan GitHub
Pertama kalian harus download Git di website resminya, yaitu http://git-scm.com/downloads dan pilih Linux/Unix

<img width="292" height="170" alt="image" src="https://github.com/user-attachments/assets/e8c2f950-4c99-4862-b693-64fcab1a49b6" />

Setelah kalian pilih Linux/Unix. cari distribusi yang sesuai. Untuk Debian jalankan command
```bash
apt-get install git
```
<img width="571" height="330" alt="image" src="https://github.com/user-attachments/assets/dfc967ac-c4f7-401b-a68f-db138bdc3afb" />

<img width="643" height="387" alt="image" src="https://github.com/user-attachments/assets/cb9d82b1-dffc-4e76-8513-b6e9a54995cc" />

Setelah selesai, pergi ke VS Code dan buka terminal dengan klik tombol keyboard Ctrl + Shift + P dan cari *"Terminal: Create New Terminal"*

Dalam terminal VS Code, ketik command
```bash
git config --global user.name (nama akun github kalian)
git config --global user.email (email akun github kalian)
```
Catatan: hapus tanda "()".

Jika sudah selesai, pergi ke repository di GitHub lalu copy link untuk cloning repository GitHub

<img width="461" height="349" alt="image" src="https://github.com/user-attachments/assets/c521bb6e-7dd2-421c-97d5-f2109da5035f" />

Lalu pergi ke VS Code dan klik menu *"Source Control"* lalu pilih *"Clone Repository"*, dan terakhir paste link cloning repository GitHub yang sudah di copy sebelumnya.

<img width="763" height="322" alt="image" src="https://github.com/user-attachments/assets/43f3b3d2-d011-4390-8c41-4e97faf6eeed" />

Terakhir, pilih menu Open dan clone repository GitHub sudah jadi.

<img width="574" height="140" alt="image" src="https://github.com/user-attachments/assets/46ffd5bd-7185-45de-9a36-3b5a9609a175" />

<img width="307" height="211" alt="image" src="https://github.com/user-attachments/assets/561bcd0f-f9a4-4bd1-aeab-5de71dd751e6" />
