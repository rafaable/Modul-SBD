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
Sukses Input
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
Informasi kurang lengkap
```
{
  "nama_lengkap": "Rian Sanjaya",
  "kartu_identitas": "3273012345678123",
  "nomor_sim": "950112345123",
  "nomor_telepon": "081234567890",
  "status_verifikasi": "terverifikasi"
}
```

Nomor SIM duplikat
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

Format SIM Bukan Angka
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

Kartu identitas kurang 16 digit
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

Nama lengkap hanya berisi spasi
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

Panjang nomor telepon tidak valid
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

Nomor telepon mengandung karakter
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

Status verifikasi tidak sesuai ENUM
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

Kedaluarsa SIM lebih dari 5 tahun
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

Kedaluarsa SIM per hari ini
```
{
  "nama_lengkap": "Dani Agastya",
  "kartu_identitas": "3273012345678456",
  "nomor_sim": "950112345456",
  "tanggal_kadaluarsa_sim": "2029-06-13",  
  "nomor_telepon": "08123456786958",
  "status_verifikasi": "terverifikasi"
}
```
## PATCH

Sukses Update Semua Field Pengguna
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

Update Field Tertentu
```json
{
  "nomor_telepon": "081211112222"
}

```

ID Pengguna Tidak Ditemukan di Database (Error ID not found)
```json
// URL: /pengguna/999 (ID tidak terdaftar)
{
  "nama_lengkap": "Rian Sanjaya"
}

```

Kartu Identitas Duplikat
```json
{
  "kartu_identitas": "3515011507010002"
}

```

Nomor SIM Duplikat
```json
{
  "nomor_sim": "960712345679"
}

```

Nama Lengkap tidak Valid / Empty String
```json
{
  "nama_lengkap": "   "
}

```

Nomor Telepon Tidak Valid / Empty String
```json
{
  "nomor_telepon": ""
}

```

Format Tanggal Salah
```json
{
  "tanggal_kadaluarsa_sim": "12-03-2028"
}

```

Status Verifikasi Tidak Valid / Di Luar ENUM
```json
{
  "status_verifikasi": "akun_palsu"
}

```
## DELETE

- Sukses hapus pengguna (ID ditemukan dan tidak memiliki relasi di tabel lain)
- ID pengguna tidak ditemukan 
- Gagal hapus karena pengguna memiliki riwayat transaksi di tabel penyewaan (`"message": "Failed : Memiliki entri di tabel lain"`)
- ID pengguna invalid integer
- ID pengguna kosong atau tidak dimasukkan pada path parameter URL
  
# Cabang
## GET
- Get all tanpa filter
- Get cabang berdasarkan ID
- Get cabang berdasarkan Kota %like%
- Get cabang filter gabungan
- ID tidak ditemukan 
- Kota tidak ditemukan
- Filter gabungan tidak ditemukan 
- ID cabang bukan angka
   
## POST
Sukses Input Cabang Baru
```json
{
  "nama_cabang": "MLG",
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "Malang"
}

```

Field kurang lengkap 
```json
{
  "nama_cabang": "MLG",
  "alamat": "Jl. Ijen No. 10, Klojen"
}

```

Field nama_cabang hanya berisi spasi atau kosong (`""`)
```json
{
  "nama_cabang": "   ",
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "Malang"
}

```

Field alamat hanya berisi spasi atau kosong (`""`)
```json
{
  "nama_cabang": "MLG",
  "alamat": "",
  "kota": "Malang"
}

```

Field kota hanya berisi spasi atau kosong (`""`)
```json
{
  "nama_cabang": "MLG",
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "   "
}

```

Nama cabang di kota tersebut sudah terdaftar
```json
{
  "nama_cabang": "SDJ",
  "alamat": "Jl. Berbeda No. 99, Sidoarjo",
  "kota": "Sidoarjo"
}

```

