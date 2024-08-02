## <span style='color:Teal'>***Business Problem Understanding***</span>

#### ***Context***


Perusahaan hotel ABC ini berkomitmen memberikan pelayanan terbaik di Portugal dan berupaya terus berinovasi untuk meningkatkan efisiensi operasional perusahaan mereka.
Perusahaan hotel ABC lebih cenderung memanfaatkan data transaksi reservasi yang customers *`Cancel`* baik melalui metode *`online`* maupun *`offline`*. Strategi ini tidak hanya bertujuan untuk melayani *Customers* dengan lebih baik tetapi juga untuk meningkatkan efisiensi operasional. 

Mengetahui status pembatalan reservasi sangat penting bagi perusahaan hotel ABC karena berdampak langsung pada perencanaan dan pengelolaan sumber daya hotel. Dengan memanfaatkan data pembatalan, ABC Hotel dapat mengoptimalkan manajemen kamar dan staf, menghindari pemborosan sumber daya dengan menyesuaikan jumlah staf yang bertugas sesuai dengan kebutuhan riil. Hal ini tidak hanya meningkatkan efisiensi operasional tetapi juga mengurangi biaya operasional dengan meminimalkan waktu dan sumber daya yang terbuang.

Selain itu, analisis data pembatalan dapat membantu hotel dalam memahami perilaku pelanggan dan mengidentifikasi pola atau tren yang menyebabkan pembatalan. Misalnya, apakah pembatalan lebih sering terjadi pada waktu tertentu atau melalui saluran pemesanan tertentu. Memahami tren ini memungkinkan ABC Hotel untuk mengembangkan strategi pemasaran dan layanan yang lebih tepat sasaran, sehingga dapat mengurangi tingkat pembatalan dan meningkatkan kepuasan pelanggan. Dengan mengidentifikasi akar penyebab pembatalan, hotel dapat mengambil langkah proaktif untuk mengatasi masalah tersebut, seperti menawarkan insentif untuk pemesanan yang tidak dibatalkan atau meningkatkan fleksibilitas dalam kebijakan pembatalan.

Terakhir, data pembatalan dapat digunakan untuk meningkatkan prediksi permintaan di masa depan. Dengan model prediksi yang lebih akurat, ABC Hotel dapat merancang strategi harga dinamis dan promosi yang lebih efektif, memastikan bahwa tingkat hunian tetap optimal meskipun terdapat pembatalan. Hal ini akan membantu meningkatkan pendapatan dan memberikan pengalaman yang lebih baik bagi pelanggan, karena hotel dapat memastikan ketersediaan kamar dan layanan sesuai dengan kebutuhan pelanggan.

 #### ***Stakeholder***
Dalam upaya meningkatkan efisiensi operasional perusahaan hotel, divisi yang sangat penting sebagai *stakeholder* ini adalah ***Revenue Management*** pada perusahaan ABC. Divisi ini bertanggung jawab untuk mengoptimalkan pendapatan dari kamar hotel.

#### ***Problem Statement***
Perusahaan hotel ABC di Portugal sedang berupaya mengoptimalkan pengelolaan bisnisnya. Fokus utama tantangan perusahaan adalah ingin menciptakan sebuah sistem yang dapat memprediksi *Customers* yang kemungkinan besar akan `membatalkan` reservasi. Dengan begitu, perusahaan hotel dapat mengatur anggaran dan operasional secara lebih efektif, serta meningkatkan keuntungan.

#### ***Goals***
Tujuan dari proyek ini adalah untuk mengembangkan sistem prediktif yang dapat mengidentifikasi *customer* yang `cenderung membatalkan` reservasi. Dengan menggunakan hasil prediksi ini, perusahaan berencana untuk mengoptimalkan layanan yang diberikan kepada *customer*, sehingga dapat `meningkatkan efisiensi` anggaran. Selain itu, tujuan lainnya adalah memastikan operasional perusahaan berjalan lebih lancar. Dengan menerapkan informasi dari data, perusahaan berharap dapat meningkatkan kepuasan *customer* dan mengelola sumber daya dengan lebih efektif.

