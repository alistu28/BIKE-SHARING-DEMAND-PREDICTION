# Bike Sharing Demand
_Created By : Alifia Listu Samatha - JCDS Purwadhika Bandung_

![](https://cdn.lyft.com/static/bikesharefe/logo/CapitalBikeshare-main.svg)

Perusahaan Capital Bikeshare adalah perusahaan yang membuat sistem berbagi sepeda di Washington, D.C. Sistem berbagi sepeda adalah generasi baru persewaan sepeda tradisional di mana seluruh proses, mulai dari keanggotaan hingga persewaan hingga pengembalian, dilakukan secara otomatis. Pengguna dapat dengan mudah menyewa sepeda dari satu lokasi dan mengembalikannya ke lokasi lain menggunakan sistem ini. Saat ini terdapat lebih dari 500 program berbagi sepeda di seluruh dunia, dengan lebih dari 500 ribu sepeda. Sistem ini saat ini mendapatkan popularitas karena pentingnya masalah lalu lintas, lingkungan, dan kesehatan.

Selain aplikasi dari perusahaan Capital Bikeshare yang menarik, karakteristik data yang dihasilkan oleh sistem berbagi sepeda membuatnya menarik untuk penelitian. Berbeda dengan jenis transportasi lain seperti bus atau kereta bawah tanah, durasi perjalanan, posisi keberangkatan dan kedatangan dicatat secara eksplisit dalam sistem ini. Fitur ini mengubah sistem berbagi sepeda menjadi jaringan sensor virtual yang dapat digunakan untuk memonitor mobilitas kota. Akibatnya, pemantauan data ini diharapkan dapat mendeteksi peristiwa terpenting di kota.

# Contents
1. Business Understanding
2. Data Understanding
3. Exploratory Data Analysis
4. Modeling
5. Conclusion
6. Recommendation

# Business Understanding

**Stakeholders**

**Tim Operasional** di Perusahaan Capital Bikeshare

**Problem Statement**

Berbagi sepeda (*bike-sharing*) muncul sebagai sarana transportasi alternatif yang secara komprehensif dapat memperbaiki masalah lingkungan, kemacetan lalu lintas, kualitas hidup yang buruk yang disebabkan oleh sistem transportasi yang berorientasi pada mobil, dan dapat menjamin efek praktis. Namun, meskipun banyak keuntungannya, jumlah kota dan bisnis yang enggan memperkenalkan program sepeda bersama semakin meningkat karena kerugian dari biaya tetap yang tinggi seperti biaya pemasangan atau biaya operasional. Dengan demikian, **prediksi permintaan yang akurat diperlukan untuk pengoperasian program bike sharing yang berkelanjutan**.

**Goals**

Berdasarkan permasalahan tersebut, Perusahaan Capital Bikeshare tentu perlu memiliki *tool* yang dapat memprediksi dan membantu Tim Operasional dalam **menentukan jumlah sepeda yang harus disediakan pada waktu tertentu**. Adanya perbedaan pada berbagai fitur yang terdapat pada suatu atribut, seperti suhu, cuaca, dan musim dapat menambah keakuratan prediksi jumlah sepeda.

Bagi Perusahaan Capital Bikeshare, *prediction tool* yang dapat memberikan prediksi jumlah sepeda pada waktu serta memahami pola yang telah ditetapkan yang diikuti orang (*User Capital Bikeshare*) dapat membantu mengoptimalkan sistem berbagi sepeda, memaksa operator untuk mengantisipasi kepadatan sepeda atau kekurangan sepeda di stasiun tertentu dan mengoptimalkan redistribusinya sebagai respons terhadap situasi tersebut.

**Analytic Approach**

Jadi, kita perlu menganalisis data untuk mengidentifikasi pola di antara fitur-fitur yang ada yang membedakan satu pola sewa dari yang lain. Selanjutnya akan **dibuat model regresi** yang akan membantu perusahaan dalam menyediakan '*tool*' untuk memprediksi jumlah sepeda yang dibutuhkan pada waktu tertentu, yang akan berguna bagi Tim Operasional dalam mengoptimalkan pendistribusian sepeda pada waktu yang tepat sehingga dapat meningkatkan kepuasan pelanggan terhadap sistem.

**Metric Evaluation**

Evaluasi  metrik yang akan digunakan adalah RMSE, MAE, dan MAPE.

- **RMSE** adalah rata-rata akar kuadrat dari *error*.
- **MAE** adalah nilai absolut rata-rata dari *error*.
- **MAPE** adalah rata-rata proporsi *error* yang dihasilkan oleh model regresi.
- Semakin **rendah** nilai RMSE, MAE, dan MAPE, semakin **baik** model memprediksi jumlah sepeda berdasarkan batasan fitur yang digunakan.

Selain itu, jika model yang akan digunakan sebagai **model akhir adalah model linear**, kita dapat menggunakan R-squared atau Adjusted R-squared. Nilai R-squared digunakan untuk mengetahui seberapa baik model dapat merepresentasikan varians keseluruhan data. Semakin mendekati 1, maka semakin fit pula modelnya terhadap data observasi. Namun, metrik ini tidak valid untuk model non-linear.

# Modeling Workflow

Test

# Conclusion

**Exploratory Data Analysis**
- Sebagian besar persewaan adalah untuk perjalanan sehari-hari ke tempat kerja.
- Jam : Hitungan persewaan sepeda sebagian besar berkorelasi dengan waktu dalam sehari. Hitungan mencapai titik tertinggi selama jam sibuk pada hari kerja dan sebagian besar seragam pada siang dan sore hari di luar hari kerja.
- Suhu : Orang umumnya lebih suka bersepeda pada suhu sedang hingga tinggi. Terlihat bahwa jumlah sewa tertinggi antara 32 - 36 derajat Celcius.
- Musim : Terlihat bahwa jumlah persewaan sepeda tertinggi di Musim Semi (Juli hingga September) dan Musim Panas (April hingga Juni) dan terendah di Musim Dingin (Januari hingga Maret).
- Cuaca: Terlihat bahwa jumlah persewaan sepeda tertinggi pada hari yang cerah dan terendah pada hari bersalju atau hujan.
- Kelembaban : Dengan meningkatnya kelembapan, terlihat adanya penurunan jumlah sewa sepeda.
- Pengguna *casual* cenderung lebih sering menyewa sepeda selama waktu santai, sedangkan pengguna *registered* menggunakan sepeda untuk kebutuhan kerja sehari-hari.

**Machine Learning Modeling**
- Model XGBoost Regression mengungguli 4 model regresi lainnya (linear regression, knn regression regression, decision tree regression, random forest regression) dalam hal RMSE, MAE, dan MAPE.
- Dari hasil Benchmark Model dan Hyperparameter Tuning, diperoleh model XGBoost dengan performa terbaik dengan parameter terbaik sebagai berikut:

<center>

| Parameter     | Value          |
|---------------|----------------|
| scaler        | RobustScaler() |
| n_estimators  | 205            |
| max_depth     | 7              |
| learning_rate | 0.1            |

</center>

- Metrik evaluasi yang digunakan pada model ini adalah nilai RMSE, MAE & MAPE. Tidak menggunakan R-squared karena model akhir bukan model linear.
- Model mengalami peningkatan performa (nilai RMSE, MAE & MAPE berkurang) dengan dilakukannya hyperparameter tuning, walaupun hanya sedikit (kurang dari 6 persen).

<center>

| Metrics | XGBoost (Before Tuning) | XGBoost (After Tuning) | Decrease Percentage|
|---------|-------------------------|------------------------|--------------|
| RMSE    | 42.037373               | 39.900587              | ↓5.08%    |
| MAE     | 25.642264               | 24.23665               | ↓5.48%    |
| MAPE    | 0.255405                | 0.243843               | ↓4.52%    |

</center>

- Nilai RMSE = 39.9 (dibulatkan menjadi 40), maka ini menunjukkan bahwa hasil prediksi model berkisar kurang lebih 40 sepeda dari niali prediksi model dengan nilai maksimum yang dilatih model adalah 645 sepeda.
- Walau kedua metrics (RMSE dan MAE) mengembalikan nilai error yang sama, nilai RMSE lebih tinggi dari MAE karena RMSE lebih sensitif terhadap outlier, dan outlier dalam dataset yang meningkatkan nilai error.
- Nilai MAPE = 24.38, maka ini menunjukkan bahwa rata-rata hasil prediksi model adalah 24,38% dari target.
- Fitur yang paling mempengaruhi target (count) adalah fitur 'hour', diikuti oleh fitur 'onehot_working_day_1'.
- Secara keseluruhan hasil prediksi sudah cukup baik, namun masih terdapat beberapa hasil prediksi yang menyimpang baik lebih tinggi (overestimation) atau lebih rendah (underestimation).
- Menyelidiki beberapa tanggal dan jam tertentu dengan deviasi yang tinggi menunjukkan bahwa ada kejadian khusus yang terjadi pada hari tersebut yang tidak dapat diambil sebagai masukan untuk model, oleh karena itu tidak dapat diwakili oleh model. Contohnya:

<center>

| Type                                  | Date                            | Event                                                                                                                                                                                                                                                          | Impact                                                                                                                                                                                                                                                                                                                                                                      |
|---------------------------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Underestimation (-296 Sepeda)   | Senin, 16 April 2012 (7 AM)     | [ Pembukaan Kembali Institut Politeknik Virginia Setelah 1 Tahun Tutup Karena Kasus Pembunuhan Masal ](  https://www.washingtonpost.com/blogs/campus-overload/post/va-tech-marks-massacre-anniversary-by-returning-to-class/2012/04/16/gIQAesOQLT_blog.html  ) | Karena limitasi data yang hanya ada 2 tipe tahun (2011 dan 2012), sedangkan pada bulan yang sama di tahun 2011 terjadi peristiwa penembakan masal di Institut Politeknik Virginia hingga sempat ditutup. Mesin tidak dapat memprediksi pembukaan kembali suatu institut yang tutup. Hal ini berpengaruh pada jumlah sewa bike-share yang meningkat pesat di hari pembukaan. |
| Overestimation (+214 Sepeda) | Minggu, 19 Agustus 2012 (15 PM) | [ Gempa di Off Coast Washington D.C 5.2 SR Jam 8 Pagi ]( https://earthquakescanada.nrcan.gc.ca/recent/2012/20120819.0807/index-en.php )                                                                                                                        | Terjadinya gempa pada hari minggu pagi, menyebabkan orang-orang lebih waspada terhadap gempa susulan dan lebih memilih untuk berdiam dirumah dan memastikan keadaan luar aman terlebih dahulu. Mesin juga tidak bisa memprediksi bencana alam yang datang. Hal ini berpengaruh pada penurunan jumlah sewa sepeda.                                                           |

</center>

- Permintaan sistem berbagi sepeda sangat bergantung pada musim dan kondisi lingkungan yang membuatnya dapar diprediksi menggunakan model pembelajaran mesin (*Machine Learning*).
- Model ini juga dapat digunakan untuk deteksi peristiwa dan anomali seperti yang sudah dijelaskan diatas.

**Limitation**

- Project ini memiliki beberapa keterbatasan karena selalu ada outlier dalam praktiknya dan model mungkin gagal memprediksinya.
- Datanya hanya 2 tahun (2011 - 2012) sehingga hanya dapat menunjukan pola 2 tahun. 
- Kejadian harian yang dilaporkan merupakan faktor spesifik yang dapat bervariasi, adanya beberapa kejadian di hari itu yang tidak ada laporannya kepada publik dapat membatasi dalam interpretasi anomali.

# Recommendation

**Dari Sisi Bisnis**
- Saat merencanakan sepeda tambahan ke stasiun, jam sewa puncak harus dipertimbangkan, yaitu 7–9 pagi dan 5–6 sore.
- Sebagian besar persewaan adalah untuk pergi bekerja setiap hari. Jadi tim operasional harus meluncurkan lebih banyak stasiun di dekat gedung kerja untuk menjangkau pelanggan utama mereka.
- Disarankan adanya diskon musiman untuk mengandalkan perubahan musim dan memprioritaskan pesepeda di musim gugur dan musim dingin yang jumlahnya sedikit peminatnya.
- Adanya data tentang rute yang paling banyak digunakan dapat membantu membangun jalur khusus sepeda.
- Dikarenakan rendahnya penggunaan sepeda pada malam hari, sebaiknya dilakukan perawatan sepeda pada malam hari.
- Mengubah pelanggan terdaftar menjadi pelanggan biasa di akhir pekan dengan memberi mereka diskon dan kupon dapat menaikan profit perusahaan.

**Dari Sisi Teknis (Machine Learning Modeling)**
- Penambahan fitur stasiun karena setiap stasiun tentunya memiliki persyaratan yang berbeda, sehingga dengan adanya fitur ini akan meningkatkan kualitas prediksi model.
- Setelah penambahan fitur, model ini juga dapat digunakan untuk pengembangan model seperti model prediksi permintaan sepeda di setiap stasiun dengan melihat karakteristik masing-masing stasiun. 
- Penambahan data pada cuaca Heavy Rain/Snow, karena datanya hanya ada 3.
- Penambahan data di tahun lain yang berbeda seperti kumpulan data dari tahun 2011-2016 dapat meningkatkan kualitas prediksi model.
- Penggunaan model timeseries forecasting seperti Simple Moving Average (SMA), Exponential Smoothing (SES), Autoregressive Integration Moving Average (ARIMA), dan Neural Network (NN) dapat dicoba digunakan.
