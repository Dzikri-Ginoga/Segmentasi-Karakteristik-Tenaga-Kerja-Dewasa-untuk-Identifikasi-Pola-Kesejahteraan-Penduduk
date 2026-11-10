# Segmentasi Karakteristik Tenaga Kerja Dewasa untuk Identifikasi Pola Kesejahteraan Penduduk

Studi kasus analisis data sensus angkatan kerja dewasa menggunakan **Adult Census Income Dataset** (1994 US Census Bureau) untuk memetakan karakteristik sosio-demografis serta faktor penentu tingkat kesejahteraan penduduk (klasifikasi pendapatan `<=50K` vs `>50K`).

---

## Ringkasan Proyek & Pemenuhan Rubrik Capaian

Proyek ini disusun dan distrukturisasi secara menyeluruh dengan memenuhi **14 Butir Capaian**:

1. **Data Understanding**:
   - **Sumber Data & Lisensi**: Ekstraksi Sensus AS 1994 oleh Ronny Kohavi & Barry Becker (UCI Machine Learning Repository, lisensi CC BY 4.0).
   - **Data Dictionary**: 15 variabel lengkap dengan definisi tipe data, skala pengukuran (rasio, ordinal, nominal), dan satuan pengukuran (tahun, USD, jam/minggu).
   - **Representativitas & Bias**: Identifikasi keterbatasan dan bias sampel (bias gender pria 66.9%, bias etnis White 85.4%, bias geografis US 89.6%, serta justifikasi bobot makro `fnlwgt`).
2. **Exploratory Data Analysis (EDA) Berinsight**:
   - **Statistik Deskriptif**: Analisis mean, median, skewness, kurtosis, IQR, dan dispersi (CV) dengan kesimpulan terpadu.
   - **Visualisasi Fitur & Target**: Analisis pola distribusi numerik & kategorikal, visualisasi ketimpangan kelas target (75.9% vs 24.1%), serta kohort siklus hidup usia (*age cohort analysis*).
   - **Analisis Korelasi (Minimal 3 Insight Kunci)**:
     1. *Pendidikan (`education_num`)*: Korelasi positif tertinggi (+0.34) dengan pendapatan >50K.
     2. *Status Perkawinan (`marital_status`)*: Pekerja berstatus `Married-civ-spouse` memiliki rasio pendapatan >50K sebesar 44.7%, jauh melampaui kelompok lajang (4.6%).
     3. *Modal Finansial (`capital_gain`)*: Meskipun >91% bernilai nol, kepemilikan keuntungan modal meningkatkan peluang berpenghasilan >50K hingga 57.6%.
     4. *Disparitas Gender & Beban Jam Kerja*: Disparitas peluang pendapatan tinggi pria (30.6%) vs wanita (10.9%) yang beririsan dengan perbedaan jam kerja rata-rata.
3. **Audit Kualitas Data**:
   - Pemeriksaan terperinci missing values per kolom (`occupation` 5.66%, `workclass` 5.64%, `native_country` 1.79%).
   - Deteksi 24 baris duplikasi identik.
   - Perhitungan batas pencilan (metode IQR) untuk setiap fitur numerik.
4. **Data Cleaning**:
   - Penghapusan 24 baris duplikat identik.
   - Imputasi modus pada variabel kategorikal untuk mempertahankan ukuran sampel 32,537 observasi.
   - Penyajian tabel dan visualisasi komparatif **Kondisi Sebelum vs Sesudah Pembersihan**.
5. **Data Preprocessing**:
   - **Splitting Data Bebas Data Leakage**: Pemisahan 80:20 secara terstratifikasi (`stratify=y`) dilakukan **sebelum** fitting encoder, scaler, dan oversampling.
   - **Encoding & Scaling**: `OneHotEncoder(drop='first')` untuk variabel nominal dan `RobustScaler` untuk fitur numerik yang memiliki outlier ekstrem.
   - **Penanganan Class Imbalance**: Penerapan **SMOTE** (*Synthetic Minority Over-sampling Technique*) khusus pada data training untuk menghasilkan rasio kelas seimbang 50:50.
6. **Feature Selection & Engineering**:
   - Rekayasa fitur: `capital_net` (laba bersih investasi modal), `has_capital_gain`, `has_capital_loss`, dan `is_us_native`.
   - Eliminasi fitur: `fnlwgt` (bobot makro sensus yang tidak relevan dengan karakteristik individual) dan `education` (100% multikolinear dengan `education_num`).
   - Bukti empiris: Evaluasi kepentingan fitur menggunakan **Random Forest Feature Importance**.

---

## Struktur File

```text
├── adult.csv           # Dataset mentah Adult Census Income
├── DS_Projek.ipynb     # Jupyter Notebook utama 
├── README.md           # Dokumentasi proyek
└── .gitignore          # Konfigurasi pengabaian file temporary
```

---

## Cara Menjalankan Notebook

1. Pastikan Python 3.8+ telah terinstal.
2. Pasang pustaka pendukung yang diperlukan:
   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn imbalanced-learn
   ```
3. Buka dan jalankan Jupyter Notebook:
   ```bash
   jupyter notebook DS_Projek.ipynb
   ```
