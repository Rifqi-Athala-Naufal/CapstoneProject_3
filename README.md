
# Capstone Project 3

 - **Rifqi Athala Naufal**
 - **JCDSOL - 013**


# **Bank Marketing Campaign**

## Business Problem Understanding
**Context**

Jenis produk keuangan yang digunakan masyarakat semakin bervariasi. Salah satu produk keuangan yang banyak dikenal masyarakat adalah deposito berjangka. Mekanisme deposito berjangka adalah nasabah menyetorkan sejumlah uangnya ke bank atau lembaga keuangan, dan uang tersebut baru dapat ditarik setelah jangka waktu tertentu. Sebagai imbalannya, nasabah akan diberikan bunga tetap sesuai dengan jumlah nominal uang yang disetorkan.

Meski demikian, sebagai badan usaha yang memiliki produk keuangan dan nasabah masing-masing, bank tetap harus bersaing agar tidak kehilangan nasabah. Salah satu cara untuk mendapatkan nasabah baru adalah dengan melakukan kampanye pemasaran.

Target :

No (0) : Apabila nasabah tidak tertarik deposit

Yes (1) : Apabila nasabah tertarik deposit

**Problem Statement**

Proses Marketing campaign bank perlu memperkirakan waktu dan sumber daya untuk menargetkan nasabah. Apabila campaign dilakukan kepada semua nasabah, biaya dan usaha yang dikeluarkan akan sangat besar, sehingga perlu dilakukan pemilihan ke beberapa nasabah tertentu saja. Bank perlu meningkatkan efisiensi kampanye dengan mengetahui kandidat nasabah mana yang tertarik menempatkan depositnya ke bank.

**Goals**

Berdasarkan problem statement tersebut, bank perlu memiliki kemampuan untuk memprediksi kemungkinan seorang kandidat tertarik menempatkan depositnya atau tidak, sehingga campaign dapat difokuskan kepada nasabah yang tertarik untuk menempatkan deposit ke bank.

Lebih lanjut, perusahaan perlu mengetahui faktor apa saja yang dapat membuat seorang nasabah tersebut tertarik untuk menempatkan deposito, sehingga mereka dapat membuat rencana yang lebih baik dalam pendekatan penawaran produk deposito.

**Analytic Approach**

Penelitian ini akan melakukan analisa untuk menemukan pola yang membedakan kandidat yang tertarik menempatkan deposito atau tidak. Selanjutnya, model klasifikasi akan dibangun untuk membantu bank memprediksi peluang seorang nasabah tertarik menempatkan deposito atau tidak.

**Metric Evaluation**

Type 1 error : False Positive

-   Konsekuensi: sia-sianya biaya marketing campaign, waktu dan sumber daya

Type 2 error : False Negative

-   Konsekuensi: kehilangan calon nasabah

Berdasarkan konsekuensinya, maka sebisa mungkin yang akan kita lakukan adalah membuat model yang dapat mengurangi biaya marketing campaign dari bank tersebut, tetapi tanpa membuat menjadi kurangnya/tidak cukup kandidat nasabah yang dibutuhkan bank. Jadi kita ingin sebanyak mungkin prediksi kelas positif yang benar, dengan sesedikit mungkin prediksi false positive. metric utama yang akan kita gunakan adalah  `roc_auc`.

## Data Understanding

### Attribute Information
| Attribute | Data Type | Description |
| --- | --- | --- |
| age | numeric | Age of customer
| job | categorical | Type of job
| balance | numeric | Customer's account balance |
| housing | binary | Customer is having a housing loan
| loan | binary | Customer is having a personal loan
| contact | categorical | type of contact method
| month | categorical | Last contact month
| campaign | numeric | Number of contacts performed during the campaign
| pdays | numeric | Number of days passed after the prospective customer was last contacted from the previous campaign
| poutcome | categorical | Outcome of the previous campaign
| deposit | binary | "yes" if customer interested to deposit; "no" if customer not interested to deposit.

## Data Cleaning

Tidak ada data yang hilang/kosong sehingga siap dipakai untuk melakukan analisa terhadap masalah dan pembuatan model.

Tipe data yang ada susah sesuai dengan fiturnya, jadi tidak perlu merubah tipe data, dan lanjut ke tahap Analisa Datanya untuk keperluan masalah yang dihadapi.

## Data Analysis

Berdasarkan plot yang dibuat, dapat kita simpulkan bahwa :

1. Pesebaran data nasabahyang tertarik deposit dan tidak tertarik seimbang, jadi tidak diperlukan handling imbalance
2. Nasabah yang tidak memiliki  `housing`  loan cenderung memiliki potensi minat terhadap deposit yang lebih tinggi dibandingkan dengan yang memiliki  `housing`  loan.
3. Nasabah yang tidak memiliki personal  `loan`  cenderung memiliki potensi minat terhadap deposit yang lebih tinggi dibandingkan dengan yang memiliki  `loan`.
4. Usia nasabah yang tertarik deposit atau tidak tertarik memiliki rentang nilai yang sama, dengan nilai median sekitar 40 tahun.
5. Pada grafik Deposit vs Balance terdapat  _outlier_  apakah nasabah tertarik melakukan deposit atau tidak. Dalam hal ini, data  _outlier_  tidak akan dihilangkan karena jumlah datanya besar.

