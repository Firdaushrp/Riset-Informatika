# Implementasi Model Document Understanding Transformer (Donut) pada Sistem Pencatatan Pengeluaran Bulanan Berbasis Character Recognition

# 1. Dataset Rencana Riset Kecil

### Sumber Dataset

- Dataset publik: COnsolidated Receipt Dataset for Post-OCR Parsing.
- Dataset Mandiri: Citra struk belanja fisik dari berbagai _minimarket_, _supermarket_, dan restoran lokal yang difoto secara langsung menggunakan kamera _smartphone_.

### Informasi yang Diekstraksi

- Tanggal Transaksi (_Transaction Date_)
- Total Pengeluaran (_Total Amount_)

Kategori akhir akan disesuaikan dengan anotasi dan kebutuhan fitur aplikasi pencatatan keuangan.

### Rencana Pengolahan Data

1. Seleksi dan pemeriksaan kualitas citra (membuang gambar yang terlalu blur hingga tidak terbaca mata).
2. Anotasi teks dan pelabelan entitas _JSON format_.
3. Pembagian data ke dalam _train_, _validation_, dan _test set_.
4. _Preprocessing_ citra (grayscaling, binarization) jika diperlukan oleh algoritma.
5. Augmentasi data pada _data train_ (penambahan _noise_, variasi kecerahan, rotasi ringan) untuk mensimulasikan hasil foto nyata.

---

# 2. Research Gap

Penelitian terdahulu telah banyak membahas ekstraksi teks menggunakan OCR tradisional (seperti Tesseract) pada dokumen terstruktur. Namun, ekstraksi informasi spesifik pada struk belanja seringkali masih menggunakan pendekatan _rule-based_ (_Regular Expression_) yang kaku dan rentan gagal ketika dihadapkan pada variasi _layout_ mesin kasir yang berbeda-beda.

Penelitian ini mengusulkan penggunaan algoritma Donut yang dilatih menggunakan kombinasi dataset publik dan dataset mandiri hasil foto langsung. Sistem ini tidak hanya membaca teks, tetapi juga dirancang untuk mengidentifikasi letak dan konteks nilai (Tanggal, Total) pada berbagai variasi kualitas struk (lecek, pudar, pencahayaan kurang) di Indonesia.

Kesenjangan penelitian (_research gap_) yang akan dikaji meliputi:

- **Keterbatasan Dataset Lokal:** Kurangnya dataset struk belanja representatif di Indonesia yang mencakup kondisi riil (lecek, terlipat, tinta pudar).
- **Kelemahan Model Kaku:** Pendekatan OCR tradisional yang sering gagal memahami hierarki dan tata letak tidak beraturan pada struk _minimarket_ lokal.
- **Kebutuhan Komputasi Ringan:** Kebutuhan akan sistem ekstraksi yang cukup ringan namun akurat untuk diimplementasikan sebagai alat pencatat pengeluaran harian.

---

# 3. Research Mind Map

- **Sistem OCR Pencatatan Pengeluaran Bulanan**
  - **1. Pengumpulan Data**
    - Dataset Publik (Kaggle/Github)
    - Dataset Mandiri (Foto Kamera HP)
  - **2. Pra-Pemrosesan (_Preprocessing_)**
    - Resizing & Normalisasi
    - Augmentasi (Rotasi, Pencahayaan, Noise)
  - **3. Pemodelan & Ekstraksi (_Core AI_)**
    - Algoritma: [Pilih: Donut / EasyOCR + Regex]
    - Pengenalan Karakter (Teks)
    - Pemahaman Tata Letak (_Key-Value Extraction_)
  - **4. Luaran Data (_Output_)**
    - Nama Toko
    - Tanggal
    - Total Belanja
  - **5. Integrasi Aplikasi**
    - Penyimpanan ke _Database_ (Pencatatan Keuangan)
    - Antarmuka Pengguna (_Dashboard_ Pengeluaran)

---

# 4. Rencana Evaluasi Metric

Untuk mengukur performa dari algoritma yang diusulkan, penelitian ini akan menggunakan beberapa metrik evaluasi standar dalam _Computer Vision_ dan _Natural Language Processing_ (NLP):

1. **Character Error Rate (CER):** Untuk mengukur seberapa banyak kesalahan karakter yang dibaca oleh OCR dibandingkan dengan teks aslinya (sangat penting untuk keakuratan angka Total).
2. **Word Error Rate (WER):** Untuk mengukur tingkat kesalahan pengenalan kata secara keseluruhan.
3. **Precision:** Mengukur persentase entitas (Toko, Tanggal, Total) yang diekstraksi oleh sistem yang benar-benar relevan.
4. **Recall:** Mengukur kemampuan sistem dalam menemukan seluruh entitas target yang ada di dalam struk.
5. **F1-Score:** Rata-rata harmonis dari _Precision_ dan _Recall_, memberikan gambaran performa keseluruhan sistem dalam mengekstraksi informasi yang tepat.
