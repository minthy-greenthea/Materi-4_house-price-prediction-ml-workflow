# Studi Kasus Machine Learning: House Price Prediction (Supervised Regression)

Repositori ini berisi implementasi *end-to-end Machine Learning workflow* untuk studi kasus **Prediksi Harga Rumah (*House Price Prediction*)** menggunakan bahasa pemrograman Python. Proyek ini disusun sebagai tugas implementasi dari **Informatics Practitioner Lecture Series: Introduction to Machine Learning** bersama pemateri **Ibu Taniza Tajudin (Universiti Teknologi MARA / UiTM Kedah, Malaysia)**.

---
**Nama:** [Ayuni Salsyabilla Putri]
**NPM:** [G1A024096  ]
**Program Studi:** Informatika — Universitas Bengkulu
**Topik Kuliah Umum:** Introduction to Machine Learning

---

## Latar Belakang Studi Kasus
Sesuai dengan materi yang dipaparkan oleh Ibu Taniza Tajudin, *Machine Learning* memungkinkan algoritma mempelajari data historis untuk menemukan pola (*patterns*) secara otomatis dan menghasilkan prediksi tanpa perlu menuliskan aturan logika (*if-then rules*) secara manual.

Dalam studi kasus ini, permasalahan penentuan harga properti dimodelkan menggunakan pendekatan **Supervised Learning — Regression** karena target keluaran (*output label*) yang ingin diprediksi berupa nilai numerik kontinu (`Price_USD`). Fitur masukan (*input features* / atribut) yang digunakan mengacu langsung pada simulasi materi kuliah umum:
1. **`Size_sqft`**: Luas bangunan rumah (dalam satuan *square feet*).
2. **`Bedrooms`**: Jumlah kamar tidur.
3. **`Location`**: Kategori lokasi kota (`City A` = Pusat Kota Besar, `City B` = Pinggiran Kota, `City C` = Area Pedesaan).
4. **`Price_USD`** *(Target Output)*: Harga rumah dalam satuan USD.

---

## Alur Kerja Implementasi (7-Step Machine Learning Workflow)

Kode program di dalam *notebook* [`House_Price_Prediction_ML_Workflow.ipynb`](./House_Price_Prediction_ML_Workflow.ipynb) disusun secara sistematis mengikuti 7 tahapan *Machine Learning Workflow* dari pemateri:

1. **Step 1: Data Collection:**
   Mengumpulkan dataset mentah (`raw_house_data.csv`) sebanyak 154 baris yang merepresentasikan kondisi data dunia nyata (memuat *missing values*, data duplikat, dan *outliers*).
2. **Step 2: Data Preprocessing:**

Menghapus 4 baris data yang terduplikasi (*remove duplicates*).

Menangani 8 nilai kosong (`NaN`) pada kolom `Size_sqft` dan `Bedrooms` dengan metode imputasi nilai tengah (*median*).

Memfilter dan membuang 2 data anomali ekstrem (*outliers*).

Melakukan konversi tipe data teks menjadi numerik (*encoding*) pada kolom `Location` (`City C = 1`, `City B = 2`, `City A = 3`) serta mendemonstrasikan normalisasi fitur (*Min-Max Scaling* ke rentang `0–1`).
   * Menyimpan hasil pembersihan sebanyak 148 baris ke dalam file `cleaned_house_data.csv`.
3. **Step 3: Split Data:**
   Membagi data bersih dengan proporsi **80% Training Set** (118 baris) untuk pelatihan generalisasi pola dan **20% Testing Set** (30 baris) sebagai *unseen data* untuk validasi model.
4. **Step 4: Choose Model:**
   Memilih 3 algoritma Regresi yang dibahas pada perkuliahan untuk dikomparasi:

*Linear Regression*

*Polynomial Regression (Degree 2)*

*Support Vector Regression (SVR)*
5. **Step 5: Train Model:**
   Melatih ketiga algoritma pada data latih (`X_train`, `y_train`) hingga model berhasil menemukan bobot pengaruh tiap fitur terhadap harga rumah.
6. **Step 6: Evaluate Model:**
   Mengukur performa ketiga model pada *Testing Set* menggunakan metrik **Mean Absolute Error (MAE)**, **Root Mean Squared Error (RMSE)**, dan **R-Squared ($R^2$ Score)**, serta membandingkan skor *Training* vs *Testing* untuk memastikan tidak terjadi *overfitting* maupun *underfitting*.
7. **Step 7: Deploy for AI Inference:**
   Menggunakan model terbaik untuk memprediksi harga rumah baru yang belum pernah dilihat sebelumnya (*unseen real-world data*), termasuk skenario rumah dengan 3 kamar tidur di `City B` sebagaimana dicontohkan pada *slide* pemateri.

---

## Ringkasan Hasil Evaluasi Model

Berdasarkan pengujian pada 20% *Testing Set*, ketiga algoritma menunjukkan performa yang sangat baik dan stabil (*Good Fit* / bebas *overfitting*):

| Algoritma Model | Metrik Utama | Hasil Evaluasi | Status Model |
| :--- | :--- | :--- | :--- |
| **Linear Regression** *(Model Terbaik)* | **R² Test / MAE** | **~98.5% / ~$9,500 USD** | **Good Fit (Optimal & Stabil)** |
| **Polynomial Regression (Degree 2)** | R² Test / MAE | ~98.4% / ~$9,700 USD | Good Fit (Optimal & Stabil) |
| **Support Vector Regression (SVR)** | R² Test / MAE | ~96.8% / ~$13,200 USD | Good Fit (Optimal & Stabil) |

**Kesimpulan Evaluasi:** Algoritma **Linear Regression** terpilih sebagai model terbaik karena memiliki tingkat kesalahan (MAE) paling rendah dan akurasi $R^2$ tertinggi pada data uji, dengan selisih antara *Training* dan *Testing* di bawah 1%.

---

## Struktur File di Repositori
* [`House_Price_Prediction_ML_Workflow.ipynb`](./House_Price_Prediction_ML_Workflow.ipynb) : Kode program utama (Jupyter Notebook / Google Colab) lengkap dengan penjelasan tiap tahap, tabel output, dan visualisasi grafik.
* [`raw_house_data.csv`](./raw_house_data.csv) : Dataset mentah sebelum tahap *Data Preprocessing*.
* [`cleaned_house_data.csv`](./cleaned_house_data.csv) : Dataset bersih setelah tahap *Data Preprocessing*.
* [`README.md`](./README.md) : Dokumentasi dan laporan ringkas studi kasus.
