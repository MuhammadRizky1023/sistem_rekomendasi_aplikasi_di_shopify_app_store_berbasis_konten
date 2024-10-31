# Laporan Proyek Rekomendasi bedasarkan Content Shopify - Muhammad Rizky

## Domain Proyek
Rekomendasi bedasarkan content adalah elemen kunci dalam platform e-commerce yang dapat meningkatkan konversi dan kepuasan pelanggan. Dengan menggunakan teknik rekomendasi yang efektif, seperti Content-Based Filtering, kita dapat membantu pelanggan menemukan produk yang sesuai dengan preferensi mereka berdasarkan karakteristik produk. Proyek ini bertujuan untuk membangun sistem rekomendasi berbasis Content-Based Filtering untuk meningkatkan pengalaman pengguna dan keterlibatan mereka di platform Shopify.

## Business Understanding
### Problem Statements
- Bagaimana cara memberikan rekomendasi produk yang relevan bagi pelanggan Shopify berdasarkan data produk?
- Teknik rekomendasi apa yang efektif untuk meningkatkan relevansi dan akurasi rekomendasi produk?

### Goals
- Membangun sistem rekomendasi yang mampu memberikan saran produk relevan untuk setiap pelanggan di Shopify.
- Menggunakan pendekatan Content-Based Filtering untuk menyediakan rekomendasi berbasis karakteristik produk.

### Solution Statements
- Menggunakan Content-Based Filtering untuk memberikan rekomendasi berdasarkan kesamaan fitur produk seperti kategori, deskripsi, dan rating.

## Data Understanding
Dataset yang digunakan mencakup data aplikasi Shopify, termasuk informasi seperti **id**, **title**, **developer**, **rating**, **reviews_count**, **description**, dan **tagline**. Dataset ini memungkinkan analisis karakteristik produk untuk memberikan rekomendasi yang akurat.

### Struktur Data
| **Fitur**         | **Deskripsi**                                                               |
|-------------------|-----------------------------------------------------------------------------|
| **id**            | ID unik untuk setiap aplikasi                                               |
| **title**         | Nama aplikasi                                                               |
| **developer**     | Pengembang atau perusahaan yang membuat aplikasi                            |
| **rating**        | Rating rata-rata aplikasi berdasarkan ulasan pengguna                       |
| **reviews_count** | Jumlah ulasan yang diterima oleh aplikasi                                   |
| **description**   | Deskripsi aplikasi                                                          |
| **tagline**       | Ringkasan singkat aplikasi                                                  |

### Kondisi Data
- **Missing Values**: Tidak ada nilai kosong dalam dataset ini.
- **Duplikat**: Tidak ditemukan data duplikat dalam dataset.

## Exploratory Data Analysis (EDA)
EDA bertujuan untuk memahami karakteristik dan pola dalam data, seperti distribusi rating aplikasi, jumlah ulasan yang telah di terima.

