# Prediksi Harga Mobil Bekas di Saudi Arabia

## Pendahuluan

Menentukan harga mobil bekas yang tepat adalah tantangan yang sering dihadapi oleh penjual dan pembeli di Saudi Arabia. **OTO MOBILE**, sebagai platform jual beli mobil bekas terkemuka, ingin memberikan solusi yang memudahkan pengguna dalam memperkirakan harga mobil bekas secara akurat. Untuk mencapai hal ini, kami mengembangkan model prediksi harga mobil bekas menggunakan **Machine Learning** yang akan diintegrasikan ke dalam platform OTO MOBILE.

## Metodologi CRISP-DM

Proyek ini mengikuti kerangka kerja **CRISP-DM (Cross-Industry Standard Process for Data Mining)**, yang terdiri dari enam tahap utama:

1. [Business Understanding](#1-business-understanding)
2. [Data Understanding](#2-data-understanding)
3. [Data Preparation](#3-data-preparation)
4. [Modeling](#4-modeling)
5. [Evaluation](#5-evaluation)
6. [Deployment](#6-deployment)

---

## 1. Business Understanding

Pada tahap ini, kami berfokus pada pemahaman tujuan bisnis dan bagaimana solusi yang diusulkan dapat memenuhi kebutuhan tersebut.

### Tujuan Bisnis

- **Menyediakan alat prediksi harga mobil bekas** yang akurat untuk membantu pengguna OTO MOBILE dalam menentukan harga jual atau beli yang wajar.
- **Meningkatkan kepercayaan dan kenyamanan pengguna** dengan memberikan estimasi harga berbasis data.
- **Memperkuat posisi OTO MOBILE** sebagai platform yang inovatif dan customer-centric.

### Pernyataan Masalah

Menaksir harga mobil bekas secara manual seringkali tidak akurat karena melibatkan banyak variabel dan subjektivitas. Dengan membangun model Machine Learning, kami dapat mengotomatisasi proses ini dan menghasilkan prediksi yang lebih konsisten dan dapat diandalkan.

---

## 2. Data Understanding

Tahap ini melibatkan pengumpulan dan pemahaman data yang tersedia untuk proyek ini.

### Deskripsi Dataset

Dataset berisi **5624 entri** dengan 11 fitur berikut:

| Kolom         | Deskripsi                                         |
|---------------|---------------------------------------------------|
| **Type**      | Tipe mobil bekas (misalnya, SUV, sedan).          |
| **Region**    | Wilayah tempat mobil dijual.                      |
| **Make**      | Merek mobil (misalnya, Toyota, Ford).             |
| **Gear_Type** | Jenis transmisi (Automatic atau Manual).          |
| **Origin**    | Asal mobil (Saudi, Gulf Arabic, dll.).            |
| **Options**   | Fitur atau opsi yang tersedia di mobil.           |
| **Year**      | Tahun pembuatan mobil.                            |
| **Engine_Size** | Ukuran mesin dalam liter.                       |
| **Mileage**   | Jarak tempuh mobil dalam kilometer.               |
| **Negotiable**| Apakah harga bisa dinegosiasikan (`True`/`False`).|
| **Price**     | Harga jual mobil dalam Saudi Riyal (SAR).         |

### Analisis Data Awal

- **Variasi Harga**: Harga mobil berkisar dari **0** hingga **850,000 SAR**, dengan rata-rata **53,074 SAR**. Nilai **0** pada kolom harga menunjukkan data yang tidak valid atau harga yang dapat dinegosiasikan.
- **Distribusi Fitur**:
  - **Make**: Toyota adalah merek paling umum (**25.4%**).
  - **Gear_Type**: Transmisi otomatis mendominasi (**86.7%**).
  - **Region**: Riyadh adalah wilayah penjualan terbesar (**40.4%**).
- **Masalah Data**: Terdapat nilai harga **0** dan anomali pada jarak tempuh (misalnya, nilai yang sangat tinggi).

---

## 3. Data Preparation

Pada tahap ini, data diproses dan disiapkan untuk modeling.

### Langkah-langkah

1. **Data Cleaning**:
   - Menghapus entri dengan harga **0** atau menggantinya dengan nilai **NaN**.
   - Menangani outlier pada kolom **Mileage** dan **Engine_Size**.
2. **Handling Missing Values**:
   - Mengisi nilai yang hilang menggunakan teknik imputasi jika diperlukan.
3. **Encoding Variabel Kategorikal**:
   - Menggunakan **Binary Encoding** untuk kolom seperti `Type`, `Region`, dan `Mage`.
   - Menggunakan **One-Hot Encoding** untuk kolom seperti `Gear_Type`, `Origin`, dan `Option`.
4. **Feature Engineering**:
   - Membuat fitur baru seperti **Age** (umur mobil) dengan mengurangkan tahun sekarang dengan `Year`.
5. **Data Normalization**:
   - Melakukan normalisasi atau standardisasi pada fitur numerik untuk skala yang konsisten -> Robust Scalar.
6. **Data Splitting**:
   - Membagi data menjadi **training set** dan **testing set** dengan rasio 80:20.

---

## 4. Modeling

Di tahap ini, beberapa model Machine Learning dibangun dan dilatih menggunakan data yang telah dipersiapkan.

### Model yang Digunakan

1. **Linear Regression**:
   - Sebagai baseline model untuk memahami hubungan linear antara fitur dan harga.
2. **Random Forest Regressor**:
   - Memanfaatkan ensemble learning untuk menangani data yang kompleks dan non-linear.
3. **XGBoost Regressor**:
   - Model boosting yang efektif untuk meningkatkan akurasi prediksi.

### Teknik Evaluasi

- **K-Fold Cross Validation**:
  - Menggunakan 5-fold cross-validation untuk memastikan model generalisasi dengan baik dan menghindari overfitting.
  
### Hyperparameter Tuning

- Menggunakan **Grid Search** untuk menemukan kombinasi hyperparameter terbaik untuk setiap model.

---

## 5. Evaluation

Evaluasi model dilakukan untuk menentukan model terbaik yang akan digunakan.

### Metrik Evaluasi

- **Mean Absolute Percentage Error (MAPE)**:
  - Dipilih karena harga mobil memiliki rentang yang luas, sehingga persentase kesalahan lebih relevan.
- **Root Mean Squared Error (RMSE)**:
  - Untuk mengukur kesalahan dengan memberi bobot lebih pada kesalahan yang lebih besar.
- **R-squared (R²)**:
  - Untuk mengetahui seberapa baik model menjelaskan variabilitas data.

### Hasil Evaluasi

**Model Terbaik**: Berdasarkan hasil evaluasi, **XGBoost Regressor** memiliki performa terbaik dengan MAPE terendah dan R² tertinggi.

---

## 6. Deployment

Memyimpan model dengan menggunakan library **pickle**

---

## Kesimpulan

Dengan mengikuti metodologi **CRISP-DM**, kami berhasil membangun model prediksi harga mobil bekas yang akurat menggunakan **XGBoost Regressor**. Model ini mampu membantu pengguna OTO MOBILE dalam menentukan harga jual atau beli yang wajar, sehingga meningkatkan kepercayaan dan kenyamanan dalam transaksi.

**Manfaat bagi OTO MOBILE**:

- **Peningkatan Layanan**: Memberikan fitur tambahan yang bermanfaat bagi pengguna.
- **Keunggulan Kompetitif**: Menjadi platform pertama yang menawarkan prediksi harga berbasis Machine Learning.
- **Data-Driven Decision Making**: Menggunakan wawasan dari data untuk strategi bisnis yang lebih baik.

---