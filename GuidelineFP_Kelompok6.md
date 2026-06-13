# Github
Bisa di powershell windows btw
### Baru bikin pertama kali
Masuk ke folder tempat kamu mau nyimpen file backendnya, misal:
```
cd Documents        # atau folder mana saja yang kamu mau
```
Clone repo
```
git clone https://github.com/rafaable/Backend_RentalMotor.git
```
Masuk dulu ke folder baru yang udah di-clone!
```
cd Backend_RentalMotor
```
Kalau udah masuk, ketik ini buat masuk terminal vscode langsung
```
code .
```
### Sebelumnya udah clone
Kalau sebelumnya udah clone dan **jaga jaga kalau beberapa file di github ada perubahan**, kalian bisa pull dulu TAPI pastikan kalian sudah masuk folder backendnya, misal:
```
cd path/ke/Backend_RentalMotor
```
Baru pull
```
git pull origin main
code .
```
### Prosedur push
Ini buat cek dulu, setelah kamu ngerjain tuh yang berubah apa aja
```
git status
```
1. Case mau push semua perubahan (tapi koordinasi dulu kalau pas cek git status, file bagian anggota lain ikut keubah)
   ```
   git add .
   git commit -m "nambahin atau ngubah apa gitu misal"
   git push origin main
   ```
2. Push folder tertentu saja:
   ```
   git add nama-folder/
   git commit -m "update folder ini"
   git push origin main
   ```
3. Push file tertentu saja:
   ```
   git add folder/nama-file.py
   git commit -m "update file ini"
   git push origin main
   ```
# Step by step

- Pastikan python & git udah terlihat, cirinya kalau buka CMD
   ```
   python --version
   git --version
   ```
   Muncul versi python & gitnya. Kalau belum, install dulu  
- Buka VSCode pakai command ini
  ```
  code .
  ```
- Ok sekarang pindah terminal VSCode, jalanin virtual environment
  ```
  python -m venv venv
  ```
- Terus pindah ke command prompt, masuk dulu ke foldernya terus jalanin ini
  **TIAP BUKA ULANG PROJECT HARUS JALANIN INI**
  ```
  cd Backend_RentalMotor
  venv\Scripts\activate
  ```
  Kalau berhasil muncul gini
  > (venv) C:\...
- Install semua library
  ```
  pip install fastapi uvicorn pymysql pymongo python-dotenv pydantic
  ```
- Di terminal VSCode
  ```
  pip freeze > requirements.txt
  ```
- Buat file .env yang isinya begini
  ```
   MYSQL_HOST=localhost
   MYSQL_PORT=3306           -- bagian ini disesuaikan!
   MYSQL_USER=root
   MYSQL_PASSWORD=
   MYSQL_DB=rental_motor

   MONGO_URI=mongodb://localhost:27017
   MONGO_DB=rental_motor
  ```
  Bagian mySQL port lihat di XAMPP kalian,
  sesuaikan isi baris MySQL dan kolom port  
  lain lainnya harusnya sama sih
  terus install dotenv
  ```
  npm install dotenv
  ```
  Kalau nggak bisa, coba salah satu dari ini
  ```
  yarn add dotenv
  pnpm add dotenv
  ```
- Jalanin ini di terminal vscode
  ```
  uvicorn app.main:app --reload
  ```
  terus salin ini di halaman browser mana aja
  ```
  http://127.0.0.1:8000/docs#/
  ```

