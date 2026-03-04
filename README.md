# 📊 SMB Seller Performance Analysis

## 📓 Notebook Analisis
- [`Data_Pre-Processing_e-commerce.ipynb`](notebook/Data_Pre-Processing_e-commerce.ipynb)  
  Notebook yang berisi proses persiapan data, baik dari data cleaning hingga agregrasi dataset
- [`EDA_e-commerce.ipynb`](notebook/EDA_e-commerce.ipynb)  
  Notebook utama yang berisi proses eksplorasi data, untuk menjawab business question.
  
## 📌 Project Overview

Proyek ini menganalisis performa seller UMKM pada marketplace. Tujuan utama analisis ini adalah mengidentifikasi perbedaan karakteristik antara seller dengan performa tinggi dan rendah serta menentukan strategi yang dapat membantu seller kecil meningkatkan performa penjualan mereka.

---

## 📊 Business Context

Sebagian besar penjual di marketplace merupakan pelaku UMKM yang secara kolektif memberikan kontribusi signifikan terhadap Gross Merchandise Value (GMV). Namun, banyak dari mereka mengalami stagnasi dan kesulitan untuk berkembang. Oleh karena itu, diperlukan analisis data mendalam untuk mengidentifikasi faktor-faktor utama yang memengaruhi kinerja dan pertumbuhan penjual UMKM tersebut.

---

## 🎯 Business Questions

1. Mengidentifikasi seller dengan performa tinggi dan rendah  
2. Menemukan faktor utama yang memengaruhi GMV seller  
3. Mengevaluasi apakah perbaikan operasional memiliki dampak signifikan terhadap performa seller  
4. Memberikan rekomendasi strategi berbasis data untuk meningkatkan performa seller  

---

## 📂 Dataset

Dataset yang digunakan adalah [Brazilian E-Commerce Public Dataset (Olist)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data) yang tersedia di Kaggle.

Dataset ini terdiri dari beberapa tabel utama:

- `orders`
- `order_items`
- `payments`
- `reviews`
- `products`

Data dari beberapa tabel tersebut digabungkan dan diproses menjadi dua dataset utama:

- **Order-level dataset**
- **Seller-level dataset**

---

## 🔍 Analysis Approach

### 1️⃣ Data Preprocessing

Tahap ini dilakukan untuk memastikan kualitas data sebelum analisis dilakukan.

Beberapa proses yang dilakukan:

- Memperbaiki tipe data pada fitur yang diperlukan
- Menyeleksi fitur yang relevan untuk kebutuhan analisis pada setiap dataset
- Melakukan feature engineering untuk mempermudah analisis, antara lain:
  - `seller_processing_days`
  - `delivery_time_days`
  - `delivery_delay_days`

---

### 2️⃣ Dataset Aggregation

Data dari beberapa tabel digabungkan secara bertahap untuk membentuk dataset analisis.

**Order-Level Dataset**
- Grain: **1 baris = 1 order**
- Dataset yang digunakan:
  - `orders`
  - `payments`
  - `reviews`
- Join dilakukan menggunakan **order_id**

**Item-Level Dataset**
- Grain: **1 baris = 1 item dalam order**
- Dataset yang digunakan:
  - `order_items`
  - `order_level`
  - `products`

Proses join:
- `order_items` + `order_level` *(inner join, on = order_id)*
- hasil join + `products` *(left join, on = product_id)*

**Seller-Level Dataset**
- Grain: **1 baris = 1 seller**
- Dataset item-level kemudian diagregasi untuk menghasilkan metrik performa tiap seller.

---

### 3️⃣ Exploratory Data Analysis (EDA)

Dataset yang sudah berada pada **seller-level** kemudian dianalisis untuk menjawab business questions.

Analisis dilakukan dengan:
- membandingkan performa **Top 25% vs Bottom 25% seller**
- mengidentifikasi faktor yang memengaruhi GMV
- melakukan **gap analysis** antar kelompok seller

## 💡 Key Findings

### 🔥 GMV Sangat Terkonsentrasi

Distribusi GMV menunjukkan konsentrasi yang sangat tinggi pada sebagian kecil seller:

- **Top 25% seller menyumbang 86.78% GMV**
- **Top 10% seller menyumbang 67.18% GMV**
- **Top 5% seller menyumbang 53.05% GMV**

Hal ini menunjukkan pola **power-law distribution**, di mana sebagian kecil seller menyumbang sebagian besar pendapatan marketplace.

---

### 📈 Volume Penjualan adalah Driver Utama GMV

Perbandingan median antara Top 25% dan Bottom 25% seller:

| KPI | Top 25% | Bottom 25% |
|-----|--------|-----------|
| Total Orders | 60 | 1 |
| Average Item Price | 138 | 49 |
| Processing Time | 1 hari | 2 hari |

Temuan utama:

- Gap volume transaksi mencapai **60x**
- Gap harga hanya sekitar **2.8x**

Artinya:

> Perbedaan GMV terutama didorong oleh volume transaksi, bukan harga produk.

---

### ⚠️ Efisiensi Operasional Bukan Pembeda Utama

Perbedaan metrik operasional antara top seller dan bottom seller relatif kecil.

Hal ini menunjukkan bahwa:

> Efisiensi operasional lebih berfungsi sebagai **hygiene factor** daripada **growth driver**.

Perbaikan operasional saja tidak cukup untuk meningkatkan GMV seller secara signifikan.

---

## 🚀 Strategic Recommendations

### Short-Term — Risk Mitigation

Fokus mempertahankan **Top 5% seller** karena mereka menyumbang lebih dari setengah GMV marketplace.

---

### Medium-Term — Growth Acceleration

Fokus pada **Middle 50% seller** yang memiliki potensi besar untuk berkembang melalui:

- peningkatan exposure
- partisipasi dalam campaign
- optimasi listing produk

---

### Selective Intervention for Bottom Sellers

Tidak semua seller dengan performa rendah perlu ditingkatkan.

Seller bottom dapat dibagi menjadi:

- seller dengan potensi pertumbuhan
- seller dengan performa struktural rendah

Strategi awal yang disarankan adalah meningkatkan exposure untuk menguji potensi demand sebelum melakukan intervensi operasional.

---

## 🧠 Key Business Insight

Performa seller dengan GMV rendah lebih disebabkan oleh **kurangnya volume transaksi dan exposure**, bukan oleh kualitas operasional yang buruk.

Strategi pertumbuhan marketplace sebaiknya lebih fokus pada **peningkatan traffic dan demand** daripada hanya meningkatkan efisiensi operasional.

---

## 🛠 Tools Used

Analisis dilakukan menggunakan:

- **Python**
- **Pandas**
- **Jupyter Notebook**

Python digunakan untuk proses data cleaning, agregasi data, segmentasi seller, dan analisis eksploratif.

---
