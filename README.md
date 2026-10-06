# 📊 Analisis Performa Pelanggan dan Produk Dari Data Superstore

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
3. **Outlier:** ditemukan outlier pada kolom Quantity (1,70%), Sales (11,68%), Discount (8,57%), dan Profit (18,82%). Outlier dianggap valid sehingga tidak dilakukan penanganan khusus (disarankan konfirmasi ke pemberi data). Tidak terdapat outlier pada kolom lainnya.
4. **Export:** data bersih diekspor ke Excel (`Sample - Superstore Clean Dataset.xlsx`) untuk divisualisasikan di Tableau.

## 📈 KPI Utama

| Total Keuntungan | Total Penjualan | Margin Keuntungan | Jumlah Pelanggan | Total Pesanan |
|:---:|:---:|:---:|:---:|:---:|
| $286.397,02 | $2.297.200,86 | 12,47% | 793 | 5.009 |

## 🔍 Insight dari Data

Dari total penjualan sebesar $2.297.200,86, perusahaan berhasil membukukan keuntungan $286.397,02 atau margin 12,47%. Angka ini tampak positif, namun di baliknya terdapat beberapa pola menarik yang layak diperhatikan.

Diskon menjadi titik awal cerita. Data menunjukkan hubungan negatif antara besarnya diskon dan keuntungan: semakin besar diskon, semakin besar pula kecenderungan terjadinya kerugian. Tanpa diskon, Technology mampu menghasilkan margin 33,96%, Office Supplies 29,52%, dan Furniture 22,71%. Ketika diskon mencapai rentang 21%–30%, Furniture mulai merugi dengan margin -10,75%. Pada diskon di atas 30%, seluruh kategori mengalami kerugian, yaitu Furniture -45,76%, Office Supplies -119,27%, dan Technology -27,41%. Hal ini dapat terjadi karena diskon memotong harga jual, sementara biaya modal dan operasional tetap sama.

Dampak diskon terasa paling besar pada Furniture. Kategori ini hanya mencatat margin sekitar 1%–4% sepanjang 2014–2017 dan kembali menurun di tahun terakhir. Penyebab utamanya adalah sub-kategori Tables yang merugi $17.725,48 dan Bookcases yang merugi $3.472,56, kemungkinan akibat diskon yang terlalu besar serta biaya logistik yang tinggi. Office Supplies juga mengalami penurunan margin di tahun terakhir, dan hal ini diduga berkaitan dengan pemberian diskon di atas 20%. Sementara itu, sub-kategori Supplies turut mencatat kerugian sebesar $1.189,10.

Di sisi lain, Technology tampil sebagai penopang keuntungan. Technology memberi keuntungan terbesar di seluruh segmen dan menjadi kategori dengan margin tertinggi di tahun terakhir, dengan Copiers ($55.617,82), Phones ($44.515,73), dan Accessories ($41.936,64) sebagai sub-kategori paling menguntungkan. Menariknya, Office Supplies justru mendominasi jumlah pesanan (60,30%) dan kuantitas terjual, sehingga volume penjualan terbesar tidak selalu sejalan dengan keuntungan terbesar.

Cerita serupa terlihat pada segmen pelanggan. Consumer menyumbang keuntungan terbesar dan lebih dari separuh pesanan, tetapi memiliki margin paling rendah. Sebaliknya, Home Office memiliki margin paling tinggi namun kontribusi pesanan dan keuntungan paling kecil. Kondisi ini menunjukkan bahwa strategi penjualan masih cenderung terfokus pada segmen Consumer, sehingga potensi segmen Home Office belum tergarap optimal.

## 💡 Recommendation

Berdasarkan temuan di atas, beberapa langkah berikut dapat dipertimbangkan untuk menjaga keuntungan perusahaan.

Pertama, disarankan untuk membatasi diskon maksimum sebesar 20%. Mengingat diskon di atas 20% konsisten menimbulkan kerugian, perusahaan dapat mempertimbangkan alternatif promosi yang lebih aman bagi margin, seperti sistem bundling atau gratis ongkos kirim dengan minimum transaksi tertentu.

Kedua, disarankan untuk memperbaiki margin Furniture, khususnya sub-kategori Tables, hingga mendekati 0% dalam waktu 4 bulan. Langkah yang dapat dipertimbangkan antara lain membatasi diskon di bawah 20%, menaikkan harga Tables sekitar 10%, serta menegosiasikan biaya logistik dengan mitra pengiriman. Dengan begitu, Tables diharapkan tidak lagi merugi dan tidak membebani total keuntungan perusahaan.

Ketiga, disarankan untuk meningkatkan transaksi dan penjualan segmen Home Office sebesar 10% dalam waktu 4 bulan. Hal ini dapat dilakukan melalui campaign marketing, misalnya iklan di Facebook, Instagram, dan TikTok yang ditargetkan kepada pekerja freelance dan pekerja WFH, serta didukung promo bundling. Mengingat segmen ini memiliki margin tertinggi, peningkatan transaksinya berpotensi memberi kontribusi keuntungan yang lebih sehat bagi perusahaan.

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
