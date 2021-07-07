# Titanic Survivability Prediction
Prediksi mengenai keselamatan penumpang dari tenggelamnya kapal titanic dengan beberapa faktor tertentu berdasarkan dataset titanic.

## Dataset
Dari dataset yang kita miliki kita memiliki data dari 891 penumpang dengan informasi sebagai berikut:
1. sex = jenis kelamin penumpang
2. age = umur penumpang
3. parch = jumlah orang tua / anak yang ikut didalam kapal titanic
4. fare = harga tiket
5. class = kelas penumpang berada
6. deck = deck penumpang berada
7. embark_town = kota asal
8. alive = berhasil selamat atau tidak
9. alone = berada dikapal sendirian atau tidak

## Data Analysis
Kita perlu menganalisa data untuk menentukan feature apa saja yang akan digunakan didalam model yang akan dibuat.
Salah satu cara untuk menentukan feature yang bisa digunakan bisa dengan melihat korelasi atau hubungan diantara variabel feature dengan variabel labelnya.
Dapat dimulai dengan memisahkan tipe datanya antara numeric dan categorical:

### 1. Hubungan antara Data Numeric dan Survivability
Survivability dalam dataset ini adalah data `alive`, karena data `alive` masih dalam bentuk categorical kita akan membuat 1 kolom baru yang bernama `is_alive` berisi hasil mapping data `alive` menjadi data numeric. 
Data numeric dalam dataset ini adalah : age, parch,	fare & alone
Karena ada minimal satu dari data diatas yang memiliki distribusi tidak normal, maka kita akan menggunakan metode 'spearman' untuk mengecek korelasi

