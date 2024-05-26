# Purwadhika-Project-Module-3---Bank-Campaign

Pada Project ini akan membahas Data Analysis yang bersumber dari Data Bank Marketing Campaign, [link] https://drive.google.com/drive/folders/1RbARQXmF64lrOV-RSBhLa5vKk0vBVMEf.

Secara garis besar, Project ini berisikan :
1. Business Problem Understanding
2. Data Understanding
3. Data Cleaning
4. Data Preparation & Feature Engineering
5. Modeling & Evaluation
6. Prediction : Pickle
7. Conclusion & Recomendation

## 1. Business Problem Understanding

Context <br>
Berikut ini adalah kumpulan data yang menggambarkan hasil kampanye pemasaran bank. Kampanye yang dilakukan sebagian besar didasarkan pada panggilan telepon langsung, menawarkan klien bank untuk menempatkan deposito berjangka. Jika setelah semua upaya penandaan klien telah setuju untuk menempatkan deposit - variabel target ditandai 'ya', jika tidak 'tidak'.

Target : <br>
Tidak (0) : Tidak menempatkan deposit. <br>
Ya (1) : Menempatkan deposit.

**Problem Statement :**

Proses kampanye pemasaran bank memakan waktu dan sumber daya jika bank menargetkan semua nasabah tanpa melakukan penyaringan terlebih dahulu. Bank ingin meningkatkan efisiensi kampanye dengan mengetahui kandidat mana yang akan menempatkan depositnya ke bank.

Jika kampanye yang dilakukan kepada semua calon/kandidat depositor, maka waktu dan biaya tersebut akan sia-sia jika calon depositor tersebut tidak mau menempatkan uangnya di bank.

**Goals :**

Maka berdasarkan permasalahan tersebut, bank ingin memiliki kemampuan untuk memprediksi kemungkinan seorang kandidat akan/ingin menempatkan depositnya atau tidak, sehingga dapat memfokuskan kampanye pada kandidat yang bersedia menempatkan deposit ke bank.

Dan juga, perusahaan ingin mengetahui apa/faktor/variabel apa yang membuat seorang kandidat mau menempatkan deposito atau tidak, sehingga mereka dapat membuat rencana yang lebih baik dalam mendekati kandidat potensial (kandidat yang ingin menempatkan depostionya).

**Analytic Approach :**

Jadi yang akan kita lakukan adalah menganalisis data untuk menemukan pola yang membedakan kandidat yang mau menempatkan deposito atau tidak.

Kemudian kita akan membangun model klasifikasi yang akan membantu bank untuk dapat memprediksi probabilitas seorang kandidat akan/ingin menempatkan deposito atau tidak.

**Metric Evaluation**

Type 1 error : False Positive  
Konsekuensi: sia-sianya biaya kampanye, waktu dan sumber daya

Type 2 error : False Negative  
Konsekuensi: kehilangan calon depositor

Berdasarkan konsekuensinya, maka sebisa mungkin yang akan kita lakukan adalah membuat model yang dapat mengurangi cost kampanye dari bank tersebut, tetapi tanpa membuat menjadi kurangnya/tidak cukup kandidat depositor yang dibutuhkan bank. Jadi harus kita seimbangkan nanti antara precision dan recallnya dari kelas positive (kandidat depositor). Jadi nanti metric utama yang akan kita gunakan adalah roc_auc.

## 2. Data Understanding

Note : <br>
- Sebagian besar fitur bersifat kategori (Nominal, Ordinal, Binary)
- Setiap baris data merepresentasikan informasi seorang customer yang pernah dilakukan bank campaign di masa lalu

### Attribute Information

| Atribut/Feature | Tipe Data | Deskripsi |
| --- | --- | --- |
| age | numeric | Umur customer
| job | categorical | Tipe-tipe job
| balance | numeric | Rata-rata balance tahunan |
| housing | binary | Memiliki cicilan rumah
| loan | binary | Memiliki hutang personal
| contact | categorical | Tipe kontak komunikasi
| month | categorical | Kontak terakir dalam setahun
| campaign | numeric | Jumlah kontak yang dilakukan selama kampanye
| pdays | numeric | Jumlah hari berlalu setelah customer terakhir dihubungi dari kammpanye sebelumnya
| poutcome | categorical | Hasil dari kampanye pemasaran sebelumnya
| deposit | binary | customer berlangganan deposit berjangka

