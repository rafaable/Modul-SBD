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
  "nama_lengkap": "Indah Permata",
  "kartu_identitas": "3273012345678456",
  "nomor_sim": "950112345456",
  "tanggal_kadaluarsa_sim": "2032-06-13",
  "nomor_telepon": "081234567999",
  "status_verifikasi": "terverifikasi"
}
```
12. Kedaluarsa SIM per hari ini
```
{
  "nama_lengkap": "Shin Yuna",
  "kartu_identitas": "3273012345678400",
  "nomor_sim": "950112345499",
  "tanggal_kadaluarsa_sim": "2028-06-13",   -- tanggalnya diganti
  "nomor_telepon": "081234567987",
  "status_verifikasi": "terverifikasi"
}
```


