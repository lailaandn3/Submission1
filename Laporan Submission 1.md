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
- Menggunakan metrik R² Score dan Cross-validation untuk mengevaluasi performa model.

## **📊 Data Understanding**

Dataset yang digunakan dalam proyek ini adalah dataset "Ames Housing" yang dapat diakses dari https://www.kaggle.com/datasets/prevek18/ames-housing-dataset. Dataset ini terdiri dari berbagai fitur yang menjelaskan kondisi, ukuran, lokasi, dan karakteristik rumah.

### Jumlah Data

- Total data: 2930

- Total fitur: 82 kolom fitur (fitur prediktor) + 1 kolom target (SalePrice)

### Kondisi Data

- Missing Values
Beberapa fitur memiliki missing value, misalnya fitur Alley, Pool QC, Fence, dan Misc Feature yang memiliki missing value cukup banyak

- Duplikat
    Dari pengecekan `df.duplicated().sum()` ditemukan tidak ada data duplikat pada dataset.

- Tipe Data
    Dataset terdiri dari tipe data numerik dan kategorikal. Variabel kategorikal diubah menjadi variabel numerik melalui teknik One Hot Encoding sebelum modeling.

- Uraian Fitur Dataset Ames Housing

| No. | Nama Fitur      | Deskripsi Singkat                                               |
| --- | --------------- | --------------------------------------------------------------- |
| 1   | Order           | Nomor urut data                                                 |
| 2   | PID             | ID unik properti                                                |
| 3   | MS SubClass     | Kategori jenis bangunan                                         |
| 4   | MS Zoning       | Zona penggunaan lahan                                           |
| 5   | Lot Frontage    | Panjang sisi properti yang berbatasan dengan jalan              |
| 6   | Lot Area        | Luas tanah (dalam sqft)                                         |
| 7   | Street          | Tipe permukaan jalan (contoh: Paved, Gravel)                    |
| 8   | Alley           | Jenis gang belakang (jika ada)                                  |
| 9   | Lot Shape       | Bentuk lahan (contoh: Regular, IR1)                             |
| 10  | Land Contour    | Kondisi kontur tanah (contoh: Flat, Low)                        |
| 11  | Utilities       | Ketersediaan utilitas (air, listrik, dll)                       |
| 12  | Lot Config      | Konfigurasi lot (Corner, Inside, dll)                           |
| 13  | Land Slope      | Tingkat kemiringan tanah                                        |
| 14  | Neighborhood    | Lingkungan atau kawasan tempat rumah berada                     |
| 15  | Condition 1     | Kondisi rumah terhadap fasilitas utama                          |
| 16  | Condition 2     | Kondisi rumah terhadap fasilitas sekunder                       |
| 17  | Bldg Type       | Tipe bangunan utama (1Fam, 2fmCon, Duplx, dll)                  |
| 18  | House Style     | Gaya rumah (1Story, 2Story, Split, dll)                         |
| 19  | Overall Qual    | Penilaian kualitas keseluruhan rumah (skala 1–10)               |
| 20  | Overall Cond    | Penilaian kondisi keseluruhan rumah (skala 1–10)                |
| 21  | Year Built      | Tahun rumah dibangun                                            |
| 22  | Year Remod/Add  | Tahun renovasi/penambahan terakhir                              |
| 23  | Roof Style      | Tipe atap                                                       |
| 24  | Roof Matl       | Bahan atap                                                      |
| 25  | Exterior 1st    | Material eksterior utama                                        |
| 26  | Exterior 2nd    | Material eksterior kedua                                        |
| 27  | Mas Vnr Type    | Jenis veneer batu pada dinding rumah                            |
| 28  | Mas Vnr Area    | Luas veneer batu                                                |
| 29  | Exter Qual      | Kualitas eksterior rumah                                        |
| 30  | Exter Cond      | Kondisi eksterior rumah                                         |
| 31  | Foundation      | Jenis pondasi rumah                                             |
| 32  | Bsmt Qual       | Kualitas basement                                               |
| 33  | Bsmt Cond       | Kondisi basement                                                |
| 34  | Bsmt Exposure   | Pencahayaan basement (jendela)                                  |
| 35  | BsmtFin Type 1  | Jenis penyelesaian basement 1                                   |
| 36  | BsmtFin SF 1    | Luas basement dengan tipe 1                                     |
| 37  | BsmtFin Type 2  | Jenis penyelesaian basement 2                                   |
| 38  | BsmtFin SF 2    | Luas basement dengan tipe 2                                     |
| 39  | Bsmt Unf SF     | Luas basement yang belum selesai (unfinished)                   |
| 40  | Total Bsmt SF   | Total luas basement                                             |
| 41  | Heating         | Jenis sistem pemanas rumah                                      |
| 42  | Heating QC      | Kualitas sistem pemanas                                         |
| 43  | Central Air     | Ada/tidaknya AC sentral                                         |
| 44  | Electrical      | Sistem kelistrikan rumah                                        |
| 45  | 1st Flr SF      | Luas lantai 1                                                   |
| 46  | 2nd Flr SF      | Luas lantai 2                                                   |
| 47  | Low Qual Fin SF | Luas bagian rumah dengan kualitas rendah                        |
| 48  | Gr Liv Area     | Luas total area tinggal di atas tanah                           |
| 49  | Bsmt Full Bath  | Jumlah kamar mandi penuh di basement                            |
| 50  | Bsmt Half Bath  | Jumlah kamar mandi setengah di basement                         |
| 51  | Full Bath       | Jumlah kamar mandi penuh di atas tanah                          |
| 52  | Half Bath       | Jumlah kamar mandi setengah di atas tanah                       |
| 53  | Bedroom AbvGr   | Jumlah kamar tidur di atas tanah                                |
| 54  | Kitchen AbvGr   | Jumlah dapur                                                    |
| 55  | Kitchen Qual    | Kualitas dapur                                                  |
| 56  | TotRms AbvGrd   | Total jumlah ruangan di atas tanah (tidak termasuk kamar mandi) |
| 57  | Functional      | Fungsi rumah apakah normal atau tidak                           |
| 58  | Fireplaces      | Jumlah perapian                                                 |
| 59  | Fireplace Qu    | Kualitas perapian                                               |
| 60  | Garage Type     | Jenis garasi                                                    |
| 61  | Garage Yr Blt   | Tahun garasi dibangun                                           |
| 62  | Garage Finish   | Tingkat penyelesaian garasi                                     |
| 63  | Garage Cars     | Kapasitas garasi dalam jumlah mobil                             |
| 64  | Garage Area     | Luas garasi                                                     |
| 65  | Garage Qual     | Kualitas garasi                                                 |
| 66  | Garage Cond     | Kondisi garasi                                                  |
| 67  | Paved Drive     | Apakah jalan masuk rumah beraspal                               |
| 68  | Wood Deck SF    | Luas dek kayu                                                   |
| 69  | Open Porch SF   | Luas teras terbuka                                              |
| 70  | Enclosed Porch  | Luas teras tertutup                                             |
| 71  | 3Ssn Porch      | Luas 3-season porch (ruang tambahan semi outdoor)               |
| 72  | Screen Porch    | Luas teras berpagar kawat nyamuk                                |
| 73  | Pool Area       | Luas kolam renang                                               |
| 74  | Pool QC         | Kualitas kolam renang                                           |
| 75  | Fence           | Jenis pagar rumah                                               |
| 76  | Misc Feature    | Fitur tambahan lain (seperti lift, gudang kecil, dll)           |
| 77  | Misc Val        | Nilai fitur tambahan                                            |
| 78  | Mo Sold         | Bulan penjualan rumah                                           |
| 79  | Yr Sold         | Tahun penjualan rumah                                           |
| 80  | Sale Type       | Tipe penjualan rumah                                            |
| 81  | Sale Condition  | Kondisi penjualan rumah                                         |
| 82  | SalePrice       | Harga jual rumah (target variabel)                              |