## 3. Data Cleaning

Tidak ada data yang hilang/kosong, semua feature bisa digunakan dan siap pakai untuk melakukan analisa terhadap masalah dan juga pembuatan model machine learningnya.

Data tipe yang ada susah sesuai dengan featurenya, jadi tidak perlu merubah tipe data, dan lanjut ke tahap Analisa Datanya untuk keperluan masalah yang dihadapi.

## Data Analysis

Berdasarkan plot yang dibuat, dapat kita simpulkan bahwa :

1. Pesebaran data customer yang deposit atau tidak seimbang, jadi tidak diperlukan handling imbalance
2. Usia customer yang melakukan deposit atau tidak yakni sama, sekitar di rentang 40 tahunan
3. Pada grafik Deposit vs Balance, terdapat outliers baik pada customer yang melakukan deposit atau tidak, namun disini tidak akan dihapus untuk outliersnya, dikarenakan terlalu banyak jumlahnya. 

## 4. Data Preparation & Feature Engineering

Sekarang mari kita melakukan fitur encoding untuk fitur-fitur categorical yang kita miliki.
Yang akan kita lakukan adalah :

1. Merubah fitur/kolom `job` menggunakan One Hot Encoding, karena fitur ini tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit.

2. Merubah fitur/kolom `housing` menggunakan One Hot Encoding, karena fitur ini tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit.

3. Merubah fitur/kolom `loan` menggunakan One Hot Encoding, karena fitur ini tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit.

4. Merubah fitur/kolom `contact` menggunakan One Hot Encoding, karena fitur ini tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit.

5. Merubah fitur/kolom `month` menggunakan One Hot Encoding, karena fitur ini tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit.

6. Merubah fitur/kolom `poutcome` menggunakan One Hot Encoding, karena fitur ini tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit.

## 5. Modelling & Evaluation

Terlihat bahwa model Random Forest adalah yang terbaik untuk roc_aucnya dari setiap model yang menggunakan default hyperparameter.

## 6. Prediction : Pickle

Dikarenakan model yang dibuat adalah Random Forest, maka pickle dilakukan compress menggunakan zipx untuk mengkompresi pickle yang ukruran file nya lebih dari 25Mb (yang mana limitasi dari github).

## 7. Conclusion & Recommendation

Berdasarkan hasil classification report dari model kita, kita dapat menyimpulkan/mengambil konklusi bahwa bila seandainya nanti kita menggunakan model kita untuk memfilter/menyaring list customer yang akan kita coba tawarkan, maka model kita dapat mengurangi 74% customer yang tidak tertarik untuk tidak kita approach, dan model kita dapat mendapatkan 65% customer yang tertarik dari seluruh customer yang tertarik melakukan deposit. (semua ini berdasarkan recallnya)

Model kita ini memiliki ketepatan prediksi customer yang tertarik melakukan deposito sebesar 70% (precisionnya), jadi setiap model kita memprediksi bahwa seorang customer itu tertarik, maka kemungkinan tebakannya benar itu sebesar 70% kurang lebih. Maka masih akan ada customer yang sebenarnya tidak tertarik tetapi diprediksi sebagai customer yang tertarik sekitar 26% dari keseluruhan kandidat yang tidak tertarik (berdasarkan recall).

Berdasarkan analisa tersebut, terlihat bahwa dengan menggunakan model kita, maka bank bisa menghemat biaya yang cukup besar tanpa mengorbankan terlalu banyak jumlah customer potensial yg tertarik.

#### Recommendation

Hal-hal yang bisa dilakukan untuk mengembangkan project dan modelnya lebih baik lagi :

- Memperbaiki modelling dari sebelumnya atau melakukan improvement dari model yang sudah dibuat.
- Menambahkan fitur2 atau kolom2 baru yang kemungkinan bisa berhubungan dengan ketertarikannya, seperti status perkawinan, tingkat edukasi, dan lainnya.
- Mencoba algorithm ML yang lain dan juga mencoba hyperparameter tuning kembali.
- Menganalisa data-data yang model kita masih salah tebak untuk mengetahui alasannya dan karakteristiknya bagaimana.