Nama Cabang sama tapi di Kota yang berbeda
```json
{
  "nama_cabang": "SDJ",
  "alamat": "Jl. Pahlawan No. 2, Genteng",
  "kota": "Surabaya"
}

```

Tipe data input tidak valid
```json
{
  "nama_cabang": 123,
  "alamat": "Jl. Ijen No. 10, Klojen",
  "kota": "Malang"
}

```

## PATCH
Sukses Update Semua Field Cabang
```json
{
  "nama_cabang": "SDJ BARU",
  "alamat": "Jl. Gajah Mada No. 100, Sidoarjo",
  "kota": "Sidoarjo"
}

```

Update Field Tertentu 
```json
{
  "alamat": "Jl. Raya Delta No. 55, Sidoarjo"
}

```

ID Cabang Tidak Ditemukan
```json
Misal cabang = 99999
```

Nama Cabang Tidak Valid / Hanya Spasi
```json
{
  "nama_cabang": "   "
}

```

Alamat Tidak Valid / Hanya Spasi
```json
{
  "alamat": ""
}

```

Kota Tidak Valid / Hanya Spasi
```json
{
  "kota": "   "
}

```

Nama Kota Terlalu Panjang
```json
{
  "kota": "Kota Metropolitan Surabaya Bagian Barat Selatan Timur Raya"
}

```

## DELETE
- Sukses hapus: ID ditemukan, tidak memiliki relasi
- ID tidak ditemukan
- GCabang masih memiliki relasi di tabel lain
- ID cabang invalid integer
- ID cabang kosong

# Penyewaan
## Get
Get berhasil
* Get all tanpa filter
* Get id_pengguna = 1
* Get id_kendaraan = 2
* Get id_karyawan = 1
* Get waktu_kembali_down = 2026-06-01, waktu_kembali_up = 2026-06-15
* Get status_penyewaan = aktif
* Get id_pengguna = 99
* Get id_kendaraan = 99
* Get id_karyawan = 99
* Get waktu_kembali_down = 2026-01-01, waktu_kembali_up = 2026-01-10
* Get tanggal terbalik
* Get status_penyewaan = dibatalkan

# Post

Informasi tidak lengkap
{
  "id_pengguna": 20, -- yah tapi sesuaikan lagi
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Format tanggal salah
{
  "id_pengguna": 20, -- yah tapi sesuaikan lagi
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_mulai": "09-09-2026",
  "waktu_selesai_rencana": "09-12-2026",
  "status_penyewaan": "aktif"
}

Rentang tanggal terbalik
{
  "id_pengguna": 20, -- yah tapi sesuaikan lagi
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_mulai": "2026-09-19",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Status selain aktif
{
  "id_pengguna": 20, -- yah tapi sesuaikan lagi
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "dibatalkan"
}

Pengguna tidak terdaftar
{
  "id_pengguna": 100, 
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Pengguna tidak terverifikasi
{
  "id_pengguna": 20, -- cari id terakhir yang selain diverifikasi
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Pengguna masih memiliki penyewaan aktif
{
  "id_pengguna": 10,
  "id_kendaraan": 12,
  "id_karyawan": 9,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Kendaraan tidak tersedia
{
  "id_pengguna": 20, -- pengguna yang terverifikasi
  "id_kendaraan": 14,
  "id_karyawan": 9,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Karyawan tidak terdaftar
{
  "id_pengguna": 20, -- pengguna yang terverifikasi
  "id_kendaraan": 11,
  "id_karyawan": 90,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Karyawan & kendaraan tidak berasal dari cabang yang sama
{
  "id_pengguna": 20, -- pengguna yang terverifikasi
  "id_kendaraan": 11,
  "id_karyawan": 1,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

Ini yang berhasil
{
  "id_pengguna": 20, -- yah tapi sesuaikan lagi
  "id_kendaraan": 11,
  "id_karyawan": 1,
  "waktu_mulai": "2026-09-09",
  "waktu_selesai_rencana": "2026-09-12",
  "status_penyewaan": "aktif"
}