### **🔎 Exploratory Data Analysis (EDA)**

Sebelum melakukan modeling, dilakukan exploratory data analysis untuk memahami struktur dan karakteristik data yang digunakan. Beberapa langkah EDA yang dilakukan antara lain:

- Melihat ringkasan informasi dataset menggunakan fungsi df.info() untuk mengidentifikasi tipe data dan jumlah missing value pada setiap kolom. Dari hasil ini diketahui terdapat beberapa fitur dengan missing value cukup banyak seperti Alley, Mas Vnr Type, dan lain-lain.

- Melakukan analisis statistik deskriptif pada fitur numerik untuk memahami distribusi nilai, seperti mean, median, standar deviasi, serta pengecekan nilai minimum dan maksimum.

- Dataset ini terdiri dari 82 kolom fitur dan 1 kolom target yaitu SalePrice yang merupakan harga jual rumah.

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

**4. Split Data 🧪**

Data dipisahkan menjadi fitur dan target, kemudian dibagi menjadi data latih dan data uji dengan perbandingan 80:20. Pemisahan ini dilakukan untuk memastikan bahwa model dapat diuji pada data yang belum pernah dilihat sebelumnya, sehingga performanya lebih objektif.


## 🧠 **Modeling**

Pada tahap ini, dilakukan pemilihan dan pengembangan algoritma machine learning untuk membangun model prediksi harga rumah. Dua algoritma utama digunakan, yaitu **Linear Regression** sebagai baseline dan **Random Forest Regressor** sebagai model lanjutan yang lebih kompleks.

---

### **1. Baseline Model – Linear Regression 📉**

**Linear Regression** adalah metode statistik yang digunakan untuk memodelkan hubungan linear antara satu atau lebih variabel independen (fitur) dan variabel dependen (harga rumah).

