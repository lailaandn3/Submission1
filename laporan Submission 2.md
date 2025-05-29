# Laporan Proyek Machine Learning - Laila

## 📚 Project Overview

Sistem rekomendasi film merupakan salah satu aplikasi utama dari kecerdasan buatan yang digunakan untuk membantu pengguna menemukan konten yang relevan dari sekian banyak pilihan yang tersedia. Dengan meningkatnya jumlah konten digital, seperti film dan serial, pengguna sering kali merasa kesulitan dalam memilih tontonan yang sesuai dengan preferensi mereka. Sistem rekomendasi hadir untuk mengatasi masalah ini dengan menyarankan konten yang relevan berdasarkan data pengguna sebelumnya.

Dalam konteks ini, dua pendekatan utama yang digunakan adalah:

1. **Content-Based Filtering (CBF)**: Pendekatan ini merekomendasikan item berdasarkan kesamaan atribut atau konten dari item yang telah disukai pengguna sebelumnya. Misalnya, jika seorang pengguna menyukai film bergenre aksi, sistem akan merekomendasikan film aksi lainnya.

2. **Collaborative Filtering (CF)**: Pendekatan ini merekomendasikan item berdasarkan preferensi pengguna lain yang memiliki kesamaan minat. Misalnya, jika pengguna A dan B memiliki riwayat penilaian film yang serupa, maka film yang disukai B namun belum ditonton oleh A akan direkomendasikan kepada A.

Penelitian sebelumnya menunjukkan bahwa kombinasi dari kedua pendekatan ini dapat menghasilkan sistem rekomendasi yang lebih akurat dan personal. Sebagai contoh, sebuah studi mengembangkan sistem rekomendasi film yang menggabungkan teknik collaborative filtering dan content-based filtering untuk meningkatkan akurasi dan keberagaman rekomendasi (Kurniawan & Harahap, 2022).

Dengan latar belakang tersebut, proyek ini bertujuan untuk membangun dan mengevaluasi dua sistem rekomendasi film: satu berbasis content-based filtering dan satu lagi berbasis collaborative filtering, menggunakan dataset MovieLens yang terkenal. Pendekatan ini diharapkan dapat memberikan wawasan tentang efektivitas masing-masing metode dalam memberikan rekomendasi yang relevan bagi pengguna.

---

### Referensi

