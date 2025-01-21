# MusicRecommendation

# Project Overview
Rekomendasi musik adalah salah satu tantangan besar dalam bidang teknologi informasi, terutama bagi platform musik digital yang menawarkan berbagai macam lagu. Sistem rekomendasi musik menggunakan teknik machine learning untuk mempersonalisasi pengalaman pengguna dengan memberikan saran lagu berdasarkan preferensi atau perilaku pengguna sebelumnya. Salah satu metode populer dalam sistem rekomendasi adalah Content-Based Filtering, yang memberikan rekomendasi berdasarkan kesamaan atribut konten musik.

Pentingnya sistem rekomendasi musik adalah untuk meningkatkan pengalaman pengguna di platform streaming musik dengan memberikan lagu yang relevan dengan preferensi mereka. Sistem yang baik akan meningkatkan interaksi dan retensi pengguna pada platform, yang berdampak pada pendapatan dan pengembangan platform tersebut.

Referensi data : https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset/data

# Business Understanding
**Problem Statement**
- Bagaimana cara mengatasi masalah keberagaman genre dan preferensi musik pengguna yang beragam?
- Bagaimana cara mengatasi user yang bosan dengan lagu tidak trendy?

**Goals**
- Meningkatkan pengalaman pengguna dengan menyarankan lagu-lagu yang sesuai dengan preferensi musik mereka.
- Memberikan rekomendasi lagu kepada pengguna berdasarkan input lagu tertentu dari popularitas yang sama

**Solution statements**
- Content-Based Filtering menggunakan Cosine Similarity:
  ```
  Sistem ini menganalisis fitur-fitur teknikal dari lagu seperti tempo, loudness, dan danceability untuk mencari kesamaan antara lagu yang dimasukkan dan lagu lainnya.
  Setiap lagu dipetakan sebagai vektor dalam ruang fitur, dan rekomendasi diberikan berdasarkan kemiripan antar vektor fitur.
  ```
  ini berfungsi untuk mendapatkan lagu yang mirip dengan kategori yang dipilih sebelumnya.
- Collaborative Filtering (SVD):
  ```
  Rekomendasi berdasarkan interaksi antara pengguna dan lagu-lagu, dipecah menggunakan Singular Value Decomposition (SVD) untuk menemukan pola tersembunyi dalam matriks interaksi
  ```
  ini berfungsi untuk memberikan insight lagu baru dengan kemiripan terkait popularitas dari lagu mereka.
  
# Data Understanding
Dataset yang digunakan adalah dataset lagu dengan informasi berikut:
```
track_id: ID unik untuk setiap lagu.
artists: Nama artis atau grup yang menyanyikan lagu.
album_name: Nama album tempat lagu tersebut berada.
track_name: Nama lagu.
popularity: Popularitas lagu berdasarkan streaming.
duration_ms: Durasi lagu dalam milidetik.
explicit: Menandakan apakah lagu tersebut mengandung konten eksplisit (ya/tidak).
danceability: Seberapa mudah lagu untuk ditarikan (skala 0–1).
energy: Energi dalam lagu (skala 0–1).
loudness: Volume rata-rata lagu dalam decibel.
speechiness: Seberapa banyak elemen berbicara dalam lagu.
acousticness: Seberapa alami atau akustik suara dalam lagu.
instrumentalness: Seberapa banyak instrumental dalam lagu.
liveness: Seberapa banyak elemen live dalam lagu.
valence: Suasana hati dari lagu (positif atau negatif).
tempo: Kecepatan lagu dalam BPM (beats per minute).
time_signature: Indikator tanda birama musik.
track_genre: Genre musik dari lagu.
Jumlah data yang digunakan adalah sekitar 20.000 baris untuk menjaga performa dan efisiensi sistem rekomendasi.
```

