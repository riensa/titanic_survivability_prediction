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

<p align="center">
  <img src="https://raw.githubusercontent.com/riensa/titanic_survivability_prediction/main/images/Screen%20Shot%202021-07-07%20at%205.10.52%20PM.png" width="350" >
</p>

Berdasarkan heatmap diatas dapat disimpulkan bahwa nilai korelasi antara is_alive dengan age, parch dan alone berada dibawah 0.3 yang berarti nilai korelasinya rendah, maka ketiga fitur tersebut tidak akan digunakan dalam model.

### 2. Hubungan antara Data Categorical dan Survivability
Kita dapat menggunakan chi2_contingency untuk melihat apakah ada hubungan diantara data alive dengan sex, class, deck dan embark_town.
Berdasarkan hasil uji test, dapat kita simpulkan bahwa tidak Ada keterkaitan antara deck dan alive maka kita bisa tidak menggunakan fitur tersebut dalam model

### 3. Missing Value
Hingga saat ini kita sudah memilih feature yang akan kita gunakan didalam model yaitu fare, sex, class dan embark_town.
Kita perlu mengecek terlebih dahulu apakah ada missing value diantara 4 feature tersebut.
Setelah dicek, ternyata terdapat missing value pada feature embark_town, karena embark_town merupakan data categorical nominal kita dapat menggunakan modus (data yang muncul paling banyak) untuk mengganti missing value tersebut

## Preprocessing
karena model hanya menerima angka numerik, maka kita perlu mengubah semua fitur yang sudah kita pilih tersebut menjadi angka numerik
### 1. class
class merupakan data categorical dengan tipe ordinal, maka kita akan menggunakan **Category Encoders Library** untuk mengubah data tersebut menjadi numerik

### 2. sex & embark_town
sex & embark_town merupakan data categorical dengan tipe nominal, maka kita akan menggunakan **One Hot Encoding** untuk mengubah data tersebut menjadi numerik

### 3. fare
fare adalah angka numerik yang memiliki banyak outlier, maka kita bisa scaling datanya dengan menggunakan **Robust Scaler**

## Splitting & Transform Data
Dari dataset yang sudah dipreprocessing, kita dapat membagi data tersebut menjadi train dataset & test dataset dengan perbandingan 70:30

## Model Fitting & Evaluation
Kita menggunakan dataset hasil preprocessing tersebut kedalam 3 model yang berbeda, yaitu

1. Logistic Regression dengan Nilai Akurasi : 0.8251121076233184
2. KNN Classifier dengan Nilai Akurasi : 0.8295964125560538
3. Decision Tree dengan Nilai Akurasi : 0.8251121076233184

Dari 3 model tersebut, nilai akurasi kurang lebih sama berada di sekitar 82% dengan KNN Classifier memiliki nilai akurasi paling tinggi yaitu sekitar 82.96%
