# 📊 Analisis Performa Pelanggan dan Produk (Superstore)

## 📌 Overview Project
Project ini bertujuan untuk menganalisis performa keuntungan perusahaan ritel berdasarkan kategori produk, sub-kategori, segmen pelanggan, dan pemberian diskon.

Analisis dilakukan menggunakan **Superstore Dataset** yang berisi informasi pesanan seperti tanggal pemesanan, metode pengiriman, segmen pelanggan, lokasi, kategori produk, nilai penjualan, kuantitas, diskon, dan keuntungan.

Melalui analisis ini diharapkan dapat diperoleh insight yang membantu perusahaan memahami sumber keuntungan dan kerugian, sehingga dapat mendukung keputusan terkait kebijakan diskon, strategi produk, dan fokus segmen pelanggan.

## ❗ Problem Statement
Pelaku usaha ritel menghadapi margin keuntungan yang semakin tipis meskipun penjualan terus meningkat. Kenaikan omzet tidak otomatis diikuti pertumbuhan laba karena pelaku usaha harus memberikan berbagai program diskon untuk menjaga daya beli masyarakat, di tengah kenaikan biaya dan pelemahan nilai tukar rupiah.

> Sumber: [Katadata – Profit Peritel Menyusut Akibat Diskon dan Biaya Naik](https://katadata.co.id/berita/industri/6a74489906fb8/profit-peritel-menyusut-akibat-diskon-dan-biaya-naik) (6 Agustus 2026)

Dengan menganalisis data penjualan, kita dapat mengidentifikasi sumber keuntungan dan kerugian perusahaan. Insight dari analisis ini dapat membantu:

- Manajemen dalam menentukan kebijakan diskon yang tidak merugikan
- Tim produk dalam memperbaiki kategori dan sub-kategori dengan performa rendah
- Tim sales dan marketing dalam menentukan segmen pelanggan yang perlu difokuskan

## ❓ Business Question
Beberapa pertanyaan yang ingin dijawab dalam analisis ini antara lain:

1. Bagaimana performa keuntungan kategori dan sub-kategori? Apakah semuanya menghasilkan keuntungan?
2. Bagaimana margin keuntungan setiap kategori selama empat tahun terakhir?
3. Apakah ada pengaruh diskon terhadap performa keuntungan kategori?
4. Bagaimana performa setiap segmen pelanggan? Apakah segmen dengan keuntungan terbesar memiliki margin keuntungan terbesar?

## 📊 Dataset
- **Nama:** Superstore Dataset
- **Sumber:** [Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final/data)
- **Format:** CSV
- **Jumlah baris:** 9.994
- **Jumlah kolom:** 21

Variabel utama pada dataset:

| Kolom | Deskripsi |
|---|---|
| Row ID | ID unik setiap baris |
| Order ID | ID pesanan unik |
| Order Date | Tanggal pemesanan produk |
| Ship Date | Tanggal pengiriman produk |
| Ship Mode | Metode pengiriman produk |
| Customer ID / Customer Name | ID dan nama pelanggan |
| Segment | Segmen pelanggan (Consumer, Corporate, Home Office) |
| Country, State, City, Postal Code, Region | Informasi lokasi pelanggan |
| Product ID / Product Name | ID dan nama produk |
| Category | Kategori produk (Furniture, Office Supplies, Technology) |
| Sub-Category | Subkategori produk |
| Sales | Nilai penjualan produk |
| Quantity | Jumlah produk |
| Discount | Diskon yang diberikan |
| Profit | Keuntungan/kerugian yang diperoleh |

## 🧹 Data Preparation
1. **Data Exploration:** tidak ditemukan inkonsistensi, missing value, maupun duplicate value.
2. **Tipe data:** kolom `Order Date` dan `Ship Date` masih bertipe string, sehingga diubah menjadi `datetime`.
3. **Outlier:** ditemukan outlier pada kolom Quantity (1,70%), Sales (11,68%), Discount (8,57%), dan Profit (18,82%). Outlier dianggap valid sehingga tidak dilakukan penanganan khusus (disarankan konfirmasi ke pemberi data).
4. **Export:** data bersih diekspor ke Excel (`Sample - Superstore Clean Dataset.xlsx`) untuk divisualisasikan di Tableau.

## 📈 KPI Utama

| Total Keuntungan | Total Penjualan | Margin Keuntungan | Jumlah Pelanggan | Total Pesanan |
|:---:|:---:|:---:|:---:|:---:|
| $286.397,02 | $2.297.200,86 | 12,47% | 793 | 5.009 |

## 🔍 Insight dari Data

### 1. Diskon di atas 20% mengubah untung menjadi rugi
- Terdapat hubungan negatif antara diskon dan keuntungan: semakin besar diskon, semakin cenderung merugi.
- Diskon 21%–30% sudah membuat kategori Furniture rugi (margin -10,75%).
- Diskon di atas 30% membuat **semua kategori** rugi: Furniture -45,76%, Office Supplies -119,27%, Technology -27,41%.
- Margin terbesar ada pada kategori Technology tanpa diskon (33,96%).

### 2. Furniture memiliki margin rendah dan menurun
- Sub-kategori yang merugi: **Tables** (-$17.725,48), **Bookcases** (-$3.472,56), dan **Supplies** (-$1.189,10, kategori Office Supplies).
- Margin Furniture hanya berkisar 1%–4% selama 2014–2017 dan turun di tahun terakhir. Office Supplies juga mengalami penurunan margin di tahun terakhir, kemungkinan akibat diskon di atas 20%.
- Kerugian pada Tables dan Bookcases diduga akibat diskon terlalu besar dan biaya akuisisi/logistik yang tinggi.

### 3. Segmen Home Office: margin terbesar, tetapi kontribusi terkecil
| Segmen | Total Keuntungan | Margin Keuntungan | Proporsi Pesanan |
|---|---:|---:|---:|
| Consumer | $134.119,21 | 11,55% | 51,94% |
| Corporate | $91.979,13 | 13,03% | 30,22% |
| Home Office | $60.298,68 | 14,03% | 17,84% |

Consumer memberi keuntungan terbesar namun dengan margin terkecil, sedangkan Home Office memiliki margin terbesar tetapi jumlah pesanan dan keuntungan paling kecil. Hal ini mengindikasikan penjualan terlalu fokus pada segmen Consumer.

### 4. Insight tambahan
- **Office Supplies** adalah kategori paling dominan berdasarkan total pesanan (60,30%) dan kuantitas terjual, namun **Technology** memberi keuntungan terbesar di semua segmen.
- **Technology** merupakan kategori dengan margin terbesar di tahun terakhir.
- Sub-kategori paling menguntungkan: Copiers ($55.617,82), Phones ($44.515,73), dan Accessories ($41.936,64).

## 💡 Recommendation

### 1. Batasi Diskon Maksimum 20%
Hentikan pemberian diskon di atas 20%. Ganti dengan sistem bundling atau gratis ongkir dengan minimum transaksi.

### 2. Tingkatkan Margin Furniture, Khususnya Sub-Kategori Tables, Menjadi 0% dalam 4 Bulan
- Hentikan diskon di atas 20%
- Naikkan harga Tables sebesar 10% agar margin mendekati 0% (tidak rugi, tidak untung)
- Turunkan biaya logistik melalui negosiasi dengan mitra logistik

### 3. Tingkatkan Transaksi dan Penjualan Segmen Home Office sebesar 10% dalam 4 Bulan
- Jalankan campaign marketing (iklan di Facebook, Instagram, dan TikTok) dengan target audiens pekerja freelance dan pekerja WFH
- Sediakan promo bundling

## 📊 Dashboard
Dashboard interaktif dibuat di Tableau dengan filter **Segment** dan **Kategori**, terdiri dari:

- 5 KPI (Total Keuntungan, Total Penjualan, Margin Keuntungan, Jumlah Pelanggan, Total Pesanan)
- Jumlah keuntungan setiap sub-kategori
- Heatmap hubungan kategori diskon dengan margin keuntungan
- Scatter plot diskon vs keuntungan per kategori
- Margin keuntungan per tahun berdasarkan kategori
- Proporsi segmen pelanggan dan kategori berdasarkan total pesanan
- Heatmap keuntungan, penjualan, dan kuantitas per kategori setiap segmen
- Total keuntungan dan margin keuntungan berdasarkan segmen

(https://github.com/ahmad2129/Mini-Project-Visualisasi/blob/main/dashboard/Dashboard%20Visualisasi.png)

## 📊 Presentasi Project
Untuk melihat penjelasan lengkap dari project ini, silakan lihat slide presentasi berikut:

🔗 [https://github.com/ahmad2129/Mini-Project-Visualisasi/blob/main/report/Presentasi%20Mini%20Project%20Power%20BI%20%26%20Tableau%201%20Ahmad%20Malik%20Ibrahim.pdf](#)

## 🛠 Tools yang Digunakan
- **Python** (Data Exploration, Data Cleaning & Data Preparation)
- **Tableau** (Visualisasi dan Dashboard)
- **Excel** (Format data bersih untuk Tableau)

## 👤 Author
**Ahmad Malik Ibrahim**
Lulusan kedokteran dengan minat pada statistik, analisis, dan matematika, yang sedang menargetkan karir sebagai data analis.
