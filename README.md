# CapstoneModule3
## California Housing Price

# Business Problem Understanding
**Context**

Dataset ini berisi tentang informasi rumah-rumah dari distrik-distrik di California berdasarkan data tahun 1990. Meskipun data ini sudah lama, dataset ini masih dapat digunakan karena memberikan wawasan tentang pola-pola dasar yang memengaruhi harga rumah. Dataset ini terdiri dari beberapa fitur seperti lokasi geografis, jumlah kamar, jumlah rumah tangga, populasi, usia rata-rata rumah, pendapatan rata-rata, serta nilai rata-rata rumah. Selain itu, terdapat informasi tentang kedekatan geografis rumah dengan laut, yang dapat memengaruhi nilai properti di wilayah tersebut

**Problem Statement**

dikutip dari [AntaraNews](https://www.antaranews.com/berita/4160796/harga-rumah-di-california-catat-rekor-tertinggi-pada-mei-2024).
Harga rumah median di seluruh California, negara bagian dengan jumlah penduduk terbesar di Amerika Serikat (AS), mencatatkan rekor tertinggi baru pada Mei 2024. Karena kelangkaan rumah yang dijual, terutama pada segmen pasar dengan Harga yang lebih terjangkau, terus mendorong Harga median rumah di California ke rekor tertinggi baru. 

Dengan meningkatnya Harga median rumah di California, penting untuk memahami faktor-faktor apa saja yang mempengaruhi Harga rumah untuk membantu berbagai pihak seperti agen properti dan pengembang perumahan untuk mengambil keputusan dalam menentukan harga rumah.

**Goals**

Berdasarkan permasalahan yang ada, Meskipun dataset yang kita miliki tidak bisa untuk memprediksi harga rumah saat ini, tapi kita bisa memahami tentang faktor-faktor yang memengaruhi harga rumah karena sangat penting bagi berbagai pihak. Fitur seperti usia rumah, populasi, pendapatan rata-rata, dan lokasi geografis (misalnya kedekatan dengan laut) dapat memberikan wawasan penting tentang nilai properti atau harga rumah.

**Analytic Approach**

Jadi yang diperlukan adalah menganalisis data untuk menemukan pola atau hubungan antara fitur yang tersedia dalam mempengaruhi Harga rumah.

perlu juga untuk membangun model prediksi menggunakan algoritma regresi untuk memprediksi nilai median rumah berdasarkan fitur-fitur yang tersedia. Model prediksi ini akan sangat berguna untuk membantu berbagai pihak, seperti pembeli rumah, agen properti dan pengembang perumahan, dalam membuat keputusan berdasarkan wawasan data. 

**Metric Evaluation**

Evaluasi metrik yang akan digunakan adalah RMSE, MAE, dan MAPE.
1. RMSE (Root Mean Square Error): Nilai ini menunjukkan akar rata-rata kuadrat dari error. RMSE mengukur tingkat kesalahan prediksi dengan memberikan bobot yang lebih besar pada error yang lebih besar. Semakin kecil RMSE, semakin baik performa model.
2. MAE (Mean Absolute Error): Nilai rata-rata absolut dari error yang menunjukkan seberapa jauh prediksi model dari nilai sebenarnya. MAE memberikan gambaran tentang kesalahan rata-rata tanpa memperhatikan arah error.
3. MAPE (Mean Absolute Percentage Error): Rata-rata persentase error relatif terhadap nilai sebenarnya. MAPE cocok digunakan untuk mengukur akurasi model dalam konteks harga rumah, karena error dinyatakan dalam bentuk persentase, yang lebih mudah dimengerti.

# Data Understanding
**Column Description**

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| longitude | Float | Koordinat geografis rumah berdasarkan bujur |
| latitude | Float | Koordinat geografis rumah berdasarkan lintang |
| housing_median_age | Float | Usia rata-rata rumah |
| total_rooms | Float | Total jumlah ruangan |
| total_bedrooms | Float | Total jumlah kamar tidur |
| population | Float | Jumlah total penduduk |
| households | Float | Jumlah total rumah tangga |
| median_income | Float | Pendapatan rata-rata per rumah tangga |
| ocean_proximity | Object | Kedekatan geografis rumah dengan laut |
| median_house_value | Float | Nilai rata-rata rumah |

<br>

**Exploratory Data Analysis**
Melakukan Exploratory data pada kolom numerik dan kategorikal

# Data Preprocessing
1. Missing Value
    Dilakukan pengecekan missing value, karena terdapat missing value maka missing value tersebut ditangani setelah dilakukan observasi.
2. Duplicate Data
    Setelah dilakukan pengecekan tidak ada data yang duplikat
3. Label Encoding
    Karena untuk ocean_proximity merupakan jarak kedekatan dengan laut, jika menggunakan One Hot Encoding  ditakutkan tidak sesuai dengan urutan jarak kedekatan laut, maka dari itu disini saya menggunakan manual label encoding.
4. Data Correlation
    Dilakukan pengecekan korelasi dengan menggunakan Correlation Matrix.
5. Outliers Detection
    Dilakukan pengecekan dan penanganan untuk outliers.
6. Feature Selection
    Melakukan drop fitur pada fitur yang memiliki korelasi kecil dengan target dan juga fitur yang sekiranya tidak dibutuhkan. tetapi setelah membuat model, saya coba bandingkan model ketika dilakukan fitur selection dan tidak, ternyata model lebih baik ketika tidak dilakukan fitur selection sehingga saya tidak jadi melakukan fitur selection.

# Modeling
1. Data Splitting
2. Model Selection & Scaling Data
3. Tuning
4. Performance Comparison
5. Feature Importances

# Conclusion & Recommendation
**Conclusion**
Berdasarkan analisis data yang dilakukan diawal, fitur 'proximity_encode' dan 'median_income' adalah fitur yang paling berpengaruh terhadap 'median_house_value', hal ini juga didukung kuat oleh pemodelan yang telah dilakukan menggunakan model XGBoost Regressor.

Pada model ini digunakan 3 metrics evaluation, yaitu RMSE, MAE, dan MAPE. Nilai MAPE yang dimiliki oleh model setelah dilakukan hypertparameter tuning adalah 17.86%. Nilai MAPE sebesar 17.86% menunjukkan bahwa model ini berada dalam kategori Good Forecasting, yang berarti rata-rata prediksi model meleset sekitar 17.86% dari nilai actual.

Dengan nilai ini, model dapat digunakan untuk memperkirakan nilai median house value pada rentang data yang mirip dengan data training. Meskipun demikian, hasil evaluasi juga menunjukkan bahwa terdapat beberapa outlier yang menyebabkan prediksi jauh meleset dari nilai aktual, baik dalam bentuk overestimation maupun underestimation. Hal ini dapat disebabkan oleh keterbatasan fitur dalam dataset yang digunakan. Fitur tambahan yang lebih relevan, seperti faktor eksternal atau atribut yang lebih spesifik, berpotensi meningkatkan akurasi prediksi model di masa depan.

Untuk mengetahui tingkat efektivitas penggunaan model, karena dataset yang kita gunakan adalah data dari tahun 1990 maka **Backtesting** adalah metode yang paling relevan untuk mengukur efektivitas model dalam memprediksi data historis.

**Recommendation**
    Lakukan Backtesting untuk menguji tingkat efektivitas model terhadap harga median house value.

Lalu, hal-hal yang dapat dilakukan untuk mengembangkan model agar lebih baik lagi, seperti:
1. Tentukan prediksi yang memiliki nilai error tinggi (overestimation dan underestimation). Pemisahan error akan membantu mengidentifikasi area yang perlu diperbaiki. Setelah mengelompokkan data berdasarkan error, periksa hubungan antara error dan fitur-fitur yang ada (seperti median income, proximity encode, longitude, dan latitude). Temukan fitur mana yang paling berkontribusi terhadap error tinggi dan perbaiki dengan feature engineering atau transformasi fitur.

2. Gunakan ensemble methods seperti bagging atau boosting untuk mengurangi overfitting dan meningkatkan stabilitas model.

3. Gunakan pembagian data yang lebih tepat dengan cross-validation atau hold-out validation untuk mengevaluasi model dengan data yang tidak terlihat. Jika memungkinkan, gunakan data terbaru untuk melakukan validasi model dan menghindari overfitting pada data historis.

4. Pertimbangkan untuk menggabungkan beberapa fitur yang ada untuk menciptakan fitur baru yang lebih informatif.

5. Kita juga bisa mengembangkan model untuk memprediksi Harga rumah dinamis, yang mempertimbangkan faktor ekonomi dan sosial masyarakat. Untuk melakukan itu kita bisa saja melibatkan variabel lain misalkan seperti tingkat pengangguran, pertumbuhan ekonomi, dll.
