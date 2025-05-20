# **Laporan Proyek Machine Learning - [Laila]**
## **🏘️ Domain Proyek**

Prediksi harga rumah adalah aspek krusial di bidang real estat, yang mempengaruhi pembelian, penjualan, investasi, dan kebijakan perencanaan kota. Estimasi harga yang tepat akan membantu beragam pihak, seperti pembeli, penjual, agen properti, dan lembaga keuangan, untuk mengambil keputusan yang tepat. Kendati itu, kompleksitas faktor yang dipengaruhikan, antara lain lokasi, ukuran, fasilitas.

Selama beberapa tahun terakhir, pendekatan machine learning menunjukkan potensi yang sangat besar untuk memperbaiki akurasi prediksi harga rumah. Algoritma Random Forest dapat mengolah hubungan non-linear dan interaksi kompleks antar fitur, membuat alat ini sebagai alat yang sangat berguna di dalam struktur prediktif harga rumah. Penelitian oleh Wiltshire (2022) mengindikasikan bahwa Random Forest Regression bisa saja memprediksi harga rumah secara efektif melihat dari lokasi dan properti feature, menghasilkan akurasi yang sangat tinggi di dalam prediksi harga.

Selain itu, proses seleksi fitur yang tepat (feature selection) juga berperan penting dalam menginisiasi performa model. Guo (2023) menegaskan bahwa proses seleksi fitur yang relevan dapat secara signifikan menambah akurasi prediksi harga rumah melalui pencabutan noise dan overfitting dalam.

Proyek ini membawa tujuan untuk mengembangkan model prediksi hargas rumah yang akurat dari dataset Ames Housing yang diciptakan oleh De Cock (2011) sebagai peletakan alternatif dari Boston Housing Dataset. Dengan mempergunakan teknik machine learning dan pemilihan feature yang tepat, proyek ini diharapkan dapat menentukan faktor utama yang mempengaruh hargas rumah dan menyajikan alat prediksi yang dapat diaplikasikan pada konteks dunia nyata."

### **📚 Daftar Referensi:**

- De Cock, D. (2011). Ames, Iowa: Alternative to the Boston Housing Data as an End of Semester Regression Project. Journal of Statistics Education, 19(3). https://doi.org/10.1080/10691898.2011.11889627

- Wiltshire, A. (2022). House Price Prediction using Random Forest Machine Learning Technique. Procedia Computer Science, 199, 806–813. https://doi.org/10.1016/j.procs.2022.01.100

- Guo, J. (2023). Feature Selection in House Price Prediction. Highlights in Business, Economics and Management, 21. https://drpress.org/ojs/index.php/HBEM/article/view/14755
## **🎯 Business Understanding**

**📌 Problem Statements**
- Bagaimana cara memprediksi harga rumah berdasarkan fitur-fitur yang tersedia?
- Fitur apa yang paling berpengaruh terhadap harga rumah?

**🎯 Goals**
- Membangun model machine learning untuk memprediksi harga rumah.
- Mengidentifikasi fitur-fitur yang memiliki kontribusi besar terhadap harga.

**💡 Solution Statements**
- Membangun dua model: Linear Regression sebagai baseline dan Random Forest Regressor sebagai model advanced.
- Evaluasi dilakukan dengan metrik R² Score dan Cross-validation untuk menilai generalisasi model.

## **📊 Data Understanding**

Dataset yang digunakan dalam proyek ini adalah dataset "Ames Housing" yang dapat diakses dari https://www.kaggle.com/datasets/prevek18/ames-housing-dataset. Dataset ini terdiri dari berbagai fitur yang menjelaskan kondisi, ukuran, lokasi, dan karakteristik rumah.

**🧾 Penjelasan Fitur**
- OverallQual : Kualitas material dan hasil akhir rumah secara keseluruhan.
- GrLivArea : Luas area tempat tinggal di atas tanah (dalam kaki persegi).
- YearBuilt : Tahun rumah dibangun.
- GarageCars : Kapasitas garasi dalam jumlah mobil.

Dataset ini terdiri dari 82 kolom fitur dan 1 kolom target yaitu SalePrice yang merupakan harga jual rumah.

## **🧹 Data Preparation**

**🧼 1. Data Cleaning**

Langkah-langkah pembersihan data yang dilakukan:
- Mengisi missing value numerik dengan nilai median.
- Menghapus kolom yang memiliki banyak missing value atau tidak relevan seperti Alley, Pool QC, Fence, dan Misc Feature.
-Mengisi missing value kategorikal dengan nilai modus.

**⚙️ 2. Data Preprocessing**

- Mengubah variabel kategorikal menjadi numerik menggunakan One Hot Encoding dengan drop_first=True untuk menghindari dummy variable trap.

**🛠️ 3.Feature Engineering**

Salah satu langkah yang dilakukan dalam tahap feature engineering adalah membuat fitur baru yang dapat memberikan informasi tambahan bagi model. Dalam hal ini, dibuat fitur House_Age yang merepresentasikan umur rumah pada saat dijual. Fitur ini dihitung dari selisih antara tahun penjualan rumah (Yr Sold) dan tahun rumah dibangun (Year Built).

