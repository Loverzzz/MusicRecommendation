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
Jumlah data awal : 114000 rows and 21 Coloumn
Jumlah data subset yang digunakan : 23999 and 21 Coloumn
Kondisi :
  - Missing Value = 0
  - Duplicated = 0
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
 - Subset Data: Hanya 23.999 baris pertama yang digunakan untuk mempercepat proses pelatihan dan evaluasi model.

# Modelling and Result
Model yang digunakan untuk sistem rekomendasi ini adalah Content-Based Filtering dengan menggunakan Cosine Similarity.
Cara Kerja Model 1 : 
- Content-Based Filtering dengan Cosine Similarity: Model pertama yang dibangun adalah Content-Based Filtering menggunakan Cosine Similarity untuk menghitung kesamaan antar lagu berdasarkan fitur teknikal seperti tempo, loudness, energy, dan lainnya.
- Cosine Similarity digunakan untuk mengukur kedekatan vektor fitur lagu yang dimasukkan oleh pengguna dengan vektor fitur lagu lainnya.
Tahapan Model 1:
- Preprocessing data untuk mengatasi duplikat, nilai hilang, dan melakukan standarisasi.
- Menggunakan Cosine Similarity untuk mencari kesamaan antara lagu-lagu berbasis fitur numerik dalam Content-Based Filtering.
Cara Kerja Model 2:
- Sebuah model Singular Value Decomposition (SVD) diterapkan pada matriks interaksi pengguna-lagu (matriks pengguna x lagu).
- Dengan SVD, kita dapat mengurangi dimensi matriks interaksi dan menemukan pola tersembunyi antara pengguna dan lagu. Dengan demikian, rekomendasi berbasis perilaku pengguna dapat dilakukan.
Tahapan Model 2:
- Membangun User-Item Interaction Matrix untuk Collaborative Filtering dan menggunakan SVD untuk menemukan pola tersembunyi dalam data interaksi.
- Memberikan rekomendasi berdasarkan kesamaan antar lagu baik dengan pendekatan Collaborative Filtering (SVD).
Hasil Top-N Rekomendasi Model 1 :
Recommended Tracks for 'bad liar':
1. Bad Liar (similarity: 1.0000)
2. ugly (similarity: 0.9842)
3. Shallow (similarity: 0.9746)
4. Forever Young (Glee Cast Version) (similarity: 0.9720)
5. Em Teu Altar (similarity: 0.9652)
6. Million Years Ago (similarity: 0.9646)
7. 我的歌 (similarity: 0.9606)
8. Closure (similarity: 0.9594)
9. Dear My Friend, (similarity: 0.9587)
10. Thursday (similarity: 0.9587)

Cosine Similarity digunakan untuk mengukur kesamaan antar lagu berdasarkan fitur teknikal mereka (misalnya, danceability, energy, loudness).
Skor similarity berkisar antara 0 hingga 1, dengan 1 berarti kedua lagu sangat mirip dan 0 berarti sangat berbeda.
Hasil dari perhitungan cosine similarity digunakan untuk memberikan rekomendasi lagu yang paling mirip dengan lagu yang dimasukkan oleh pengguna.

Hasil Top-N Rekomendasi Model 2 :
Rekomendasi Lagu berdasarkan SVD untuk 'Bad Liar':
1. 10,000 DOLLARS (similarity: 0.9757)
2. 10,000 Hours (similarity: 0.9378)
3. 10 Year Bender (similarity: 0.8895)
4. 10 Variations in G, K.455 on "Unser dummer Pöbel meint" by C.W. Gluck: 3. Variation II (similarity: 0.5663)
5. 1, 2, 3 (feat. Jason Derulo & De La Ghetto) (similarity: 0.5335)
6. 1-2 Buckle Your Shoe (similarity: 0.2556)
7. (Sittin' On) the Dock of the Bay (similarity: 0.2416)
8. 10 Over 10 (feat. Rotimi) (similarity: 0.2256)
9. 1/1 - Remastered 2004 (similarity: 0.1743)
10. 1 Law (similarity: 0.0881)

SVD digunakan untuk melakukan dimensionality reduction pada User-Item Interaction Matrix, dan menghasilkan rekomendasi lagu berdasarkan kesamaan antar lagu-lagu yang telah direduksi dimensinya.
Skor kesamaan antar lagu dihitung berdasarkan matriks yang telah direduksi dimensinya. Hasil rekomendasi SVD memberikan lagu-lagu yang memiliki kesamaan terbesar dengan lagu yang dicari oleh pengguna.

# Evaluasi 
1. Model 1 :
   
![image](https://github.com/user-attachments/assets/8aa58dd0-cff1-4b5c-b8ae-7736064ae91f)

Tujuan: Fungsi ini digunakan untuk menghitung precision berdasarkan rekomendasi lagu yang diberikan oleh model, yang dihitung menggunakan cosine similarity.
Rumus Precision : Jumlah Rekomendasi relevan / Jumlah rekomendasi teratas (top_n)
Parameter:
 1. track_name: Nama lagu yang ingin dicari rekomendasinya.
 2. df_subset: Data subset dari dataset yang akan digunakan dalam proses rekomendasi.
 3. cosine_sim: Matriks cosine similarity yang dihitung sebelumnya antara lagu-lagu dalam dataset.
 4. top_n: Jumlah rekomendasi teratas yang ingin dievaluasi (default 10).
 5. threshold: Batasan nilai similarity minimum agar suatu rekomendasi dianggap relevan (default 0.8).

2. Model 2:

![image](https://github.com/user-attachments/assets/a8b6c05d-e2c7-4782-81d6-77fdc5183f50)

![image](https://github.com/user-attachments/assets/1e8bdca8-011f-42ce-8f50-67a3acb5266d)

- MAE mengukur kesalahan rata-rata tanpa mempertimbangkan apakah kesalahan tersebut besar atau kecil.
- RMSE memberikan lebih banyak bobot pada kesalahan besar dan lebih sensitif terhadap nilai-nilai ekstrem, jadi jika model membuat kesalahan besar dalam beberapa prediksi, RMSE akan lebih tinggi daripada MAE.

Interpretasi Hasil:
 - MAE (0.0044): MAE yang sangat kecil (dekat dengan 0) menunjukkan bahwa rata-rata kesalahan model dalam memprediksi rating/interaction cukup kecil. Artinya, model secara keseluruhan cukup akurat dalam memperkirakan nilai rating atau popularitas lagu. Kesimpulan: Model ini cukup akurat, karena nilai MAE yang rendah mengindikasikan bahwa model tidak membuat banyak kesalahan.
 - RMSE (0.4486): RMSE yang lebih besar menunjukkan bahwa meskipun MAE sangat kecil, ada beberapa kesalahan yang lebih besar yang memengaruhi hasil keseluruhan. Ini berarti ada beberapa prediksi yang cukup jauh dari nilai aktual.
RMSE cenderung memberikan penalti lebih besar untuk kesalahan yang lebih besar, jadi nilai RMSE ini menunjukkan bahwa meskipun sebagian besar prediksi baik, ada beberapa yang jauh lebih buruk. Kesimpulan: Model memiliki beberapa prediksi yang sangat jauh dari nilai sebenarnya, meskipun rata-rata kesalahan tetap relatif kecil. Ini menunjukkan bahwa model cenderung lebih sensitif terhadap kesalahan besar.
---Ini adalah bagian akhir laporan---

