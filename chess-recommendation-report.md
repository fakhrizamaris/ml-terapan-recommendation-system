# Laporan Proyek Machine Learning - Sistem Rekomendasi Opening Catur

## Project Overview

Proyek sistem rekomendasi opening catur bertujuan memecahkan tantangan kompleks dalam strategi permainan catur. Pentingnya proyek ini terletak pada:
- Memberikan wawasan strategis bagi pemain catur
- Mengoptimalkan pemilihan pembukaan berdasarkan data
- Mendukung pengembangan keterampilan taktis

## Business Understanding

### Problem Statements
1. Bagaimana menghasilkan rekomendasi opening catur yang personal?
2. Bagaimana mengintegrasikan preferensi pemain dengan analisis data historis?
3. Bagaimana mengembangkan sistem rekomendasi adaptif untuk rentang rating 1500-2200?

### Goals
1. Menghasilkan rekomendasi opening berbasis preferensi individual
2. Mengembangkan model prediksi yang akurat
3. Menyediakan strategi pembukaan yang sesuai dengan tingkat keterampilan pemain

### Solution Approach

#### Solution Statements
1. Content-Based Filtering
   - Teknik: TF-IDF Vectorization
   - Keunggulan: Rekomendasi berbasis konten spesifik
   - Metode: Cosine Similarity untuk pengukuran kesamaan

2. Collaborative Filtering
   - Teknik: Neural Network Recommender
   - Keunggulan: Learning dari pola kolektif
   - Model: Embedding layer dengan mekanisme bias

**Alasan Pendekatan**:
- Kombinasi dua metode untuk komprehensivitas
- Mengatasi keterbatasan masing-masing pendekatan
- Fleksibilitas dalam rekomendasi

## Data Understanding

**Sumber Data**: [[3]](https://www.kaggle.com/datasets/datasnaek/chess) Chess Game Dataset (Lichess)

**Statistik Utama**:
- Total permainan: Terdeteksi dalam dataset
- Rentang rating: 1500-2200
- Variabel kunci: opening archetype, rating pemain, hasil pertandingan

**Visualisasi Data**:
- Distribusi rating pemain
- Frekuensi penggunaan opening archetype
- Pola sebaran permainan

**Exploratory Data Analysis (EDA)**:
- Identifikasi distribusi rating
- Analisis frekuensi penggunaan opening
- Eksplorasi korelasi antar variabel

## Data Preparation

**Teknik Persiapan Data**:
1. Pembersihan Data
   - Hapus duplikasi
   - Filter rentang rating

2. Transformasi Fitur
   - Encoding user dan opening
   - Normalisasi rating

**Alasan Teknik**:
- Meningkatkan kualitas data
- Mempersiapkan untuk pemodelan
- Mengurangi noise

## Modeling

**Pendekatan Rekomendasi**:
1. Content-Based Filtering
   - Metode: TF-IDF Vectorization
   - Similarity: Cosine Similarity
   - Kelebihan: Personalisasi
   - Kekurangan: Keterbatasan eksplorasi

2. Collaborative Filtering
   - Model: Neural Network Recommender
   - Teknik: Embedding dengan bias
   - Kelebihan: Pola kolektif
   - Kekurangan: Cold start problem

**Komparasi Metode**:
- Analisis kelebihan dan kekurangan
- Pertimbangan kompleksitas
- Evaluasi performa

## Evaluation

**Metrik Evaluasi**: Root Mean Square Error (RMSE)

**Formula RMSE**:
```
RMSE = √(Σ(y_prediksi - y_aktual)² / n)
```

**Interpretasi**:
- Mengukur akurasi prediksi
- Menilai kualitas model
- Memvalidasi generalisasi

**Hasil**:
- Penurunan RMSE selama training
- Rekomendasi personal yang akurat
- Validasi model pada rentang rating spesifik

## Kesimpulan dan Rekomendasi

**Capaian**:
- Sistem rekomendasi opening catur berbasis AI
- Pendekatan multi-model
- Personalisasi berdasarkan data

**Pengembangan Lanjutan**:
- Integrasi fitur tambahan
- Perbaikan algoritma
- Eksplorasi model machine learning lanjutan

**Referensi Akademis**:
- [[1]](https://link.springer.com/chapter/10.1007/978-3-031-71694-2_29) J. Aryan and P. Avinash, "A Comprehensive Survey of Evaluation Techniques for Recommendation Systems", Computation of Artificial Intelligence and Machine Learning
(ICCAIML 2024), 2024, pp. 281–304.
- [[2]](https://www.sciencedirect.com/science/article/abs/pii/S0969698921000941#preview-section-abstract) C. Sydney,  
T. Pipat, and C. Punjaporn, "A tale of two recommender systems: The moderating role of consumer expertise on artificial intelligence based product recommendations", Journal of Retailing and Consumer Services, 2021.
- [[3]](https://www.kaggle.com/datasets/datasnaek/chess) Mitchell J., "Chess Game Dataset (Lichess)", Kaggle, 2024.