Tujuan dari pembuatan fitur ini adalah agar model dapat lebih mudah mengenali pengaruh umur bangunan terhadap harga jual rumah. Setelah fitur House_Age ditambahkan, kolom asli Year Built dihapus dari data karena informasinya telah terwakili oleh fitur baru tersebut dan untuk menghindari duplikasi informasi (redundancy).


## **🧠 Modeling**

Dalam tahap ini, dilakukan beberapa langkah untuk membangun dan mengevaluasi model prediksi harga rumah.

### **1. Split Data 🧪**

Pertama, data dipisahkan menjadi fitur dan target, kemudian dibagi menjadi data latih dan data uji dengan perbandingan 80:20. Pemisahan ini dilakukan untuk memastikan bahwa model dapat diuji pada data yang belum pernah dilihat sebelumnya, sehingga performanya lebih objektif.

### **2. Baseline Model – Linear Regression 📉**

Model pertama yang digunakan adalah **Linear Regression** sebagai baseline. Model ini dilatih menggunakan data latih, lalu diuji menggunakan data uji untuk mendapatkan metrik awal performa. Hasilnya digunakan sebagai pembanding untuk model lanjutan.

Model ini menghasilkan:

* **Root Mean Squared Error (RMSE)** sebesar **29,152.88**
* **R² Score** sebesar **0.894**

### **3. Advanced Model – Random Forest Regressor🌲**

Selanjutnya, digunakan **Random Forest Regressor** tanpa hyperparameter tuning (menggunakan parameter default). Model ini dianggap lebih mampu menangkap kompleksitas hubungan antar fitur.

Model ini menghasilkan:

* **Root Mean Squared Error (RMSE)** sebesar **26,527.25**
* **R² Score** sebesar **0.912**


### 4. **📈 Evaluation**
Model dievaluasi menggunakan metrik R² Score, yang menunjukkan seberapa baik varians target bisa dijelaskan oleh fitur.

Hasil evaluasi:

- Linear Regression (R²): 0.60

- Random Forest (R² pada data uji): 0.81

- Cross-validation scores (R²): [0.90, 0.92, 0.87, 0.82, 0.90]

- Rata-rata R² CV: 0.886

Nilai ini menunjukkan bahwa model mampu menjelaskan sekitar 88.6% dari variasi harga rumah, yang berarti model memiliki performa yang cukup baik dan dapat diandalkan.

**📊 Interpretasi**:
Model Random Forest secara konsisten menghasilkan skor yang lebih tinggi dibandingkan Linear Regression, menunjukkan bahwa ia lebih mampu menangkap kompleksitas dalam data.

## 5. **🔍 Interpretasi Feature Importance 🌟**

Berdasarkan model Random Forest, fitur-fitur yang paling berpengaruh terhadap harga rumah adalah:

1. **Overall Qual** – Fitur ini memiliki skor kepentingan tertinggi, menunjukkan bahwa kualitas keseluruhan rumah merupakan faktor paling dominan dalam menentukan harga. Ini mencerminkan kondisi material dan finishing rumah secara umum.
2. **Gr Liv Area** – Luas ruang tinggal di atas tanah juga sangat berpengaruh. Semakin besar luas ruang tinggal, biasanya harga rumah juga semakin tinggi.
3. **1st Flr SF** – Luas lantai pertama menjadi indikator penting, karena biasanya merupakan area utama tempat tinggal.
4. **Total Bsmt SF** dan **BsmtFin SF 1** – Luas basement, baik yang selesai dibangun (finished) maupun total luasnya, juga memengaruhi harga rumah. Rumah dengan basement yang layak dan fungsional memiliki nilai jual lebih tinggi.
5. **2nd Flr SF** – Luas lantai dua menunjukkan besarnya rumah secara vertikal, yang juga berkontribusi pada harga.
6. **Full Bath** – Jumlah kamar mandi lengkap turut menjadi pertimbangan penting bagi pembeli rumah.
7. **Lot Area** – Luas tanah tempat rumah berdiri memengaruhi harga, terutama di lokasi premium.
8. **Garage Area** dan **Garage Cars** – Fitur garasi baik dari segi luas maupun kapasitas mobil berpengaruh terhadap nilai rumah.
9. **House\_Age** – Umur rumah (hasil rekayasa fitur) juga memberikan kontribusi terhadap harga; rumah yang lebih baru biasanya memiliki harga lebih tinggi.
10. **PID** – Meskipun ini merupakan kode identifikasi properti, bisa jadi memiliki korelasi tidak langsung terhadap harga, misalnya karena terkait lokasi tertentu.
11. **Year Remod/Add** – Tahun renovasi atau penambahan ruang menunjukkan kondisi pembaruan rumah, yang berpengaruh terhadap nilainya.
12. **Mas Vnr Area** – Luas veneer batu (hiasan batu bata di eksterior) juga berkontribusi sebagai aspek estetika rumah.
13. **Lot Frontage** – Panjang sisi properti yang berbatasan dengan jalan juga turut memengaruhi harga, terutama dari sisi tampilan depan rumah.

Fitur **Overall Qual** tampak jauh lebih dominan dibandingkan fitur lainnya, yang menegaskan pentingnya kualitas keseluruhan dalam menilai harga rumah. Hal ini juga mengindikasikan bahwa peningkatan kualitas finishing atau material bisa berdampak besar terhadap nilai properti 🔧🏠
