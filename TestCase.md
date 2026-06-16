# Pengguna
## GET
1. Get semua pengguna berhasil
2. Data pengguna kosong
3. ID tidak ditemukan
4. Nama lengkap tidak ditemukan
5. Tahun kadaluarsa SIM tidak ditemukan
6. Rentang tahun kadaluarsa SIM tidak ditemukan
7. Rentang tahun kadaluarsa SIM tidak valid
8. Status verifikasi tidak ditemukan
9. Tahun kadaluarsa SIM bukan angka
10. Filter gabungan tidak ditemukan

## POST
1. Sukses Input
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
2. Informasi kurang lengkap
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
3. Kartu identitas duplikat
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3515011203000001",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
4. Nomor SIM duplikat
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "980512345681",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
5. Format SIM Bukan Angka
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "9501123451xx",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
6. Kartu identitas kurang 16 digit
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "32730123456783",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
7. Nama lengkap hanya berisi spasi
```
{
  "nama_lengkap": "  ",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
8. Panjang nomor telepon tidak valid
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081",
  "status_verifikasi": "terverifikasi"
}
```
9. Nomor telepon mengandung karakter
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567nn90",
  "status_verifikasi": "terverifikasi"
}
```
10. Status verifikasi tidak sesuai ENUM
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2029-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "aktif"
}
```
11. Kedaluarsa SIM lebih dari 5 tahun
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "tanggal_kadaluarsa_sim": "2032-06-13",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```
12. Kedaluarsa SIM per hari ini
```
{
  "nama_lengkap": "Dani Agastya",
  "kartu_identitas": "3273012345678456",
  "nomor_sim": "950112345456",
  "tanggal_kadaluarsa_sim": "2029-06-13",   --- diubah
  "nomor_telepon": "08123456786958",
  "status_verifikasi": "terverifikasi"
}
```
## PATCH

1. Sukses Update Semua Field Pengguna

```json
{
  "kartu_identitas": "3515011203000099",
  "nomor_telepon": "081299998888",
  "nama_lengkap": "Aksa Sadajiwa Update",
  "nomor_sim": "950112345999",
  "tanggal_kadaluarsa_sim": "2029-05-20",
  "status_verifikasi": "terverifikasi"
}

```

2. Sukses Update Hanya Field Tertentu (Misal: Nomor Telepon Saja)

```json
{
  "nomor_telepon": "081211112222"
}

```

3. ID Pengguna Tidak Ditemukan di Database (Error ID not found)

```json
// URL: /pengguna/999 (ID tidak terdaftar)
{
  "nama_lengkap": "Rian Sanjaya"
}

```

4. Mengirim Field id_pengguna di dalam Body JSON (Field tidak valid untuk diupdate)

```json
{
  "id_pengguna": 1,
  "nama_lengkap": "Rian Sanjaya"
}

```

5. Kartu Identitas Sudah Terdaftar / Duplikat (Gagal karena batasan UNIQUE)

```json
{
  "kartu_identitas": "3515011507010002"
}

```

6. Nomor SIM Sudah Terdaftar / Duplikat (Gagal karena batasan UNIQUE)

```json
{
  "nomor_sim": "960712345679"
}

```

7. Nama Lengkap Tidak Valid atau Hanya Berisi Spasi Empty String

```json
{
  "nama_lengkap": "   "
}

```

8. Nomor Telepon Tidak Valid atau Hanya Berisi Spasi Empty String

```json
{
  "nomor_telepon": ""
}

```

9. Format Tanggal Kadaluarsa SIM Tidak Valid (Bukan format YYYY-MM-DD)

```json
{
  "tanggal_kadaluarsa_sim": "12-03-2028"
}

```

10. Status Verifikasi Tidak Valid / Di Luar ENUM yang Ditentukan

```json
{
  "status_verifikasi": "akun_palsu"
}

```
## DELETE

1. Sukses hapus pengguna (ID ditemukan dan tidak memiliki relasi di tabel lain)
2. ID pengguna tidak ditemukan (`"message": "Not found"`)
3. Gagal hapus karena pengguna memiliki riwayat transaksi di tabel penyewaan (`"message": "Failed : Memiliki entri di tabel lain"`)
4. ID pengguna bukan angka / *invalid integer* (Memicu error validasi tipe data FastAPI Pydantic)
5. ID pengguna kosong atau tidak dimasukkan pada path parameter URL
# Cabang
## GET
1. Get semua cabang berhasil (tanpa menggunakan filter query parameter)
2. Get cabang berdasarkan ID berhasil ditemukan
3. Get cabang berdasarkan Kota berhasil ditemukan
4. Get cabang dengan filter gabungan (ID dan Kota) berhasil ditemukan
5. ID tidak ditemukan (`"message": "id not found"` ketika `id_cabang` diisi tapi tidak ada di database)
6. Kota tidak ditemukan (`"message": "Not found!"` ketika nama `kota` diisi tapi tidak ada di database)
7. Filter gabungan tidak ditemukan (ketika ID ada tetapi Kota tidak sesuai, atau sebaliknya)
8. Data cabang kosong (`"message": "data pengguna kosong"` ketika seluruh tabel cabang tidak memiliki *record* sama sekali)
9. Validasi tipe data ID cabang bukan angka / *invalid integer* (menyebabkan error validasi FastAPI Pydantic sebelum masuk ke query database)
   
## POST
1. Sukses Input Cabang Baru
```json
{
  "nama_cabang": "MLG",
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "Malang"
}