### Distribusi bedasarkan rating
![distribusi_rating](https://github.com/user-attachments/assets/c4e18652-b3d3-46fe-afd7-ab996db6873f)

### Distribusi bedasarkan ulasan
![distribusi_ulasan](https://github.com/user-attachments/assets/fd1f2956-e599-4cca-af99-f4f8182377fa)

## Data Preprocessing
Tahapan Data Preprocessing untuk menangani nilai hilang dan menghapus data duplikat. Menangani nilai yang hilang bisa dengan rata-rata atau median.
### Menangani nilai yang hilang
      df_apps.fillna({'rating': df_apps['rating'].mean()}, inplace=True)# Mengisi nilai hilang pada rating dengan rata-rata

### Memeriksa nilai duplikat
    df_apps.drop_duplicates(subset='title', keep='first', inplace=True)

## Data Preparation
 Pada tahap ini, Anda akan menggabungkan kolom teks yang relevan, seperti title, description, dan tagline menjadi satu kolom content untuk representasi yang lebih kaya.
### 1. Membuat Kolom Konten
          from sklearn.feature_extraction.text import TfidfVectorizer
          df_apps['content'] = df_apps['title'] + " " + df_apps['description'] + " " + df_apps['tagline'] 
### 2. Text Preprocessing dan Vectorization
         vector = TfidfVectorizer(stop_words='english', ngram_range=(1, 2), max_df=0.9, min_df=0.2)
         matrix_vector = vector.fit_transform(df_apps['content'])

## Model Development: Content-Based Filtering
Content-Based Filtering menganalisis kesamaan antara fitur aplikasi (seperti kategori, deskripsi, dan rating) untuk memberikan rekomendasi yang mirip dengan aplikasi yang telah disukai oleh pengguna.

- **TF-IDF Vectorization**: Teknik ini digunakan untuk mengubah deskripsi aplikasi menjadi vektor, sehingga kesamaan antar aplikasi dapat dihitung.
- **Cosine Similarity**: Cosine Similarity digunakan untuk mengukur kesamaan antara aplikasi yang telah diberi rating tinggi oleh pengguna dan aplikasi lainnya. Aplikasi dengan skor kemiripan tertinggi kemudian direkomendasikan.

## Evaluation Model
menampilkan hasil rekomendasi beserta kemiripannya dengan model yang telah di buat.
# JewelExchange Product Feed API Recommendation

Rekomendasi berikut disusun berdasarkan tingkat kemiripan aplikasi dengan *JewelExchange Product Feed API*, bertujuan untuk membantu pengguna menemukan alternatif produk atau fitur serupa di platform Shopify. Aplikasi-aplikasi ini memiliki kemiripan dalam fungsi pengelolaan produk, manajemen stok, dan integrasi feed.

## Daftar Rekomendasi Produk Berdasarkan Kemiripan

| **Judul**                          | **Kemiripan (%)** |
|------------------------------------|--------------------|
| Search Veil                        | 83.86             |
| Affiliate Product Feed             | 82.82             |
| Feeds Bridge                       | 78.68             |
| Auto Hide Sold‑out Products        | 78.56             |
| Nostock‑Noshow                     | 78.44             |
| IconEcom: Print On Demand          | 77.74             |
| Push Down & Hide Out of Stock      | 76.49             |
| Simple Bulk Price Editor           | 76.37             |
| Ablestar Bulk Product Editor       | 75.13             |
| Nada: Sort & Hide Sold‑out         | 74.71             |
| Blog Linker                        | 73.88             |
### Evaluation Model dengan matrix Precision at K, Recall at K
precision at k: Menghitung berapa banyak rekomendasi yang relevan di antara K rekomendasi teratas, dinyatakan dalam persen. recall at k: Menghitung berapa banyak item relevan yang ter-rekomendasi di antara K rekomendasi teratas terhadap total item relevan, juga dalam bentuk persen.

## Conclusion
Kesimpulan dari proyek sistem rekomendasi aplikasi Shopify ini menunjukkan bahwa pendekatan berbasis konten dapat secara efektif mengidentifikasi aplikasi yang memiliki kesamaan fitur atau fungsi yang tinggi, sesuai dengan kebutuhan pengguna. Dengan menghitung kemiripan menggunakan Cosine Similarity, sistem ini mampu memberikan daftar rekomendasi aplikasi dengan tingkat kemiripan tertentu, membantu pengguna menemukan aplikasi yang relevan tanpa harus mencari secara manual. Evaluasi yang dilakukan melalui metrik precision dan recall menunjukkan seberapa baik model ini dalam merekomendasikan aplikasi yang benar-benar relevan, meskipun tantangan seperti ketersediaan data perilaku pengguna tetap menjadi keterbatasan.



## Referensi
1. Lops, P., de Gemmis, M., & Semeraro, G. (2011). Content-based Recommender Systems: State of the Art and Trends. *Recommender Systems Handbook*, 73-105. https://doi.org/10.1007/978-0-387-85820-3_3
2. Aggarwal, C. C. (2016). Content-Based Recommender Systems. In *Recommender Systems* (pp. 139-166). Springer, Cham. https://doi.org/10.1007/978-3-319-29659-3_5
3. Van Meteren, R., & Van Someren, M. (2000). Using Content-Based Filtering for Recommendation. In *Proceedings of the Machine Learning in the New Information Age: MLnet/ECML2000 Workshop*, 47-56.