#### ***Analytic Approach***

Sebagai data scientist pada perusahaan hotel ABC, saya akan melakukan *data preparation* dan menentukan model klasifikasi yang tepat untuk memprediksi. Model klasifikasi yang akan diuji adalah logistic regression, random forest classifier, decition tree classifier, XGBClassifier, dan AdaBoostClassifier, kemudian Kita akan membangun model klasifikasi yang akan membantu perusahaan memprediksi probabilitas pembatalan *booking* oleh seorang *customer*.

### ***Metric Evaluation***

#### Target:
- **0**: Tidak Membatalkan
- **1**: Membatalkan

- **True Positive (TP)**: Pelanggan yang diprediksi membatalkan dan benar-benar membatalkan.
- **False Positive (FP)**: Pelanggan yang diprediksi membatalkan, tetapi sebenarnya tidak membatalkan.
- **False Negative (FN)**: Pelanggan yang diprediksi tidak membatalkan, tetapi sebenarnya membatalkan.
- **True Negative (TN)**: Pelanggan yang diprediksi tidak membatalkan dan benar-benar tidak membatalkan.

Fokus evaluasi model prediksi pembatalan hotel terutama pada **False Negatives** karena dampak ekonominya yang lebih merugikan. Kesalahan ini menyebabkan **kerugian** langsung berupa kehilangan **pendapatan** dan **biaya tambahan** untuk mengakomodasi pembatalan yang tidak terdeteksi. Dengan meminimalkan kasus di mana pelanggan yang sebenarnya membatalkan tetapi diprediksi tidak membatalkan (False Negative), model dapat membantu hotel mengambil tindakan pencegahan yang tepat waktu, mengurangi kerugian, dan mempertahankan pendapatan.

Tindakan Hotel Terhadap Hasil Prediksi: Jika pelanggan diprediksi akan membatalkan, hotel akan memberikan insentif berupa **voucher dinner** maksimal untuk 2 orang per kamar, untuk mendorong pelanggan tetap mempertahankan pemesanan.

- **Type 1 Error (False Positive)**: Pelanggan yang sebenarnya tidak membatalkan tetapi diprediksi membatalkan.
  - **Konsekuensi**: Hotel harus menanggung biaya dinner sebesar 20 Euro per kamar.

- **Type 2 Error (False Negative)**: Pelanggan yang sebenarnya membatalkan tetapi diprediksi tidak membatalkan.
  - **Konsekuensi**: Hotel kehilangan kesempatan untuk mendapatkan pendapatan dari harga kamar hotel.

Untuk memberikan gambaran konsekuensi secara kuantitatif, maka kita akan coba hitung dampak biaya berdasarkan asumsi berikut:
- **Harga rata-rata hotel per malam di Portugal**: 100 Euro (asumsi tengah dari rentang 50 - 150 Euro).
- **Harga dinner per orang**: 10 Euro, dengan maksimal voucher dinner untuk 2 orang per kamar adalah 20 Euro.

Dalam bisnis hotel, evaluasi model prediksi pembatalan harus fokus pada **False Negative** karena dampaknya yang signifikan terhadap kehilangan pendapatan dan biaya tambahan. Metrik **recall** sangat relevan dalam konteks ini, karena mengukur seberapa baik model dalam menangkap semua pelanggan yang membatalkan. Recall dihitung dengan rumus:

$$
\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}
$$


Meningkatkan recall membantu hotel meminimalkan dampak ekonomi dari **False Negative**, memungkinkan mereka untuk mengambil tindakan preventif yang lebih efektif, seperti memberikan voucher dinner untuk mencegah pembatalan dan meningkatkan retention rate. Dengan cara ini, hotel dapat mengoptimalkan strategi mereka dan menjaga pendapatan dengan lebih baik.