```

2. Informasi kurang lengkap (salah satu field tidak dikirim/`null`)
```json
{
  "nama_cabang": "MLG",
  "alamat": "Jl. Ijen No. 10, Klojen"
}

```

3. Field nama_cabang hanya berisi spasi atau kosong (`""`)
```json
{
  "nama_cabang": "   ",
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "Malang"
}

```

4. Field alamat hanya berisi spasi atau kosong (`""`)
```json
{
  "nama_cabang": "MLG",
  "alamat": "",
  "kota": "Malang"
}

```

5. Field kota hanya berisi spasi atau kosong (`""`)
```json
{
  "nama_cabang": "MLG",
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "   "
}

```

6. Nama cabang di kota tersebut sudah terdaftar (Cek Duplikat Kombinasi Nama + Kota)
```json
{
  "nama_cabang": "SDJ",
  "alamat": "Jl. Berbeda No. 99, Sidoarjo",
  "kota": "Sidoarjo"
}

```

7. Sukses Input dengan Nama Cabang sama tapi di Kota yang berbeda
```json
{
  "nama_cabang": "SDJ",
  "alamat": "Jl. Pahlawan No. 2, Genteng",
  "kota": "Surabaya"
}

```

8. Validasi tipe data input tidak valid (misal mengirim angka pada field string, memicu error internal FastAPI/Pydantic)

```json
{
  "nama_cabang": 123,
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "Malang"
}

```

## PATCH

1. Sukses Update Semua Field Cabang

```json
{
  "nama_cabang": "SDJ BARU",
  "alamat": "Jl. Gajah Mada No. 100, Sidoarjo",
  "kota": "Sidoarjo"
}

```

2. Sukses Update Hanya Field Tertentu (Misal: Alamat Saja)

```json
{
  "alamat": "Jl. Raya Delta No. 55, Sidoarjo"
}

```

3. ID Cabang Tidak Ditemukan (`"message": "ID not found"`)

```json
// URL: /cabang/999 (ID tidak terdaftar di database)
{
  "nama_cabang": "SBY REVO"
}

```

4. Mengirim Field id_cabang di dalam Body JSON (`"message": "field tidak valid"`)

```json
{
  "id_cabang": 1,
  "nama_cabang": "SBY REVO"
}

```

5. Mengirim Field Tidak Valid / Di Luar Skema (`"message": "field tidak valid"`)

```json
{
  "nama_cabang": "SBY REVO",
  "karyawan_baru": "Budi"
}

```

6. Nama Cabang Tidak Valid / Hanya Spasi (`"message": "Nama cabang tidak valid!"`)

```json
{
  "nama_cabang": "   "
}

```

7. Alamat Tidak Valid / Hanya Spasi (`"message": "Alamat tidak valid!"`)

```json
{
  "alamat": ""
}

```

8. Kota Tidak Valid / Hanya Spasi (`"message": "Kota tidak valid!"`)

```json
{
  "kota": "   "
}

```

9. Nama Kota Terlalu Panjang / Lebih dari 50 Karakter (`"message": "Nama kota terlalu panjang!"`)

```json
{
  "kota": "Kota Metropolitan Surabaya Bagian Barat Selatan Timur Raya"
}

```
## DELETE

1. Sukses hapus cabang (ID ditemukan, serta tidak memiliki relasi di tabel karyawan maupun kendaraan)
2. ID cabang tidak ditemukan (`"message": "ID not found"`)
3. Gagal hapus karena cabang masih memiliki relasi di tabel karyawan (`"message": "Tidak bisa hapus cabang, masih ada karyawan terkait!"`)
4. Gagal hapus karena cabang masih memiliki relasi di tabel kendaraan (`"message": "Tidak bisa hapus cabang, masih ada kendaraan terkait!"`)
5. ID cabang bukan angka / *invalid integer* (Memicu error validasi tipe data FastAPI Pydantic)
6. ID cabang kosong atau tidak dimasukkan pada path parameter URL
