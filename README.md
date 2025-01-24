# Laporan Proyek Machine Learning - Fakhri Djamaris

## Domain Proyek

Analisis rekomendasi opening catur berdasarkan rentang rating pemain dari 1500-2200 merupakan aspek krusial dalam pengembangan strategi permainan catur. Studi yang dilakukan oleh Sydney et al. [2] menggarisbawahi pentingnya keahlian konsumen dalam sistem rekomendasi berbasis AI, yang secara langsung relevan dengan konteks rekomendasi opening catur.
Dalam riset tersebut, disorot bagaimana tingkat keahlian pengguna mempengaruhi efektivitas rekomendasi, sebuah konsep kunci dalam pengembangan sistem rekomendasi catur kami. Hal ini sangat sesuai dengan variasi tingkat keahlian pemain catur yang akan menggunakan sistem rekomendasi ini.

Pada riset jurnal berjudul _"A Comprehensive Survey of Evaluation Techniques for Recommendation Systems"_ [[1]](https://link.springer.com/chapter/10.1007/978-3-031-71694-2_29) menunjukkan bahwa sistem rekomendasi berbasis machine learning dapat secara signifikan meningkatkan pengalaman pengguna dalam memilih strategi.

## Business Understanding

### Problem Statements

1. Bagaimana menghasilkan rekomendasi opening catur yang personal?
2. Bagaimana mengintegrasikan preferensi pemain dengan analisis data historis?
3. Bagaimana mengembangkan sistem rekomendasi adaptif untuk rentang rating 1500-2200?

### Goals

1. Menghasilkan rekomendasi opening berbasis preferensi individual
2. Mengembangkan model prediksi yang akurat
3. Menyediakan strategi pembukaan yang sesuai dengan tingkat keterampilan pemain

### Solution Statements

1. Mengimplementasikan dua algoritma sistem rekomendasi:
   - Content-Based Filtering menggunakan TF-IDF
   - Collaborative Filtering dengan Neural Network
2. Melakukan optimasi model dengan:
   - Encoding fitur pengguna dan opening
   - Normalisasi rating
3. Menggunakan metrik RMSE untuk evaluasi model

## Data Understanding

### Kondisi Data

1. _Missing Value_: Tidak ditemukan nilai yang hilang pada dataset.
2. Duplikasi Data: Terdapat 945 data duplikat setelah pemeriksaan.
3. _Outlier_: Dilakukan analisis distribusi rating untuk memastikan kualitas data.


### Tautan Sumber Data
Dataset berasal dari Kaggle: _Chess Game Dataset (Lichess)_ [[3]](https://www.kaggle.com/datasets/datasnaek/chess)

### Variabel-variabel pada dataset:

1. id:
   - Tipe Data: Object
   - Deskripsi: id permainan catur

2. rated:
   - Tipe Data: Object
   - Deskripsi: appakah permainan catur di rating atau tidak

3. black_rating:
   - Tipe Data: Numerik
   - Deskripsi: Rating pemain hitam

4. black_id:
   - Tipe Data: Object
   - Deskripsi: id pemain hitam

5. winner:
   - Tipe Data: Kategorik
   - Deskripsi: Pemenang pertandingan

6. white_rating:
   - Tipe Data: Object
   - Deskripsi: Rating pemain putih

7. white_id:
   - Tipe Data: Object
   - Deskripsi: id pemain putih

8. increment_code:
   - Tipe Data: Kategorik
   - Deskripsi: Kode waktu pertandingan

9. turns:
   - Tipe Data: Numerik
   - Deskripsi: jumlah langkah permainan catur
   
10. moves:
   - Tipe Data: object
   - Deskripsi: pergerakan bidak catur

11. victory_status:
   - Tipe Data: Object
   - Deskripsi: Kode waktu pertandingan

12. opening_eco:
   - Tipe Data: Object
   - Deskripsi: _Encyclopaedia of Chess Openings_

13. opening_name:
   - Tipe Data: Object
   - Deskripsi: nama pembukaan catur

13. opening_ply:
   - Tipe Data: Object
   - Deskripsi: jumlah gerakan dalam pembukaan catur


## Exploratory Data Analysis (EDA)

#### Ringkasan Statistik

- Rentang rating: 1500-2200
- Jumlah unique opening: Teridentifikasi dalam analisis

#### Analisis Tren Data

Visualisasi mencakup:
- Distribusi rating pemain
![Distribusi rating pemain](https://github.com/user-attachments/assets/afb07d22-83ba-450c-b85f-8a10781b4986)
- Top 20 Pembukaan yang paling sering di mainkan
![top 20 openings](https://github.com/user-attachments/assets/d75b5d5e-298b-433a-a887-7479da0b4cf0)
- Pola sebaran permainan

#### Analisis Korelasi

- Identifikasi hubungan antar variabel
- Analisis frekuensi penggunaan opening berdasarkan rating
- Korelasi antara tipe opening dan hasil pertandingan

## Data Preparation

1. Pembersihan Data:
   - Hapus duplikasi
   - Filter rentang rating 1500-2200

2. Transformasi Fitur:
   - Encoding user dan opening
   - Normalisasi rating
   - Ekstraksi fitur opening

3. Pembagian Data:
   - Train-test split dengan rasio 80:20

### Data Preparation untuk Content-Based Filtering

1. Feature Selection

Dilakukan pemilihan fitur yang relevan untuk sistem rekomendasi opening catur
Fokus pada kolom 'opening_archetype' sebagai fitur utama untuk analisis
Kolom yang dipilih: 'opening_archetype', 'white_rating', 'black_rating', 'winner', dan 'increment_code'

2. TF-IDF Vectorization

Menggunakan TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengubah teks opening menjadi representasi numerik
TF-IDF membantu mengukur kepentingan setiap opening dalam dataset
Proses:

3. Mentransformasi teks opening menjadi vektor numerik

Menghitung bobot kepentingan setiap kata dalam opening
Menghasilkan matriks representasi fitur yang dapat digunakan untuk menghitung similaritas


### Data Preparation untuk Collaborative Filtering

1. Encoding Pengguna dan Opening

   Mengubah ID pengguna dan nama opening menjadi representasi numerik
Membuat dictionary mapping antara ID asli dan ID terkodekan
Proses encoding memungkinkan model memproses data secara efisien

2. Normalisasi Rating

   Melakukan normalisasi 'times_used' ke skala 0-1
Tujuan: Menyeragamkan rentang nilai untuk proses pelatihan model
Rumus normalisasi: (x - min_rating) / (max_rating - min_rating)

3. Pembagian Data Latih dan Validasi
- Pembagian data dengan rasio 80:20
- Menggunakan random sampling untuk memastikan distribusi data yang merata
- Memisahkan data input (user dan opening) dengan target (rating)

## Modeling

###  Content-Based Filtering :  Cosine Similarity

Tahap Pembuatan Model:
- Menggunakan TF-IDF Vectorization untuk mengubah teks opening menjadi vektor numerik
- Menghitung Cosine Similarity antara vektor opening

Cara Kerja Cosine Similarity:
1. Mengukur kesamaan antara dua vektor berdasarkan sudut di antara mereka
2. Nilai similarity berkisar antara 0-1
3. Semakin dekat nilainya ke 1, semakin mirip kedua opening tersebut

Proses Rekomendasi:

- Identifikasi opening yang paling banyak digunakan
- Temukan opening serupa menggunakan cosine similarity
- Urutkan rekomendasi berdasarkan skor kesamaan

- Prinsip algoritma: Rekomendasi berbasis kesamaan penggunaan
- Teknik: TF-IDF Vectorization
- Metode Similarity: Cosine Similarity
![download (4)](https://github.com/user-attachments/assets/45fb2bca-b422-44a1-bd93-62d99ffaddad)

- Kelebihan:
  - Personalisasi berdasarkan konten
  - Mudah diinterpretasi
- Keterbatasan:
  - Keterbatasan eksplorasi
  - Bergantung pada kualitas fitur

### Collaborative Filtering: Neural Network Recommender
1. Arsitektur Model:
   
- Embedding Layer untuk User dan Opening
- Dimensi Embedding: 50
- Regularisasi L2: 1e-6
- Activation Function: Sigmoid

2. Hyperparameter Training:

- Loss Function: Binary Crossentropy
- Optimizer: Adam
- Learning Rate: 0.001
- Batch Size: 64
- Epoch: 100

3. Cara Kerja Model:

- Belajar representasi embedding untuk user dan opening
- Memprediksi rating/preferensi berdasarkan interaksi user-opening
- Menghasilkan rekomendasi opening yang belum pernah dimainkan user

### Top-N Rekomendasi
Contoh Rekomendasi untuk User '--jim--':
1. Content-Based Filtering:
- Italian Game
- Queen's Gambit
- Sicilian Defense
- French Defense
- King's Indian Attack

2. Collaborative Filtering:

- Queen's Pawn Game
- Sicilian Defense
- King's Pawn Game
- French Defense
- Caro-Kann Defense
- Prinsip algoritma: Rekomendasi berbasis pola kolektif
- Model: Neural Network Recommender
- Teknik: Embedding layer dengan bias

Kelebihan:
  - Learning dari pola kolektif
  - Adaptif terhadap preferensi

Keterbatasan:
  - Cold start problem
  - Kompleksitas komputasi

## Evaluation

### Content-Based Filtering: Precision

Precision dihitung berdasarkan:
   - Jumlah opening relevan yang direkomendasikan
   - Total jumlah opening yang direkomendasikan


Rumus: Precision = (Jumlah Rekomendasi Relevan) / (Total Rekomendasi)

### Collaborative Filtering: RMSE

- RMSE Training: 0.23
- RMSE Validasi: 0.25
- Interpretasi: Model memiliki performa yang konsisten antara data latih dan validasi Nilai RMSE rendah menunjukkan prediksi yang akurat

#### Content Based Filtering
![Content Based Filtering](https://github.com/user-attachments/assets/b59a5704-013c-4e76-8591-4628f648c0e0)

#### Collaborative Filtering
![Screenshot 2025-01-23 093429](https://github.com/user-attachments/assets/0a12fdd4-8791-4aec-a0ea-e8b8c9770a69)


### Analisis Hasil

1. Evaluasi Keberhasilan Proyek:
   - Berhasil membangun dua model rekomendasi
   - Collaborative Filtering menunjukkan kinerja sedikit lebih baik
   - Kedua model memberikan rekomendasi yang dapat diandalkan

2. Pencapaian Tujuan:
   - Rekomendasi personal tercapai
   - Model mampu mengidentifikasi opening sesuai preferensi

3. Identifikasi Fitur Berpengaruh:
   - Rating pemain
   - Tipe opening
   - Frekuensi penggunaan opening

### Rekomendasi

1. Menggunakan kombinasi kedua model untuk rekomendasi komprehensif
2. Pelatihan ulang model secara berkala
3. Eksplorasi fitur tambahan untuk peningkatan akurasi
4. Pertimbangkan faktor eksternal seperti gaya bermain pemain

### Dampak terhadap Business Understanding
Problem Statements:

1. Rekomendasi Personal ✓
   - Kedua model menghasilkan rekomendasi berbasis preferensi individu

2. Integrasi Preferensi dan Data Historis ✓
   - Content-Based: Menggunakan karakteristik opening
   - Collaborative Filtering: Memanfaatkan pola historis pemain

3. Sistem Rekomendasi Adaptif (Rating 1500-2200) 
   - Filter data sesuai rentang rating
   - Model mampu memberikan rekomendasi spesifik

Goals:
1. Rekomendasi Personal 
2. Dapat memberikan saran yang sesuai diharapkan 
3. Strategi Opening Sesuai ECO (_Encyclopedia Chess Openings_) 

Solusi Statement:

1. Implementasi dual model berhasil
2. Encoding dan normalisasi efektif
3. RMSE rendah menunjukkan kualitas model

## Referensi

[1] J. Aryan and P. Avinash, "A Comprehensive Survey of Evaluation Techniques for Recommendation Systems", Computation of Artificial Intelligence and Machine Learning (ICCAIML 2024), 2024, pp. 281–304.

[2] C. Sydney, T. Pipat, and C. Punjaporn, "A tale of two recommender systems: The moderating role of consumer expertise on artificial intelligence based product recommendations", Journal of Retailing and Consumer Services, 2021.

[3] Mitchell J., "Chess Game Dataset (Lichess)", Kaggle, 2024.