## <span style='color:Teal'>***Conclusion***</span>

Berdasarakan analisis dan pengembangan model yang telah dilakukan, model prediktif yang mampu mengidentifikasi *customer* yang memiliki potensi melakukan *cancel* didapat menggunakan algoritma *`XGBoost`* dengan parameter:
- **feature_selection__k**:
  - Nilai k yang digunakan untuk seleksi fitur dengan SelectKBest, dengan k = 9
- **classifier**:
  - Model yang digunakan untuk klasifikasi.
  - Dalam kasus ini, XGBClassifier digunakan.
- **classifier__n_estimators**:
  - Jumlah pohon yang digunakan dalam boosting.
  - Rentang nilai yang diuji: [50, 100, 200].
- **classifier__max_depth**:
  - Kedalaman maksimum pohon.
  - Rentang nilai yang diuji: [3, 6, 9].
- **classifier__learning_rate**:
  - learning rate yang digunakan untuk memperbarui bobot.
  - Rentang nilai yang diuji: [0.01, 0.1, 0.2].
- **classifier__subsample**:
  - Proporsi sampel yang digunakan untuk melatih setiap pohon.
  - Rentang nilai yang diuji:[0.8, 0.9, 1.0].
- **classifier__colsample_bytree**:
  - Proporsi kolom yang digunakan untuk melatih setiap pohon.
  - Rentang nilai yang diuji: [0.8, 0.9, 1.0].
- **classifier__gamma**:
  - Minimum loss reduction yang diperlukan untuk melakukan pemisahan di node daun.
  - Rentang nilai yang diuji: [0, 0.1, 0.2, 0.3]

  
Didapati juga Dengan `memberikan kupon free dinner` kepada customer yang diprediksi akan melakukan cancel booking:
  - Pendapatan `hilang tanpa kupon free dinner`: 603.200 euro.
  - Pendapatan `yang didapat dengan kupon free dinner`: 482.560 euro.

`Free dinner` menambah jumlah cost hotel sebesar `120.640 euro` per malam, tetapi `pendapatan yang bisa diselamatkan` dengan kupon free dinner tersebut adalah `482.560 euro`.

## <span style='color:Teal'>***Recommendation***</span>
**Rekomendasi Bisnis**

Model prediktif yang menggunakan algoritma XGBoost dapat menjadi alat yang efektif bagi manajemen ABC Hotel untuk mengidentifikasi pelanggan yang berpotensi melakukan pembatalan. Dengan menggunakan model ini, diharapkan tim dapat mengambil tindakan proaktif untuk mengurangi tingkat pembatalan dan meningkatkan pendapatan hotel. Berikut adalah rekomendasi yang dapat diterapkan:

1. Kupon Free Dinner untuk Pelanggan yang Diprediksi Membatalkan
Berikan kupon makan malam gratis senilai 20 euro untuk dua orang per kamar kepada pelanggan yang diprediksi akan membatalkan. Penawaran ini dapat meningkatkan loyalitas pelanggan dan mengurangi insentif untuk membatalkan pemesanan.
Implementasi: Gunakan model prediksi untuk mengidentifikasi pelanggan dengan risiko pembatalan tinggi. Komunikasikan penawaran ini melalui email atau notifikasi aplikasi.

1. Program Loyalitas Pelanggan
Memperkuat program loyalitas untuk meningkatkan retensi pelanggan dan mengurangi pembatalan.
Implementasi: Berikan poin loyalitas atau diskon khusus kepada pelanggan yang sering menginap. Tawarkan manfaat tambahan seperti upgrade kamar gratis dan layanan sarapan.

1. Penawaran Paket Spesial
Penawaran paket spesial dapat menarik pelanggan untuk menginap lebih lama dan meningkatkan pendapatan.
Implementasi: Tawarkan paket menginap yang mencakup layanan tambahan seperti spa atau makan malam, dan diskon untuk menginap lebih lama atau pemesanan grup.

