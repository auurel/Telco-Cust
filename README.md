# Telco Customer Churn Prediction - Project 2

## Pengenalan
Proyek ini didedikasikan untuk memprediksi *customer churn* (pemberhentian layanan oleh pelanggan) di industri telekomunikasi. Memprediksi *churn* adalah tugas krusial bagi perusahaan untuk mempertahankan pelanggan dan membuat keputusan bisnis berbasis data guna mengurangi tingkat atrisi.

## Dataset
Dataset yang digunakan berisi informasi riwayat pelanggan dari perusahaan telekomunikasi besar, yang mencakup data demografi, langganan layanan, tagihan bulanan dan total, serta status *churn* pelanggan dalam kurun waktu satu bulan terakhir. Dataset ini terdiri dari 7.043 baris dan 21 kolom fitur.

## Objektif Proyek
Tujuan utama dari proyek ini adalah:
1. **Prediksi Churn**: Mengaplikasikan 3 metode prediktif (*machine learning*) untuk memprediksi apakah pelanggan akan melakukan *churn*.
2. **Analisis Data (EDA)**: Melakukan *Exploratory Data Analysis* (EDA) mendalam untuk memahami pola perilaku pelanggan dan faktor-faktor yang memengaruhi *churn*.
3. **Pembangunan Model**: Membangun model klasifikasi menggunakan algoritma *Logistic Regression*, *Decision Tree*, dan *Random Forest*.
4. **Evaluasi Model & Rekomendasi**: Mengevaluasi performa model menggunakan metode evaluasi formal dan menyusun rekomendasi strategi bisnis untuk mengurangi *churn* berdasarkan temuan data.

## Metodologi & Persiapan Data (Data Preparation)
Sebelum dimasukkan ke dalam model, data mentah melalui beberapa tahapan prapemrosesan:
* **Pembersihan Data**: Penanganan *blank space* dan *missing values* pada kolom `TotalCharges` dengan mengisi nilai menggunakan median data.
* **Encoding**: Menggunakan teknik *One-Hot Encoding* (`pd.get_dummies`) untuk mengonversi variabel kategorikal nominal (seperti *PaymentMethod* dan *InternetService*) menjadi format numerik agar kompatibel dengan algoritma prediksi.
* **Penanganan Imbalance Data**: Ditemukan bahwa data memiliki proporsi target yang tidak seimbang (~73.5% *No Churn* vs ~26.5% *Churn*). Hal ini diatasi dengan memberikan argumen pembobot `class_weight='balanced'` pada setiap model untuk mengoptimalkan sensitivitas deteksi kelas minoritas.

## Insight & Key Findings (Exploratory Data Analysis)
Berdasarkan visualisasi dan ekstraksi korelasi fitur, ditemukan beberapa *insight* utama pemicu *churn*:
* **Tipe Kontrak**: Pelanggan dengan kontrak jangka pendek (*Month-to-month*) memiliki tingkat risiko *churn* yang paling tinggi dan mendominasi angka pemberhentian layanan. Sebaliknya, kontrak dua tahun (*Two year*) bertindak sebagai penahan *churn* terkuat.
* **Layanan Internet**: Penggunaan layanan internet *Fiber optic* memiliki korelasi positif yang sangat tinggi terhadap keputusan pelanggan untuk *churn*, mengindikasikan adanya kemungkinan masalah kepuasan pada layanan ini.
* **Masa Berlangganan (*Tenure*)**: Masa berlangganan yang singkat sangat rentan terhadap atrisi pelanggan.

Berikut adalah perbandingan performa ketiga model:
* **Logistic Regression:** Setelah dilakukan penyeimbangan data, model ini menghasilkan nilai **Recall sebesar 0.82**. Model ini terbukti cukup stabil dalam mendeteksi pola linear pada fitur pelanggan, serta memberikan interpretabilitas yang baik.
* **Decision Tree:** Menghasilkan nilai **Recall sebesar 0.81**. Algoritma ini mengalami lonjakan performa pendeteksian kelas minoritas yang paling drastis setelah di- *balance*, membuktikan kemampuannya memetakan aturan (*rules*) keputusan secara berjenjang terhadap data pelanggan.
* **Random Forest (Model Terbaik):** Algoritma *ensemble learning* ini keluar sebagai model yang paling optimal dan *robust*. Random Forest berhasil mencetak nilai **Recall tertinggi yaitu 0.84**, sekaligus mempertahankan tingkat **Accuracy secara keseluruhan di angka 0.76**. 

**Kesimpulan Evaluasi:** Berdasarkan pembuktian dari metode evaluasi formal, Random Forest adalah model prediktif terbaik untuk kasus ini. Dengan nilai *Recall* 0.84, model ini diestimasikan mampu mendeteksi dan "menyelamatkan" 84% dari total pelanggan yang berisiko melakukan *churn*, memberikan kesempatan bagi tim pemasaran untuk mengeksekusi strategi retensi secara tepat sasaran.

## Rekomendasi Bisnis
Berdasarkan prediksi model dan korelasi data, rekomendasi strategis yang dapat diterapkan perusahaan untuk mengurangi churn adalah:
1. Menawarkan promo khusus atau diskon bagi pelanggan *Month-to-month* yang bersedia beralih ke kontrak berlangganan 1 atau 2 tahun.
2. Melakukan audit dan perbaikan kualitas pada infrastruktur layanan *Fiber Optic* untuk menekan tingkat kekecewaan pelanggan.
3. Memberikan *treatment* retensi ekstra pada pelanggan baru dengan *tenure* (masa berlangganan) di bawah 6 bulan.
