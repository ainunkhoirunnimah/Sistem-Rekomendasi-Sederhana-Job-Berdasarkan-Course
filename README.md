## 📌 Sistem Rekomendasi Kursus untuk Pekerjaan

### 🎯 Tujuan Proyek

Proyek ini bertujuan untuk membangun sistem rekomendasi yang mencocokkan deskripsi pekerjaan dengan kursus online dari Coursera. Dengan sistem ini, pengguna dapat memperoleh saran kursus yang sesuai dengan pekerjaan target mereka, guna meningkatkan keterampilan yang relevan.

### 🛠️ Pendekatan dan Dataset

Sistem rekomendasi dikembangkan dengan menggunakan dua dataset utama:

* **Job Listing Dataset:** Berisi judul pekerjaan dan deskripsi tanggung jawab serta kualifikasi yang dibutuhkan.
* **Coursera Courses Dataset:** Memuat nama kursus, partner (universitas/perusahaan), tingkat kesulitan, rating, deskripsi kursus, dan daftar keterampilan yang diajarkan.

Untuk menyatukan informasi kursus, kolom `Title`, `Difficulty`, `course_description`, dan `Skills` digabung menjadi satu kolom teks gabungan `text` sebagai representasi konten kursus.

---

### 🤖 Proses Vektorisasi: BERT via SentenceTransformer

Proyek ini menggunakan pendekatan **embedding berbasis BERT** dengan bantuan library `SentenceTransformer`.
Metode ini dipilih karena:

* **Kemampuan memahami konteks kalimat secara mendalam** dibanding metode tradisional seperti TF-IDF atau Word2Vec.
* **Presisi semantik** yang lebih tinggi dalam mencocokkan kalimat panjang dan beragam gaya bahasa, seperti antara deskripsi pekerjaan dan kursus.

Langkah-langkah utama:

1. Menggabungkan kolom-kolom penting menjadi teks utuh (job description dan course description).
2. Mengubah teks menjadi embedding menggunakan pretrained model BERT (`all-MiniLM-L6-v2`).
3. Menghitung kesamaan menggunakan **cosine similarity** antar embedding pekerjaan dan kursus.

---

### 📈 Hasil Rekomendasi

Contoh hasil rekomendasi menunjukkan bahwa sistem mampu memetakan kebutuhan pekerjaan dengan kursus yang sesuai. Contoh:

> **Job Title**: Data Analyst
> **Top Recommended Courses**:
>
> * Google Data Analytics
> * Excel Skills for Business
> * SQL for Data Science

Rekomendasi dipilih berdasarkan nilai kesamaan tertinggi dari hasil embedding.

---

### 🧩 Refleksi & Kendala

#### Kendala:

* **Ukuran model BERT** membutuhkan waktu dan sumber daya komputasi yang lebih besar.
* Perbedaan gaya penulisan antara deskripsi pekerjaan dan kursus kadang masih menyebabkan noise.
* Kursus dengan informasi terlalu umum atau promosi sulit untuk dipetakan secara tepat.

#### Solusi:

* Menggunakan versi ringan dari BERT (`all-MiniLM-L6-v2`) untuk efisiensi.
* Melakukan preprocessing menyeluruh: menghapus HTML, simbol, dan stopwords.
* Memastikan representasi teks pekerjaan dan kursus sebanding dengan menyatukan kolom-kolom informatif.