# Data Preparation
Pada tahap ini, data yang diproses meliputi penghapusan nilai yang hilang, penghapusan data duplikat, dan normalisasi fitur numerik agar semua fitur memiliki rentang yang seragam.

**Langkah-langkah Data Preparation:**
 - Menghapus Nilai Hilang: Data yang memiliki nilai kosong (missing values) akan dihapus agar tidak mempengaruhi analisis dan model.
 - Menghapus Duplikat: Data yang duplikat akan dihapus untuk menghindari redundansi dalam dataset.
 - Normalisasi Data: Menggunakan StandardScaler untuk menstandarkan data numerik (seperti danceability, energy, loudness) sehingga memiliki distribusi yang seragam dan mempercepat konvergensi model.
 - Subset Data: Hanya 20.000 baris pertama yang digunakan untuk mempercepat proses pelatihan dan evaluasi model.

# Modelling
Model yang digunakan untuk sistem rekomendasi ini adalah Content-Based Filtering dengan menggunakan Cosine Similarity.
Model 1 : 
- Content-Based Filtering dengan Cosine Similarity: Model pertama yang dibangun adalah Content-Based Filtering menggunakan Cosine Similarity untuk menghitung kesamaan antar lagu berdasarkan fitur teknikal seperti tempo, loudness, energy, dan lainnya.
- Cosine Similarity digunakan untuk mengukur kedekatan vektor fitur lagu yang dimasukkan oleh pengguna dengan vektor fitur lagu lainnya.
Model 2:
- Sebuah model Singular Value Decomposition (SVD) diterapkan pada matriks interaksi pengguna-lagu (matriks pengguna x lagu).
- Dengan SVD, kita dapat mengurangi dimensi matriks interaksi dan menemukan pola tersembunyi antara pengguna dan lagu. Dengan demikian, rekomendasi berbasis perilaku pengguna dapat dilakukan.

Collaborative Filtering dengan SVD:

Sebuah model Singular Value Decomposition (SVD) diterapkan pada matriks interaksi pengguna-lagu (matriks pengguna x lagu).
Dengan SVD, kita dapat mengurangi dimensi matriks interaksi dan menemukan pola tersembunyi antara pengguna dan lagu. Dengan demikian, rekomendasi berbasis perilaku pengguna dapat dilakukan.

Sebuah model Singular Value Decomposition (SVD) diterapkan pada matriks interaksi pengguna-lagu (matriks pengguna x lagu).
Dengan SVD, kita dapat mengurangi dimensi matriks interaksi dan menemukan pola tersembunyi antara pengguna dan lagu. Dengan demikian, rekomendasi berbasis perilaku pengguna dapat dilakukan.

# Evaluasi 
1. Cosine Similarity

![image](https://github.com/user-attachments/assets/3d363a69-7e64-4094-af88-b04c48e43792)

Cosine Similarity digunakan untuk mengukur kesamaan antar lagu berdasarkan fitur teknikal mereka (misalnya, danceability, energy, loudness).
Skor similarity berkisar antara 0 hingga 1, dengan 1 berarti kedua lagu sangat mirip dan 0 berarti sangat berbeda.
Hasil dari perhitungan cosine similarity digunakan untuk memberikan rekomendasi lagu yang paling mirip dengan lagu yang dimasukkan oleh pengguna.

2. Singular Value Decomposition (SVD)

![image](https://github.com/user-attachments/assets/b5a8979d-ff1f-4053-8739-e49710238d1d)

SVD digunakan untuk melakukan dimensionality reduction pada User-Item Interaction Matrix, dan menghasilkan rekomendasi lagu berdasarkan kesamaan antar lagu-lagu yang telah direduksi dimensinya.

Skor kesamaan antar lagu dihitung berdasarkan matriks yang telah direduksi dimensinya.
Hasil rekomendasi SVD memberikan lagu-lagu yang memiliki kesamaan terbesar dengan lagu yang dicari oleh pengguna.


---Ini adalah bagian akhir laporan---

