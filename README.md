# 🎮 Game Recommendation System with Content-Based and Collaborative Filtering

## 📌 Project Overview

Dalam dunia industri game yang berkembang pesat, jumlah game yang tersedia di berbagai platform semakin meningkat setiap tahunnya. Kondisi ini membuat pengguna kesulitan untuk menemukan game yang sesuai dengan preferensi mereka. Oleh karena itu, sistem rekomendasi game menjadi sangat penting untuk membantu pengguna menjelajahi dan menemukan game yang relevan.

Proyek ini bertujuan untuk membangun sistem rekomendasi game berbasis *Content-Based Filtering* dan *Collaborative Filtering* menggunakan dataset game yang mencakup genre, platform, skor review, dan lainnya. Rekomendasi ini diharapkan dapat memberikan pengalaman pengguna yang lebih personal dan efisien dalam menemukan game baru.

Referensi:
- [Game Recommendation Techniques - Towards Data Science](https://towardsdatascience.com/game-recommendation-systems-3eb75e1eb29d)
- [Metacritic Game Scores API Data](https://www.kaggle.com/)

---

## 💡 Business Understanding

### Problem Statement
Pengguna kesulitan menemukan game baru yang sesuai dengan selera mereka dari ribuan pilihan yang tersedia di berbagai platform.

### Goals
Mengembangkan sistem rekomendasi game yang dapat memberikan saran game serupa berdasarkan preferensi pengguna sebelumnya atau konten dari game yang pernah dimainkan.

### Solution Approach
Untuk mencapai tujuan tersebut, digunakan dua pendekatan:

1. **Content-Based Filtering**
   - Merekomendasikan game berdasarkan kesamaan fitur seperti genre, platform, dan skor review.

---

## 📊 Data Understanding

Dataset terdiri dari 13.390 entri dan 12 kolom yang mencakup informasi game seperti berikut:

| Kolom                     | Deskripsi                                      |
|---------------------------|-----------------------------------------------|
| name                      | Nama game                                     |
| metacritic_review_count   | Jumlah ulasan dari Metacritic                 |
| metacritic_review_score   | Skor ulasan Metacritic                        |
| user_review_count         | Jumlah ulasan pengguna                        |
| user_review_score         | Skor ulasan pengguna                          |
| developer                 | Nama pengembang                               |
| publisher                 | Nama penerbit                                 |
| platforms                 | Platform tempat game tersedia                 |
| genres                    | Genre game                                    |
| esrb                      | Rating ESRB (untuk batasan usia)              |
| must_play                 | Label apakah game "wajib dimainkan" (0/1)     |

Link sumber data: [Kaggle - Video Game Dataset](https://www.kaggle.com/datasets/sidtwr/videogame-dataset-metacritic)

#### Kondisi Data

#### Missing Values
Dataset Metacritic Games kemungkinan memiliki beberapa nilai yang hilang (missing values), terutama pada kolom-kolom seperti:

- `user_review_score`: Beberapa game mungkin tidak memiliki nilai ini jika belum mendapatkan cukup ulasan dari pengguna
- `metacritic_review_score`: Game yang baru dirilis atau kurang populer mungkin belum memiliki skor dari kritikus profesional
- `genres`: Beberapa ga


### Exploratory Data Analysis (EDA)
#### **Distribusi Skor Review**

![Distribusi Skor Review](https://drive.google.com/uc?export=view&id=1LuSXHh3OAiAkgNkNYdt6FOAaiRdels3D)

**Insight:**
- Mayoritas game memiliki skor Metacritic pada rentang 61–80 (60%) dan 81–100 (20.7%), yang menunjukkan bahwa sebagian besar game dalam dataset mendapatkan review yang positif hingga sangat baik. Sementara itu, hanya sebagian kecil game yang berada di kategori rendah (di bawah 60), mengindikasikan bahwa game dengan kualitas buruk relatif sedikit dalam dataset ini.

#### **Distribusi Genre**

![Distribusi Genre](https://drive.google.com/uc?export=view&id=1ZFD0dtKhfQS5sqox93qy7JGS-UVe4NGP)

**Insight:**
- Genre yang paling banyak muncul dalam dataset adalah Action Adventure, diikuti oleh 2D Platformer dan Action RPG. Ini menunjukkan bahwa genre aksi dan petualangan mendominasi pasar game, yang bisa jadi disebabkan oleh gameplay yang lebih seru dan jangkauan pemain yang lebih luas. Genre-genre ini cocok dijadikan fokus utama dalam sistem rekomendasi karena popularitasnya tinggi.

#### **Distribusi Platform**
![Distribusi Genre](https://drive.google.com/uc?export=view&id=1KhZ0mjxeBrlkM87FH-3UE5364DcoDBFY)

#### **ESRB Rating**
![ESRB Genre](https://drive.google.com/uc?export=view&id=1zTDUa_hqOoNnvePzFYunGZkxJQZDRAeQ)

**Insight:**
- Persebaran rating dari game juga beragam, dan pada dataset ini gam untuk **Teen** lebih unggu dari yang lain. sehingga dapat dikategorikan kalau game-game pada dataset ramah Remaja. Disusul game Rated E yang beda 4% dari game for Teen
  
#### **Developer**
![Developer Genre](https://drive.google.com/uc?export=view&id=14GoFf69E9pgr6I268peFItuQduSzty4Q)

**Insight:**
- Developer dari game pada dataset di ungguli oleh Capcom dengan jumlah game lebih dari 175 judul dan disusul oleh Nintendo diposisi kedua

#### **Rata-Rata Skor per Game
![Developer Genre](https://drive.google.com/uc?export=view&id=1KG6-84Gc0wpMxZ3lII8ipVifa9yC86-3)

**Insight:**
- Dari persebaran data, diambil Top 10 game dengan score terbaik dan itu diungguli oleh Soccer Management dan diposisi kedua adalah Racing Sim. Dapa diambil kesimpulan kalau para pemain game lebih menyukai game bertema sport seperti yang tertera pada posisi pertama dan kedua

#### **Platform vs Must Play**
![Developer Genre](https://drive.google.com/uc?export=view&id=15ugX-MBj00mKi1Cudc4m0ub8ZLo85MTm)

**Insight:**
- Dari data dapat dilihat Top 10 platform yang sering digunakan oleh player ketika berbaik game, dan itu diungguli oleh platform PC. Bisa diambil asumsi bahwa PC memiliki banyak game yang mudah untuk diakses oleh player.

#### **ESRB vs Genre**
![Developer Genre](https://drive.google.com/uc?export=view&id=1VCPe77utjM3vlnTHyuqnTosDWDfE8XZL)

**Insight:**
- Genre dengan Jumlah Game Terbanyak:Genre 'Action RPG' dan '2D Platformer' memiliki jumlah game tertinggi secara keseluruhan.
- 'FPS' (First Person Shooter) didominasi oleh rating Mature, menandakan bahwa genre ini lebih banyak ditujukan untuk pemain dewasa.
- Distribusi Rating ESRB: Rated E (Everyone) banyak terdapat pada genre '2D Platformer', menunjukkan bahwa genre ini ramah untuk segala usia. Rated T (Teen) mendominasi banyak genre seperti 'Action RPG', 'Action Adventure', dan 'JRPG'. Rated M (Mature) sangat dominan di genre seperti 'FPS', 'Open-World Action', dan 'Survival', menunjukkan bahwa game dengan konten lebih dewasa populer di genre-genre ini.
- Genre yang Merata di Semua Rating: Genre seperti 'Adventure' dan 'Point-and-Click' menunjukkan distribusi rating yang relatif merata, menandakan fleksibilitas genre tersebut untuk berbagai usia.
---

## 🧹 Data Preparation

Beberapa langkah yang dilakukan:
- Menggunakan TF-IDF Vectorizer untuk mengonversi data teks (genre, platform, dll) menjadi representasi numerik.
- Menormalisasi beberapa kolom numerik 

Alasan dilakukan preprocessing:
- TF-IDF dipilih karena mampu menangkap bobot penting kata pada fitur genre/platform.

### Pendekatan 1: Content-Based Filtering
- Menggunakan TF-IDF untuk genre, platform, dan skor review.
- Menghitung cosine similarity antar game.
- Menyusun fungsi untuk merekomendasikan game berdasarkan input judul.
---

## 🧠 Modeling and Result

### Top-N Recommendation
Top-N Recommendation adalah pendekatan yang berfokus pada mengidentifikasi N item teratas yang paling relevan untuk direkomendasikan kepada pengguna, bukan pada memprediksi rating secara akurat.

**Cara Kerja:**
- Menghitung skor relevansi untuk setiap game berdasarkan preferensi pengguna
- Mengurutkan game berdasarkan skor relevansi
- Memilih N game teratas untuk direkomendasikan
- Menyusun daftar Top-N game dengan skor similarity rata-rata tertinggi.
- Menyediakan hasil rekomendasi awal tanpa masukan spesifik dari pengguna.

### Tabel Hasil Top-10 Rekomendasi

| No | Nama Game | Genres | Platforms | Rata-rata Similarity |
|----|-----------|--------|-----------|-----------------------|
| 1 | Onimusha: Warlords | Action Adventure | PlayStation, PlayStation 2, PC, PlayStation 4, Xbox One | 0.253513 |
| 2 | Arietta of Spirits | Action Adventure | PC, PlayStation 4, Nintendo Switch, Xbox One | 0.250333 |
| 3 | Ice Age: Scrat's Nutty Adventure | Action Adventure | Xbox One, PlayStation 4, PC, Nintendo Switch | 0.250333 |
| 4 | Furi | Action Adventure | PlayStation 4, PC, Xbox One | 0.250333 |
| 5 | Okami HD | Action Adventure | PlayStation 3, Xbox One, PlayStation 4 | 0.250333 |
| 6 | The Lord of the Rings - Gollum | Action Adventure | PC, PlayStation 4, Xbox One | 0.248740 |
| 7 | Life is Strange: True Colors | Action Adventure | PC, Xbox Series X, PlayStation 5, Xbox One | 0.248740 |
| 8 | UFO Robot Grendizer: The Feast of the Wolves | Action Adventure | PlayStation 5, Nintendo Switch, PC | 0.248740 |
| 9 | Shadows of the Damned: Hella Remastered | Action Adventure | Nintendo Switch, PC, PlayStation 4, Xbox One | 0.248740 |
| 10 | Strayed Lights | Action Adventure | PlayStation 5, PC, Xbox One, PlayStation 4 | 0.248740 |

### 📊 Insight dari Top-N Rekomendasi

Berikut adalah beberapa insight yang diperoleh dari hasil Top-10 rekomendasi yang dihasilkan oleh sistem:

## 1. Genre Konsisten
- Semua game yang direkomendasikan memiliki genre utama **Action Adventure**.
- Hal ini menunjukkan bahwa sistem mampu memahami dan memprioritaskan genre sebagai salah satu faktor utama dalam rekomendasi.

## 2. Platform yang Relevan
- Game yang direkomendasikan sebagian besar tersedia di platform populer seperti **PlayStation 4**, **PC**, **Xbox One**, dan **Nintendo Switch**.
- Ini memastikan bahwa pengguna mendapatkan rekomendasi game yang kompatibel dengan perangkat yang mereka gunakan.

## 3. Nilai Similarity yang Tinggi
- Rata-rata nilai similarity berkisar antara **0.248** hingga **0.253**, yang termasuk tinggi dalam skala cosine similarity.
- Menunjukkan bahwa rekomendasi yang dihasilkan sangat relevan berdasarkan kombinasi fitur teks.

## 4. Variasi dalam Kesamaan
- Walaupun semua game berada dalam genre yang sama, judul-judul yang direkomendasikan tetap menawarkan variasi dari segi cerita, tema, dan gameplay.
- Ini memberikan pengguna lebih banyak pilihan tanpa mengorbankan relevansi.

## 5. Potensi Pengembangan Sistem
- Sistem saat ini hanya mengandalkan `genres` dan `platforms`.
- Untuk meningkatkan akurasi di masa depan, fitur tambahan seperti **developer**, **mode permainan** (singleplayer/multiplayer), atau **rating pengguna** dapat dipertimbangkan.

---

### Kelebihan & Kekurangan:
| Pendekatan           | Kelebihan                                   | Kekurangan                                         |
|----------------------|----------------------------------------------|----------------------------------------------------|
| Content-Based        | Tidak butuh data pengguna, cocok untuk cold start | Terbatas pada informasi fitur, tidak adaptif       |
| Collaborative Filter | Menangkap preferensi kompleks pengguna       | Butuh data interaksi pengguna, cold start issue    |

---

# 📏 Evaluation

## Metrik Evaluasi

- **Cosine Similarity**  
  Digunakan untuk mengukur tingkat kemiripan antara game berdasarkan representasi vektor dari fitur-fitur seperti `genres`, `platforms`, dan `scores`.
  - Nilai cosine similarity berkisar dari **0** (tidak mirip) hingga **1** (identik).
  - Cocok digunakan pada sistem rekomendasi berbasis Content-Based Filtering (CBF) karena fokus pada kemiripan antar item berdasarkan atribut.

- **Precision@N**  
  Digunakan untuk mengevaluasi relevansi hasil rekomendasi.
  - Precision dihitung berdasarkan proporsi game yang benar-benar relevan dibandingkan seluruh rekomendasi yang diberikan.
  - Dalam konteks ini, relevansi ditentukan dari seberapa banyak fitur (genre, platform) pada hasil rekomendasi yang sesuai dengan game input.

## Rumus Precision@N:
$$
\text{Precision@N} = \frac{\text{Jumlah fitur relevan pada rekomendasi}}{N}
$$


---

## 📈 Hasil Evaluasi

| Skema Sistem Rekomendasi | Precision@10 | Rata-rata Cosine Similarity |
|:--------------------------|:-------------|:----------------------------|
| Genres + Platforms         | 0.9           | 0.250                       |
| Genres Only                | 0.7           | 0.220                       |
| Platforms Only             | 0.6           | 0.215                       |

### Interpretasi:
- Skema dengan kombinasi **Genres + Platforms** memberikan precision tertinggi (**90%**) dan juga memiliki rata-rata similarity yang lebih tinggi dibandingkan skema lain.
- Ini menunjukkan bahwa mempertimbangkan kedua fitur sekaligus menghasilkan rekomendasi yang lebih relevan dan mirip dengan preferensi pengguna.

---

## 📊 Komparasi dan Model Terbaik

- **Genres + Platforms** terbukti sebagai skema terbaik karena:
  - Precision@10 mencapai 0.9.
  - Rata-rata Cosine Similarity juga tertinggi di antara semua skema.
- Skema ini berhasil menemukan keseimbangan antara kemiripan fitur dan relevansi hasil rekomendasi.

---

## 🔗 Hubungan dengan Business Understanding

- **Problem Statement**: Pengguna kesulitan menemukan game baru yang sesuai dengan selera mereka dari ribuan pilihan yang tersedia di berbagai platform.
- **Goal**: Mengembangkan sistem rekomendasi game yang dapat memberikan saran game serupa berdasarkan preferensi pengguna sebelumnya atau konten dari game yang pernah dimainkan.
- **Solusi**: engan menggunakan Content-Based Filtering berbasis genres dan platforms, sistem berhasil menyajikan rekomendasi game yang relevan dengan minat pengguna.
- 
### Dampaknya:
- Membantu pengguna menemukan game baru yang sesuai dengan preferensi mereka tanpa harus mencari manual dari ribuan pilihan.
- Platform game atau marketplace dapat meningkatkan waktu bermain, loyalitas pengguna, dan potensi pembelian game tambahan.




