# Panduan Membuat Database Pengeluaran Bulan Ini dengan MariaDB

## 1. Membuat Database

Setelah login ke MariaDB, mari kita buat database baru. Database ini akan menjadi rumah bagi tabel-tabel pengeluaran keuangan Anda.

```sql
CREATE DATABASE pengeluaran_harian;
```

Dengan perintah ini, MariaDB akan membuat database kosong bernama `pengeluaran_harian`. Database ini belum memiliki tabel, tetapi sudah siap menampung data keuangan. 

Setelah membuat database, jangan lupa untuk memilihnya:

```sql
USE pengeluaran_harian;
```

Perintah ini memberitahu MariaDB bahwa semua instruksi berikutnya akan dijalankan di database `pengeluaran_harian`. Tanpa langkah ini, tabel yang Anda buat bisa tersimpan di tempat lain.

> **💡 Tips:** Selalu pastikan database sudah dipilih sebelum melanjutkan pembuatan tabel.

---

## 2. Opsi Tambahan CREATE DATABASE

MariaDB menyediakan beberapa opsi tambahan untuk `CREATE DATABASE`. Salah satunya adalah menentukan karakter set dengan `DEFAULT CHARACTER SET utf8mb4`.

```sql
CREATE DATABASE keuangan_pribadi
DEFAULT CHARACTER SET utf8mb4
COLLATE utf8mb4_general_ci;
```

**Keuntungan menggunakan UTF-8:**
- Mendukung karakter khusus dan emoji
- Standar internasional untuk pengkodean teks
- Kompatibel dengan aplikasi modern

---

## 3. Verifikasi Database

### 3.1 Melihat Semua Database

```sql
SHOW DATABASES;
```

Perintah ini akan menampilkan daftar semua database dalam server MariaDB. Pastikan `pengeluaran_harian` atau `keuangan_pribadi` muncul dalam daftar tersebut.

### 3.2 Memeriksa Database Aktif

```sql
SELECT DATABASE();
```

Jika hasilnya adalah `pengeluaran_harian`, artinya Anda sedang bekerja di database yang tepat.

---

## 4. Membuat Tabel Transaksi

Perintah `CREATE TABLE` digunakan untuk membuat struktur penyimpanan data pengeluaran.

```sql
CREATE TABLE transaksi (
    id_transaksi INT PRIMARY KEY AUTO_INCREMENT,
    tanggal DATE NOT NULL,
    kategori VARCHAR(100) NOT NULL,
    jumlah DECIMAL(10,2) NOT NULL,
    keterangan VARCHAR(200)
);
```

### 4.1 Penjelasan Kolom:

| Kolom | Tipe Data | Deskripsi |
|-------|-----------|-----------|
| `id_transaksi` | INT | ID unik untuk setiap transaksi (auto increment) |
| `tanggal` | DATE | Tanggal transaksi (format: YYYY-MM-DD) |
| `kategori` | VARCHAR(100) | Kategori pengeluaran (bensin, makan, dll) |
| `jumlah` | DECIMAL(10,2) | Jumlah uang yang dikeluarkan |
| `keterangan` | VARCHAR(200) | Catatan tambahan (opsional) |

---

## 5. Mengisi Data Pengeluaran

### 5.1 Data Tanggal 10 Oktober 2026

```sql
INSERT INTO transaksi (tanggal, kategori, jumlah, keterangan) VALUES
('2026-10-10', 'Bensin', 40000.00, 'Isi bensin motor'),
('2026-10-10', 'Makan', 15000.00, 'Makan siang');
```

### Data Tanggal 11 Oktober 2026

```sql
INSERT INTO transaksi (tanggal, kategori, jumlah, keterangan) VALUES
('2026-10-11', 'Bengkel', 10000.00, 'Mengencangkan stang'),
('2026-10-11', 'Makan', 25000.00, 'Isi bensin motor');
```

---

## Query Laporan

### Melihat Semua Transaksi

```sql
SELECT * FROM transaksi 
ORDER BY tanggal, id_transaksi;
```

### Total Pengeluaran Per Tanggal

```sql
SELECT 
    tanggal, 
    SUM(jumlah) as total_pengeluaran 
FROM transaksi 
GROUP BY tanggal
ORDER BY tanggal;
```

### Total Pengeluaran Per Kategori

```sql
SELECT 
    kategori, 
    SUM(jumlah) as total,
    COUNT(*) as jumlah_transaksi
FROM transaksi 
GROUP BY kategori 
ORDER BY total DESC;
```

### Total Pengeluaran Bulan Ini

```sql
SELECT 
    SUM(jumlah) as total_bulan_ini
FROM transaksi
WHERE MONTH(tanggal) = MONTH(CURDATE())
  AND YEAR(tanggal) = YEAR(CURDATE());
```

### Pengeluaran Tertinggi

```sql
SELECT * FROM transaksi
ORDER BY jumlah DESC
LIMIT 5;
```

---

## Contoh Output

Setelah mengisi data, hasil query akan tampak seperti ini:

| id_transaksi | tanggal | kategori | jumlah | keterangan |
|--------------|---------|----------|--------|------------|
| 1 | 2026-10-10 | Bensin | 40000.00 | Isi bensin motor |
| 2 | 2026-10-10 | Makan | 15000.00 | Makan siang |
| 3 | 2026-10-11 | Bengkel | 10000.00 | Mengencangkan stang |
| 4 | 2026-10-11 | Bensin | 20000.00 | Isi bensin motor |


---

## Tips Tambahan

1. **Backup Database Secara Berkala**
   ```bash
   mysqldump -u username -p pengeluaran_harian > backup.sql
   ```

2. **Menambah Kolom Baru**
   ```sql
   ALTER TABLE transaksi ADD COLUMN metode_pembayaran VARCHAR(50);
   ```

3. **Menghapus Transaksi Tertentu**
   ```sql
   DELETE FROM transaksi WHERE id_transaksi = 1;
   ```

4. **Update Data**
   ```sql
   UPDATE transaksi 
   SET jumlah = 45000.00 
   WHERE id_transaksi = 1;
   ```

---
