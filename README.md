# Data Wilayah Indonesia (CSV)

Repositori ini menyediakan database wilayah administrasi Indonesia yang lengkap, mulai dari tingkat Provinsi hingga Kelurahan/Desa. Data ini sudah dinormalisasi dan saling berelasi, sehingga memudahkan pengembang untuk mengintegrasikannya ke dalam aplikasi atau database SQL.

## 📊 Statistik Data
* **Total Baris:** 81.248 data
* **Provinsi:** 34
* **Kabupaten/Kota:** 480
* **Kecamatan:** 6.994
* **Kelurahan/Desa:** 81.248

## 🗂️ Struktur Tabel & Field

### 1. `tbl_provinsi`
Menyimpan data tingkat provinsi beserta ibukota dan singkatan resminya.
* `id`: ID unik provinsi.
* `provinsi`: Nama lengkap provinsi.
* `ibukota`: Ibukota provinsi.
* `p_bsni`: Singkatan provinsi standar BSNI.

### 2. `tbl_kabkot`
Menyimpan data tingkat kabupaten dan kota.
* `id`: ID unik kabupaten/kota.
* `provinsi_id`: Relasi ke `tbl_provinsi(id)`.
* `kabupaten_kota`: Nama kabupaten atau kota.
* `ibukota`: Ibukota kabupaten/kota.
* `k_bsni`: Singkatan kabupaten/kota standar BSNI.

### 3. `tbl_kecamatan`
Menyimpan data tingkat kecamatan.
* `id`: ID unik kecamatan.
* `kabkot_id`: Relasi ke `tbl_kabkot(id)`.
* `kecamatan`: Nama kecamatan.

### 4. `tbl_kelurahan`
Menyimpan data tingkat kelurahan/desa beserta kode pos.
* `id`: ID unik kelurahan.
* `kecamatan_id`: Relasi ke `tbl_kecamatan(id)`.
* `kelurahan`: Nama kelurahan/desa.
* `kd_pos`: Kode pos wilayah.

---

## 🚀 Cara Penggunaan

### Contoh Join SQL
Untuk mendapatkan alamat lengkap dalam satu baris query:

```sql
SELECT 
    kel.kelurahan, kel.kd_pos, kec.kecamatan, kab.kabupaten_kota, prov.provinsi
FROM tbl_kelurahan kel
JOIN tbl_kecamatan kec ON kel.kecamatan_id = kec.id
JOIN tbl_kabkot kab ON kec.kabkot_id = kab.id
JOIN tbl_provinsi prov ON kab.provinsi_id = prov.id;
