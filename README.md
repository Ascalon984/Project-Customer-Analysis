![dreamina-2026-01-08-6528-A clean and minimalist banner, light gra](https://github.com/user-attachments/assets/7b4e142f-7db7-4c34-afce-4c9a84ec0eb5)

# 🛒 Customer Purchase Analysis Pipeline
> **Transformasi Data Mentah Menjadi Insight Bisnis yang Strategis.**

[![Python](https://img.shields.io/badge/Python-3.9+-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Library-Pandas-150458?style=for-the-badge&logo=pandas)](https://pandas.pydata.org/)
[![Maintenance](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)](#)

---

## 📖 Overview
Proyek ini mengotomatisasi alur kerja analisis data histori pembelian pelanggan. Pipeline ini mencakup pembersihan data otomatis, analisis statistik mendalam, hingga pembuatan dashboard visual untuk mendukung pengambilan keputusan bisnis yang tepat sasaran.

> 🚨 **Business Impact:** Mengidentifikasi produk dengan profitabilitas tertinggi dan memetakan pola perilaku belanja pelanggan berdasarkan waktu transaksi.

---

## 🛠️ Navigasi Modul
Akses dokumentasi teknis dan kode sumber lengkap untuk setiap tahap melalui modul di bawah ini:

| 🧹 [01. Data Cleaning](./01_Cleaning_Data.md) | 📊 [02. Data Analysis](./02_Data_Analysis.md) | 📈 [03. Visualization](./03_Data_Visualization.md) |
| :--- | :--- | :--- |
| *Handling nulls, stripping whitespace, & fixing typos.* | *Sales ranking, lookup functions, & segmenting.* | *Trend analysis & revenue distribution.* |

---

## 📊 Highlight Hasil Analisis
Berikut adalah cuplikan hasil akhir dari pipeline analisis ini:

### 1. Tren Penjualan Bulanan (High-Level View)
Analisis menunjukkan performa penjualan yang stabil dengan puncak pendapatan tertinggi terjadi pada periode Mei hingga Agustus 2023.
<img width="900" alt="Monthly Sales Trend" src="https://github.com/user-attachments/assets/2f20925f-6882-45e0-93b7-a99a68cdb5a1" />

### 2. Sebaran Kategori Produk (Market Share)
Visualisasi ini menunjukkan dominasi kategori produk berdasarkan total pendapatan yang dihasilkan oleh bisnis.
<img width="900" alt="Category Distribution" src="https://github.com/user-attachments/assets/f19adc61-0388-4758-a1e0-3b88a0657ad4" />

---

💡 Temuan Utama (Executive Insights)
Market Leader (Office Supplies): Kategori Office Supplies merupakan penyumbang pendapatan terbesar dengan total transaksi mencapai 1.130.290,02, diikuti oleh Furniture dan Electronics.

Segmentasi Produk: Menggunakan algoritma kustom, produk berhasil diklasifikasikan menjadi 4 kategori. Segmen Ekonomis mendominasi dengan total 706 produk, menunjukkan bahwa strategi harga terjangkau menjadi daya tarik utama bagi pelanggan.

Tren Pendapatan Bulanan: Performa penjualan menunjukkan stabilitas tinggi dengan puncak pendapatan (Revenue Peak) terjadi pada periode Mei - Agustus, di mana rata-rata pendapatan bulanan konsisten berada di atas 116.000.

Preferensi Pembayaran: Pelanggan menunjukkan adopsi pembayaran digital yang kuat, di mana penggunaan Debit Card menempati urutan teratas (396 transaksi), disusul oleh metode Cash dan Gift Card.

Loyalitas Produk (Ranking): Produk seperti Printer dan Laptop konsisten menempati peringkat teratas berdasarkan akumulasi TotalPrice, menjadikannya komoditas paling berharga dalam inventaris.

---

## 🚀 Cara Menjalankan Proyek
1. Clone repositori ini.
2. Pastikan file `Customer-Purchase-History.xlsx` tersedia di folder utama.
3. Install dependensi: `pip install pandas matplotlib openpyxl`.
4. Jalankan script Python sesuai urutan penomoran.

---
Organized by **[Aditya Tri Prasetyo]** • 2026 | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/aditya-tri-prasetyo-7b3a0a396) [![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=flat-square&logo=instagram&logoColor=white)](https://instagram.com/aditya.trisetya)