## Data Processing

Berdasarkan data yang kita punya, _One-hot encoding_  , teknik yang digunakan untuk mengubah variabel kategorik ke dalam format yang dapat disediakan bagi algoritma  _machine learning_  untuk melakukan pekerjaan prediksi dengan lebih baik, perlu diterapkan. Banyak algoritma  _machine learning_  tidak dapat bekerja dengan data kategorik secara langsung dan memerlukan numerical input.  _One-hot encoding_  adalah cara untuk mengubah data kategorik menjadi data numerik.

selanjutnya,  **_One-hot encoding_**  akan diaplikasikan ke kolom  `job`,  `housing`,  `loan`,  `contact`,  `month`,  `poutcome`  karena kolom ini tidak ordinal, dan juga memiliki jumlah data unik yang sedikit.

## Modelling & Evaluation
**_Random Forest_** muncul sebagai model dengan kinerja terbaik berdasarkan metrik `roc_auc`.

## Pickle

Dikarenakan model yang dibuat adalah Random Forest, maka pickle dilakukan compress karena ukuran file nya lebih dari 25Mb yang merupakan limitasi dari github.

## Conclusion


Berdasarkan hasil classification report dari model kita, kita dapat menyimpulkan bahwa apabila nantinya model kita akan digunakan untuk memfilter list nasabah yang akan kita coba tawarkan, maka model kita dapat mengurangi 75% nasabah yang tidak tertarik untuk tidak kita approach, dan model kita dapat mendapatkan 65% nasabah yang tertarik dari seluruh nasabah yang tertarik melakukan deposit. (berdasarkan recall)

Model kita ini memiliki ketepatan prediksi nasabah yang tertarik melakukan deposito sebesar 71% (precisionnya), jadi setiap model kita dapat memprediksi bahwa seorang nasabah itu tertarik, maka kemungkinan tebakannya benar itu sebesar 71% kurang lebih. Maka masih akan ada nasabah yang sebenarnya tidak tertarik namun diprediksi sebagai nasabah yang tertarik sekitar 25% dari keseluruhan nasabah yang tidak tertarik (berdasarkan recall).

Bila seandainya biaya untuk screening/menyaring data per nasabah itu $18.34 (sumber: [https://thefinancialbrand.com/news/bank-marketing/bank-marketing-budgets-advertising-roi-strategy-88835/](https://www.google.com/url?q=https%3A%2F%2Fthefinancialbrand.com%2Fnews%2Fbank-marketing%2Fbank-marketing-budgets-advertising-roi-strategy-88835%2F)), dan andaikan jumlah nasabah yang kita miliki untuk suatu kurun waktu sebanyak 200 orang (dimana andaikan 100 orang tertarik, dan 100 orang lagi tidak tertarik), maka hitungannya kurang lebih akan seperti ini :

Tanpa Model (semua nasabah kita cek dan tawarkan) :

-   Total Biaya => 200 x 18.34 USD = 3668 USD
-   Total nasabah Tertarik yang didapatkan => 100 orang (karena semua kita tawarkan)
-   Total nasabah Tertarik yang tidak didapatkan => 0 orang (karena semua kita tawarkan)
-   Biaya yang terbuang => 100 x 18.34 USD = 1834 USD (karena 100 orang menolak dan menjadi sia-sia)
-   Jumlah penghematan => 0 USD

Dengan Model (hanya nasabah yang diprediksi oleh model tertarik yang kita check dan tawarkan) :

-   Total Biaya => (65 x 18.34 USD) + (25 x 18.34 USD) = 1650.6 USD
-   Total nasabah Tertarik yang didapatkan => 65 orang (karena recall yes/yg tertarik itu 65%)
-   Total nasabah Tertarik yang tidak didapatkan => 35 orang (karena recall yes/yg tertarik itu 65%)
-   Biaya yang terbuang => 25 x 18.34 USD = 458.5 USD (berdasarkan recall no/yg tidak tertarik (25 orang menolak tawaran/tidak tertarik))
-   Jumlah penghematan => 75 x 18.34 USD = 1375.5 USD (yang dihitung hanya yang memang tidak tertarik saja, kalau yang tertarik tapi tidak ditawarkan itu tidak dihitung disini)

Berdasarkan contoh hitungan tersebut, terlihat bahwa dengan menggunakan model kita, maka Bank tersebut akan menghemat biaya yang cukup besar tanpa mengorbankan terlalu banyak jumlah nasabah potensial/nasabah yg tertarik.

## Recommendation


Hal-hal yang bisa dilakukan untuk mengembangkan project dan modelnya lebih baik lagi:

-   Menambahkan fitur - fitur atau kolom - kolom baru yang kemungkinan bisa berhubungan dengan ketertarikannya, seperti gaji atau pendapatan, jabatan pekerjaannya sekarang (apakah karyawan, manager, direktur, dan sebagainya), status pernikahan, dll.
-   Mencoba menggunakan model machine learning yang lain dan juga mencoba hyperparameter tuning kembali.   
-   Berdasarkan dataset, masih terdapat fitur  `contact`, yang menandakan bahwa metode marketing masih menggunakan metode traditional marketing, seperti menawarkan deposit dengan cara menelpon nasabah. oleh karena itu akan lebih baik dan lebih efektif apabila menambahkan metode Digital Marketing Campaign.