1. Peningkatan Pengalaman Pelanggan
Peningkatan pengalaman pelanggan dapat meningkatkan kepuasan dan mengurangi pembatalan.
Implementasi: Investasikan dalam pelatihan staf dan perbaikan fasilitas untuk meningkatkan kenyamanan dan kepuasan pelanggan.

1. Kampanye Pemasaran yang Efektif
Kampanye pemasaran yang tepat dapat menarik pelanggan baru dan mengurangi pembatalan.
Implementasi: Gunakan data analitik untuk menargetkan kampanye pemasaran ke segmen pelanggan yang tepat. Promosikan ulasan positif dan testimoni pelanggan di media sosial dan platform online.
Dengan menerapkan strategi ini, ABC Hotel dapat meningkatkan retensi pelanggan dan mengurangi tingkat pembatalan, yang pada akhirnya akan meningkatkan pendapatan dan efisiensi operasional.

**Model Improvement Recommendation**

Untuk meningkatkan kinerja model prediktif dalam mengidentifikasi pelanggan yang berpotensi membatalkan pemesanan, berikut adalah beberapa rekomendasi yang dapat diimplementasikan:

1. Peningkatan Kualitas Data
Memastikan bahwa data yang digunakan untuk pelatihan model lebih detail dan akurat sangat penting untuk meningkatkan kinerja model.
Implementasi: Pada kampanye pemasaran berikutnya, pastikan untuk mencatat hasil kampanye secara detail, termasuk informasi seperti kategori keberhasilan kampanye dan karakteristik pelanggan. Data yang lebih kaya akan membantu model belajar lebih efektif dan meningkatkan akurasi prediksi pembatalan.

1. Eksplorasi Model Alternatif
Mencoba model alternatif dapat membantu menemukan algoritma yang lebih sesuai dengan dataset dan tujuan prediktif.
Implementasi: Uji model lain seperti AdaBoost, CatBoost, atau deep learning untuk menentukan apakah ada model yang dapat memberikan recall yang lebih tinggi. Menggunakan metode seperti cross-validation untuk membandingkan performa model berdasarkan recall akan membantu dalam mengidentifikasi model yang paling efektif.

1. Penggunaan Teknik Peningkatan Recall
Fokus pada peningkatan recall sangat penting, terutama jika biaya False Negative tinggi, seperti dalam kasus pelanggan yang tidak terdeteksi membatalkan.
Implementasi: Terapkan teknik-teknik seperti oversampling pada kelas minoritas, penyesuaian threshold prediksi, atau cost-sensitive learning untuk meningkatkan recall. Memastikan bahwa model lebih sensitif terhadap kasus pembatalan dapat mengurangi kerugian terkait pembatalan yang tidak terdeteksi.

1. Feature Engineering Lebih Lanjut
Melakukan feature engineering lebih lanjut dapat membantu mengidentifikasi fitur-fitur baru yang berkontribusi lebih baik terhadap prediksi pembatalan.
Implementasi: Analisis data untuk menemukan fitur tambahan seperti pola perilaku pelanggan, tren musiman, atau interaksi antar fitur yang dapat meningkatkan kemampuan model dalam memprediksi pembatalan.

1. Pemantauan dan Penyesuaian Berkelanjutan
Pemantauan terus-menerus terhadap kinerja model dan penyesuaian sesuai kebutuhan dapat memastikan model tetap relevan dan akurat.
Implementasi: Lakukan pemantauan rutin terhadap kinerja model pada data baru dan lakukan penyesuaian pada fitur, parameter model, atau strategi prediksi untuk memastikan model tetap optimal dalam memprediksi pembatalan.
Dengan menerapkan rekomendasi ini, diharapkan model dapat meningkatkan recall dan membantu ABC Hotel dalam mengidentifikasi dan menangani pelanggan yang berpotensi membatalkan pemesanan dengan lebih efektif.






