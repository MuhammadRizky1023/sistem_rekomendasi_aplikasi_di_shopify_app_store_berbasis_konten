# Laporan Proyek Rekomendasi Shopify - Muhammad Rizky

## Domain Proyek
Rekomendasi produk adalah elemen kunci dalam platform e-commerce yang dapat meningkatkan konversi dan kepuasan pelanggan. Dengan menggunakan teknik rekomendasi yang efektif, seperti Content-Based Filtering, kita dapat membantu pelanggan menemukan produk yang sesuai dengan preferensi mereka berdasarkan karakteristik produk. Proyek ini bertujuan untuk membangun sistem rekomendasi berbasis Content-Based Filtering untuk meningkatkan pengalaman pengguna dan keterlibatan mereka di platform Shopify.

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


## Data Preparation
Pada tahap ini, data dipersiapkan untuk digunakan dalam model rekomendasi berbasis Content-Based Filtering, termasuk pembersihan teks, encoding fitur kategorikal, dan pembuatan vektor teks.

### Text Preprocessing
Untuk fitur teks seperti **description** dan **tagline**, dilakukan pembersihan teks dan tokenisasi untuk mengekstrak kata kunci yang relevan. Proses ini mencakup konversi teks ke dalam vektor menggunakan TF-IDF (Term Frequency-Inverse Document Frequency) untuk menentukan kata-kata penting dalam setiap aplikasi.


## Model Development: Content-Based Filtering
Content-Based Filtering menganalisis kesamaan antara fitur aplikasi (seperti kategori, deskripsi, dan rating) untuk memberikan rekomendasi yang mirip dengan aplikasi yang telah disukai oleh pengguna.

- **TF-IDF Vectorization**: Teknik ini digunakan untuk mengubah deskripsi aplikasi menjadi vektor, sehingga kesamaan antar aplikasi dapat dihitung.
- **Cosine Similarity**: Cosine Similarity digunakan untuk mengukur kesamaan antara aplikasi yang telah diberi rating tinggi oleh pengguna dan aplikasi lainnya. Aplikasi dengan skor kemiripan tertinggi kemudian direkomendasikan.

## Evaluation
Model dievaluasi dengan melihat relevansi rekomendasi yang diberikan menggunakan metrik **Precision** dan **Recall** untuk menilai seberapa sesuai rekomendasi yang dihasilkan oleh model.

### Hasil Evaluasi
Content-Based Filtering menunjukkan hasil yang baik dalam memberikan rekomendasi aplikasi yang mirip dengan preferensi pengguna, khususnya aplikasi dengan deskripsi, kategori, dan rating yang serupa.

## Conclusion
Proyek ini berhasil mengembangkan sistem rekomendasi berbasis Content-Based Filtering untuk meningkatkan pengalaman pelanggan di Shopify. Model ini mampu memberikan saran aplikasi yang relevan berdasarkan karakteristik aplikasi yang disukai pengguna sebelumnya.



## Referensi
1. Lops, P., de Gemmis, M., & Semeraro, G. (2011). Content-based Recommender Systems: State of the Art and Trends. *Recommender Systems Handbook*, 73-105. https://doi.org/10.1007/978-0-387-85820-3_3
2. Aggarwal, C. C. (2016). Content-Based Recommender Systems. In *Recommender Systems* (pp. 139-166). Springer, Cham. https://doi.org/10.1007/978-3-319-29659-3_5
3. Van Meteren, R., & Van Someren, M. (2000). Using Content-Based Filtering for Recommendation. In *Proceedings of the Machine Learning in the New Information Age: MLnet/ECML2000 Workshop*, 47-56.