Kurniawan, D., & Harahap, F. (2022). Hybrid Movie Recommendation System Using Collaborative Filtering and Content-Based Filtering Techniques. *International Journal of Creative Research Thoughts*, 10(2), 3491-3501. Retrieved from [https://ijcrt.org/papers/IJCRT2402820.pdf](https://ijcrt.org/papers/IJCRT2402820.pdf)

## Business Understanding

### Problem Statements

* Sulitnya pengguna dalam menemukan film yang sesuai dengan preferensi pribadi di antara banyaknya pilihan film yang tersedia.
* Kebutuhan sistem rekomendasi yang mampu memberikan rekomendasi film relevan dan personal, baik berdasarkan konten film maupun perilaku pengguna.

### Goals 

* Membangun sistem rekomendasi film yang dapat memberikan rekomendasi personal berbasis konten film (genre).
* Membangun sistem rekomendasi berbasis perilaku pengguna menggunakan rating (collaborative filtering).
* Membandingkan hasil rekomendasi dari kedua metode untuk memberikan insight terbaik.

### Solution Approach

Dalam proyek ini, digunakan dua pendekatan utama untuk mencapai goals yang telah ditetapkan:

**1. Content-Based Filtering**

 Sistem merekomendasikan film berdasarkan kesamaan fitur genre film. Setiap film direpresentasikan dalam bentuk vektor biner yang menunjukkan genre-genre yang dimiliki film tersebut. Kemiripan antar film dihitung menggunakan cosine similarity sehingga film dengan genre yang serupa akan direkomendasikan kepada pengguna.

**2. Collaborative Filtering**

 Sistem menggunakan data rating dari pengguna untuk menemukan pola kesamaan rating antar film. Berdasarkan kemiripan pola rating antar pengguna, film-film yang disukai oleh pengguna lain dengan preferensi serupa dapat direkomendasikan. Metode ini juga menggunakan cosine similarity pada matriks user-film yang berisi rating.
 
## Data Understanding

Dataset yang digunakan dalam proyek ini merupakan bagian dari **MovieLens 100k Dataset**, yang dapat diakses dan diunduh secara gratis melalui tautan berikut:
[https://grouplens.org/datasets/movielens/100k/](https://grouplens.org/datasets/movielens/100k/)

Dalam proyek ini, fokus utama diberikan pada dua struktur data:

1. **Data film** dari `u.item` : berisi informasi tentang film dan genre
2. **Data rating** dari `u.data` : berisi data rating yang diberikan oleh pengguna terhadap film

### 📌 Struktur dan Informasi Dataset

1. **Dataset `movies`**

   * Jumlah entri: 1682 film
   * Kolom: 24 kolom, terdiri dari:

     * `movie_id`: ID unik untuk setiap film
     * `title`: Judul film
     * `release_date`: Tanggal rilis film
     * `video_release_date`: (semua nilai null)
     * `IMDb_URL`: URL ke halaman IMDb
     * 19 kolom genre: setiap kolom berupa nilai biner (1 jika film termasuk genre tersebut, 0 jika tidak)

2. **Dataset `ratings`**

   * Jumlah entri: 100.000 rating
   * Jumlah pengguna unik: 943 user
   * Kolom:

     * `user_id`: ID unik pengguna
     * `movie_id`: ID film yang diberi rating
     * `rating`: Nilai rating dari 1 hingga 5
     * `timestamp`: Waktu saat rating diberikan

### 🧹 Kondisi Data

* Dataset `movies`:

  * Terdapat **1 nilai null** pada kolom `release_date`
  * Seluruh nilai pada `video_release_date` adalah null
  * Terdapat **3 nilai null** pada kolom `IMDb_URL`
* Dataset `ratings`:

  * Tidak ditemukan missing value

### 🔎 Exploratory Data Analysis (EDA)

* Terdapat **1682 film unik**
* Terdapat **943 pengguna unik**
* Genre direpresentasikan dalam bentuk vektor biner yang mencakup 19 kategori genre (seperti Action, Comedy, Drama, dll.)
* Berikut beberapa visualisasi awal untuk memahami data lebih dalam:

---

#### 📊 1. Distribusi Rating Film

Visualisasi ini menunjukkan **frekuensi rating** dari 1 hingga 5:

* Rating **4** paling sering diberikan pengguna.
* Menunjukkan kecenderungan pengguna memberikan **rating tinggi**.

![Distribusi Rating](https://raw.githubusercontent.com/lailaandn3/Submission1/b437567db75c02259c757586715ce31273341fe4/rating.png) 

---

#### 📊 2. Jumlah Film per Genre

Grafik batang di bawah ini memperlihatkan jumlah film untuk masing-masing genre dalam dataset MovieLens 100k.

* Genre Drama dan Comedy merupakan genre dengan jumlah film terbanyak.

* Disusul oleh genre Action, Thriller, dan Romance.

* Genre seperti Western, Film-Noir, Fantasy, dan Unknown memiliki jumlah film yang jauh lebih sedikit dibandingkan genre lainnya.

![Distribusi genre](https://raw.githubusercontent.com/lailaandn3/Submission1/80dc1a312683624bcfb966258e5c5b10f0784385/genre.png) 
---

#### 📊 3. Top 10 Film dengan Jumlah Rating Terbanyak

Visualisasi ini menunjukkan **10 film dengan jumlah rating terbanyak**:

* **Star Wars (1977)** menjadi film paling populer dari segi rating.
* Mayoritas film berasal dari **era 1990-an** dengan genre dominan: **fiksi ilmiah**, **komedi**, dan **aksi**.

![Distribusi film](https://raw.githubusercontent.com/lailaandn3/Submission1/a76b9d059bce666aea4714f14b2c58820d9e372c/film.png) 



## Data Preparation

Tahapan *data preparation* dilakukan untuk membersihkan dan menyiapkan data agar siap digunakan dalam proses pembangunan model rekomendasi. Langkah-langkah yang dilakukan adalah sebagai berikut:

1. **Menghapus Kolom yang Tidak Relevan**
   Kolom `video_release_date` dihapus karena seluruh nilainya kosong, sehingga tidak memberikan informasi yang berguna dalam analisis. Selain itu, kolom `IMDb_URL` juga dihapus karena tidak digunakan dalam proses pemodelan atau analisis genre.

2. **Menghapus Baris dengan Nilai Kosong (Missing Values)**
   Terdapat satu baris pada kolom `release_date` yang memiliki nilai kosong. Baris ini dihapus agar tidak menimbulkan error atau bias dalam analisis data.

3. **Membuat Dataframe Baru untuk Informasi Genre**
   Untuk keperluan pemodelan berbasis konten, dibuat dataframe baru yang hanya berisi kolom `movie_id`, `title`, dan seluruh kolom genre. Setiap kolom genre berisi nilai biner (0 atau 1) yang merepresentasikan apakah suatu film memiliki genre tersebut. Representasi ini penting untuk menghitung kemiripan antar film berdasarkan fitur kontennya.

---

### **Alasan Dilakukan Data Preparation Ini**

* Menghapus kolom dan baris yang tidak relevan bertujuan agar data menjadi bersih dan hanya berisi informasi yang berguna.
* Fokus pada fitur genre dilakukan untuk mendukung metode *Content-Based Filtering*, di mana kesamaan antar film dihitung berdasarkan kesamaan fitur konten.
* Proses ini juga menghindari terjadinya noise atau error yang dapat mengganggu akurasi sistem rekomendasi.

## Modeling and Result

Pada tahap ini, dibuat dua sistem rekomendasi film dengan algoritma berbeda, yaitu Content-Based Filtering dan Collaborative Filtering, untuk mengatasi masalah rekomendasi film yang sesuai dengan preferensi pengguna.

#### 1. Content-Based Filtering

* **Deskripsi:** Sistem ini merekomendasikan film berdasarkan kemiripan konten film, dalam hal ini menggunakan fitur genre yang direpresentasikan sebagai vektor biner.
* **Proses:**

  * Fitur genre dari dataset film diambil dan dihitung kemiripannya menggunakan cosine similarity antar film.
  * Sistem akan merekomendasikan film-film yang memiliki genre mirip dengan film input pengguna.
* **Output:**
  Misalnya untuk film "Toy Story (1995)", sistem memberikan rekomendasi 5 film mirip seperti "Aladdin (1992)" dan "Goofy Movie, A (1995)".
* **Kelebihan:**

  * Mudah dipahami dan diimplementasikan.
  * Tidak bergantung pada data pengguna yang lengkap.
* **Kekurangan:**

  * Tidak mampu memberikan rekomendasi yang memperhitungkan preferensi pengguna secara personal secara menyeluruh.
  * Terbatas pada fitur konten yang tersedia (genre saja).

#### 2. Collaborative Filtering

* **Deskripsi:** Sistem ini merekomendasikan film berdasarkan pola rating pengguna terhadap film-film lain yang serupa.
* **Proses:**

  * Data rating pengguna diubah menjadi matriks user-film.
  * Kemiripan antar film dihitung berdasarkan cosine similarity pada matriks rating tersebut.
  * Film-film yang paling mirip berdasarkan rating pengguna serupa akan direkomendasikan.
* **Output:**
  Untuk film "Toy Story (1995)", sistem merekomendasikan film seperti "Star Wars (1977)", "Independence Day (1996)", dan "Mission: Impossible (1996)".
* **Kelebihan:**

  * Mempertimbangkan preferensi pengguna yang sebenarnya melalui data rating.
  * Bisa memberikan rekomendasi yang lebih personal dan variatif.
* **Kekurangan:**

  * Membutuhkan data rating pengguna yang cukup banyak dan lengkap.
  * Rentan terhadap masalah cold start untuk film baru atau pengguna baru yang belum punya data rating.

#### Top-N Recommendation Output

Berikut adalah top-5 hasil rekomendasi dari dua pendekatan sistem rekomendasi yang telah dibangun:

🎬 Content-Based Filtering

![Content-Based Filtering](https://raw.githubusercontent.com/lailaandn3/Submission1/5caf6453f7cc7852302f5dddb3770d6e1a730791/Screenshot%202025-05-29%20090312.png)


🤝 Collaborative Filtering

![Collaborative Filtering](https://raw.githubusercontent.com/lailaandn3/Submission1/5caf6453f7cc7852302f5dddb3770d6e1a730791/Screenshot%202025-05-29%20090333.png)

## Evaluasi

Setelah membangun dua model rekomendasi, yaitu Content-Based Filtering dan Collaborative Filtering, kami melakukan evaluasi untuk mengukur performa masing-masing model menggunakan metrik Precision\@5, Recall\@5, dan RMSE (hanya untuk Collaborative Filtering).

**1. Content-Based Filtering**

* **Precision\@5 = 0.60**
  Artinya, dari 5 film yang direkomendasikan, 60% merupakan film yang benar-benar disukai oleh pengguna. Ini menunjukkan model mampu memilih film yang relevan berdasarkan kesamaan genre.

* **Recall\@5 = 1.00**
  Model berhasil merekomendasikan semua film yang disukai pengguna dalam batas 5 rekomendasi. Hal ini menunjukkan model sangat sensitif dan tidak melewatkan film favorit pengguna.

**2. Collaborative Filtering**

* **RMSE = 0.283**
  Root Mean Squared Error (RMSE) menunjukkan seberapa dekat prediksi rating dengan rating asli. Nilai RMSE yang kecil seperti 0.283 berarti model mampu memprediksi rating dengan akurasi yang cukup baik.

* **Precision\@5 = 0.60 dan Recall\@5 = 1.00**
  Mirip dengan content-based, collaborative filtering juga mampu merekomendasikan film yang sesuai preferensi pengguna dengan tingkat akurasi yang baik.

### Kesimpulan

Kedua model memberikan hasil rekomendasi yang cukup baik, dengan kelebihan dan kekurangan masing-masing. Content-Based Filtering unggul dalam merekomendasikan film berdasarkan kesamaan fitur genre, sedangkan Collaborative Filtering memanfaatkan pola rating pengguna lain untuk memberikan rekomendasi yang relevan.