* **Konsep kerja:** Model mencari garis lurus terbaik yang meminimalkan selisih kuadrat antara nilai prediksi dan nilai aktual (*least squares method*).

* **Parameter utama:**

  * `fit_intercept`: menentukan apakah model harus menghitung intersep.
  * `normalize`: apakah fitur akan dinormalisasi sebelum regresi (tergantung implementasi).
  * `copy_X`: apakah akan membuat salinan data input.
  * `n_jobs`: jumlah core untuk paralelisasi jika didukung.

* **Kelebihan:**

  * Sederhana dan mudah diimplementasikan.
  * Cepat dilatih pada dataset dengan ukuran kecil hingga sedang.
  * Hasilnya mudah diinterpretasi karena berbentuk persamaan linear.

* **Kekurangan:**

  * Hanya mampu menangkap hubungan linier antar variabel.
  * Sensitif terhadap outlier.
  * Performa kurang baik pada data yang kompleks atau non-linear.

---

### **2. Advanced Model – Random Forest Regressor 🌲**

**Random Forest Regressor** merupakan algoritma *ensemble* berbasis decision tree yang digunakan untuk menangani masalah regresi dengan pendekatan yang lebih kompleks.

* **Konsep kerja:**

  * Membuat banyak decision tree dari subset acak data (*bootstrap sampling*).
  * Setiap pohon memberikan prediksi, lalu hasil akhir diambil rata-ratanya.
  * Teknik ini mengurangi varians dan meningkatkan generalisasi model.

* **Parameter utama:**

  * `n_estimators`: jumlah pohon dalam hutan.
  * `max_depth`: kedalaman maksimum setiap pohon.
  * `min_samples_split`: jumlah minimum sampel untuk membagi node.
  * `min_samples_leaf`: jumlah minimum sampel pada daun.
  * `random_state`: untuk hasil yang konsisten (reproducible).
  * `max_features`: jumlah maksimum fitur yang dipertimbangkan saat membagi node.

* **Kelebihan:**

  * Mampu menangani hubungan non-linear antar fitur.
  * Relatif tahan terhadap outlier dan overfitting.
  * Dapat digunakan untuk menentukan pentingnya fitur (feature importance).

* **Kekurangan:**

  * Interpretasi model lebih kompleks dibandingkan linear regression.
  * Waktu pelatihan dan komputasi lebih lama, terutama jika jumlah pohon besar.
  * Bisa menjadi "black-box" jika tidak ditelusuri dengan metode interpretasi tambahan.


## **📊 Evaluation**

### **🔢 Metrik Evaluasi yang Digunakan**

Evaluasi model dilakukan dengan menggunakan metrik:

* **Root Mean Squared Error (RMSE)**: Mengukur seberapa besar deviasi rata-rata prediksi dari nilai sebenarnya dalam satuan harga rumah. Nilai RMSE yang lebih kecil berarti prediksi model lebih akurat.

* **R² Score (Coefficient of Determination)**: Menunjukkan seberapa besar variabilitas data target yang dapat dijelaskan oleh model. Semakin mendekati 1, semakin baik model dalam menjelaskan variansi harga rumah.

### **📊 Hasil Evaluasi Model**

| Model                   | RMSE      | R² Score | Cross-Validation (mean R²) |
| ----------------------- | --------- | -------- | -------------------------- |
| Linear Regression       | 29,152.88 | 0.894    | -                          |
| Random Forest Regressor | 26,527.25 | 0.912    | 0.886                      |

Dari tabel di atas, terlihat bahwa Random Forest Regressor secara konsisten memberikan performa yang lebih baik dibandingkan Linear Regression, baik dari sisi error prediksi maupun kemampuan generalisasi.

### **🔁 Analisis Cross-Validation**

Cross-validation 5-fold digunakan untuk mengevaluasi kestabilan performa model Random Forest. Berikut adalah skor R² untuk setiap fold:

```
[0.9043, 0.9269, 0.8719, 0.8243, 0.9042]
```

Nilai rata-rata R² adalah **0.886**, dengan variasi yang relatif kecil, menunjukkan bahwa model cukup stabil terhadap perbedaan data.

### **🔍 Interpretasi Feature Importance 🌟**

Berdasarkan model Random Forest, fitur-fitur yang paling berpengaruh terhadap harga rumah adalah:
![Visualisasi Feature Importance](https://raw.githubusercontent.com/lailaandn3/Submission1/b3feaa37d757328010b3d313d910d46c40303f21/download.png) 

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


### **Kesimpulan**

Berdasarkan hasil evaluasi, **Random Forest Regressor** menunjukkan performa yang lebih baik dan stabil dibandingkan Linear Regression. Oleh karena itu, model ini dipilih sebagai solusi akhir dalam memprediksi harga rumah.


