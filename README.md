# 🛒 Association Rule Mining (Market Basket Analysis) — Data Mining

[![Python Version](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Library-mlxtend](https://img.shields.io/badge/Library-mlxtend-brightgreen)](http://rasbt.github.io/mlxtend/)
[![Domain](https://img.shields.io/badge/Domain-Retail%20%26%20FnB%20Analytics-purple)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

Repositori ini berisi implementasi menyeluruh teknik **Association Rule Mining (Market Basket Analysis)** untuk mengekstraksi pola tersembunyi (*hidden co-occurrence patterns*) dari data transaksi ritel dan *Food & Beverage* (F&B). Proyek ini mencakup eksplorasi ambang batas, perhitungan metrik evaluasi mendalam, *benchmarking* algoritma **Apriori vs FP-Growth**, hingga studi kasus *end-to-end* mandiri pada transaksi kedai kopi modern.

---

## 📌 Daftar Isi
- [Latar Belakang & Konsep](#-latar-belakang--konsep)
- [Struktur Repositori](#-struktur-repositori)
- [Ringkasan Tugas & Eksperimen](#-ringkasan-tugas--eksperimen)
  - [00. Praktikum Modul (Baseline)](#00-praktikum-modul-baseline)
  - [01. Tugas 1 — Ambang Batas Support & Confidence](#01-tugas-1--ambang-batas-support--confidence)
  - [02. Tugas 2 — Analisis Metrik Lanjutan (Leverage & Conviction)](#02-tugas-2--analisis-metrik-lanjutan-leverage--conviction)
  - [03. Tugas 3 — Benchmark Komparasi Apriori vs FP-Growth](#03-tugas-3--benchmark-komparasi-apriori-vs-fp-growth)
  - [04. Tugas 4 — Studi Kasus Mandiri: Kedai Kopi "Kopi Kenangan Senja"](#04-tugas-4--studi-kasus-mandiri-kedai-kopi-kopi-kenangan-senja)
- [Formulasi Metrik Evaluasi](#-formulasi-metrik-evaluasi)
- [Panduan Instalasi & Eksekusi](#-panduan-instalasi--eksekusi)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Kontributor & Lisensi](#-kontributor--lisensi)

---

## 🧠 Latar Belakang & Konsep

**Association Rule Mining (ARM)** adalah salah satu teknik data mining nir-terawasi (*unsupervised learning*) fundamental yang bertujuan menemukan hubungan implikasi antar-item berbentuk:

$$\{X\} \implies \{Y\}$$

Di mana pembelian itemset anteseden ($X$) berkorelasi signifikan terhadap pembelian itemset konsekuen ($Y$). Analisis ini memungkinkan pelaku bisnis mengoptimalkan:
1. **Product Bundling / Promo Paket**: Menjual produk berpasangan dengan harga spesial.
2. **Store Shelf Layout / Cross-Merchandising**: Penataan rak fisik atau etalase digital yang saling mendekatkan produk berkorelasi.
3. **Recommendation Engine & POS Upselling**: Strategi kasir atau sistem checkout cerdas dalam menyarankan item pelengkap secara *real-time*.

---

## 📂 Struktur Repositori

```text
├── 00_praktikum_modul.ipynb            # Hands-on dasar alur ARM modul praktikum (Bagian 4.1 - 4.8)
├── 01_tugas_1_ambang_batas.ipynb       # Eksplorasi & sweep threshold min_support & min_confidence
├── 02_tugas_2_analisis_aturan.ipynb    # Perhitungan manual & interpretasi Leverage, Conviction, dll.
├── 03_tugas_3_apriori_vs_fpgrowth.ipynb# Benchmark performa & skalabilitas runtime Apriori vs FP-Growth
├── 04_tugas_4_studi_kasus_mandiri.ipynb# Analisis end-to-end transaksi kedai kopi mandiri
├── coffee_shop_transactions.csv        # Dataset transaksi 50 struk kedai kopi (10 menu)
├── coffee_shop_rules.csv               # Hasil ekstraksi aturan asosiasi final dari studi kasus
├── requirements.txt                    # Daftar dependensi library Python
└── README.md                           # Dokumentasi proyek
```

---

## 🔬 Ringkasan Tugas & Eksperimen

### 00. Praktikum Modul (Baseline)
- **Dataset**: 60 transaksi toko kelontong dengan 12 kategori item kebutuhan pokok.
- **Pipeline**: One-Hot Encoding (`TransactionEncoder`), Frequent Itemset Discovery (`apriori`), dan Rule Generation (`association_rules`).
- **Insight**: Teridentifikasi 3 klaster belanja utama:
  - *Klaster Sarapan*: $\{\text{Mentega, Susu}\} \rightarrow \{\text{Roti}\}$ ($\text{Lift} = 3.33, \text{Confidence} = 100\%$).
  - *Klaster Kebersihan*: Sabun Mandi, Sampo, dan Pasta Gigi.
  - *Klaster Dapur/Bumbu*: Minyak Goreng, Bawang Merah, dan Beras.

### 01. Tugas 1 — Ambang Batas Support & Confidence
- Menganalisis fenomena **Rule Explosion** vs **Rule Starvation**:
  - Penurunan $\text{min\_support}$ dari $0.15 \rightarrow 0.10$ meningkatkan jumlah kandidat itemset secara eksponensial (menjaring item-item *long-tail*).
  - Peningkatan $\text{min\_confidence} \rightarrow 0.70$ menyaring hanya aturan dengan reliabilitas tinggi (*high certainty*).
- Dilengkapi kurva **Threshold Sweep Analysis** untuk mengamati sensitivitas metrik terhadap kuantitas aturan yang terbentuk.

### 02. Tugas 2 — Analisis Metrik Lanjutan (Leverage & Conviction)
- Melakukan verifikasi validasi matematis melalui **perhitungan manual versus output `mlxtend`** untuk aturan terpilih:
  - **Support & Confidence**: Menakar frekuensi dan kepastian aturan.
  - **Lift**: Mengukur derajat ketergantungan asosiatif dibanding probabilitas acak ($\text{Lift} > 1$).
  - **Leverage**: Selisih probabilitas aktual dengan probabilitas independen ($P(X \cap Y) - P(X)P(Y)$).
  - **Conviction**: Sensitivitas aturan jika konsekuen tidak terjadi saat anteseden ada ($\frac{1 - P(Y)}{1 - \text{Confidence}}$). Nilai $\infty$ menunjukkan kepastian deterministik ($100\%$ confidence).

### 03. Tugas 3 — Benchmark Komparasi Apriori vs FP-Growth
- **Eksperimen Stress Test** pada $\text{min\_support} = 0.05$ (ambang batas rendah):
  - **Algoritma Apriori**: Menggunakan pendekatan *generate-and-test* (prinsip anti-monoton). Membutuhkan *multiple database scans* dan menghasilkan kombinasi kandidat $k$-itemset yang masif di memori.
  - **Algoritma FP-Growth (*Frequent Pattern Growth*)**: Menggunakan struktur data *FP-Tree (Frequent Pattern Tree)* terkompresi. Hanya membutuhkan **2 kali pembacaan database** dan langsung mengekstrak itemset melalui *Conditional Pattern Base*.
- **Hasil**: FP-Growth secara konsisten unggul drastis dari segi waktu eksekusi (*runtime speedup*) dan efisiensi memori ketika support diturunkan.

### 04. Tugas 4 — Studi Kasus Mandiri: Kedai Kopi "Kopi Kenangan Senja"
- **Profil Data**: 50 transaksi struk pesanan dengan 10 varian menu modern (Espresso, Americano, Kopi Susu Aren, Matcha Latte, Croissant Butter, Toast Kaya, Red Velvet Cake, dll.).
- **Top Rules Ditemukan**:
  1. $\{\text{Matcha Latte}\} \implies \{\text{Red Velvet Cake}\}$: $\text{Lift} = 5.56, \text{Confidence} = 88.9\%$.
  2. $\{\text{Americano}\} \implies \{\text{Sandwich Tuna}\}$: $\text{Lift} = 4.55, \text{Confidence} = 90.9\%$.
  3. $\{\text{Kopi Susu Aren}\} \implies \{\text{Croissant Butter}\}$: $\text{Lift} = 2.14, \text{Confidence} = 94.1\%$.
- **Rekomendasi Strategis Terapan**:
  - 🍰 **Paket "Sweet Matcha Break"**: Bundling Matcha Latte + Red Velvet Cake untuk jam santai sore hari (14.00–17.00).
  - 🥪 **Paket "Executive Quick Lunch"**: Menu kombo Americano + Sandwich Tuna menyasar pekerja kantor saat jam makan siang.
  - 🥐 **Display Showcase & Kasir Scripting**: Menempatkan Croissant Butter di samping mesin POS dan melatih barista melakukan upselling langsung saat pelanggan memesan Kopi Susu Aren.

---

## 📐 Formulasi Metrik Evaluasi

| Metrik | Formula Matematis | Rentang Nilai | Interpretasi Ideal |
| :--- | :--- | :--- | :--- |
| **Support** | $\text{Supp}(X \implies Y) = \frac{\sigma(X \cup Y)}{N} = P(X \cap Y)$ | $[0, 1]$ | Frekuensi kemunculan bersama dalam seluruh transaksi |
| **Confidence** | $\text{Conf}(X \implies Y) = \frac{P(X \cap Y)}{P(X)}$ | $[0, 1]$ | Probabilitas bersyarat $Y$ dibeli jika $X$ dibeli |
| **Lift** | $\text{Lift}(X \implies Y) = \frac{\text{Conf}(X \implies Y)}{P(Y)} = \frac{P(X \cap Y)}{P(X)P(Y)}$ | $[0, \infty)$ | $> 1$ menunjukkan korelasi positif yang saling menguntungkan |
| **Leverage** | $\text{Lev}(X \implies Y) = P(X \cap Y) - P(X)P(Y)$ | $[-0.25, 0.25]$ | $> 0$ mengindikasikan surplus ko-okurensi dibanding peluang acak |
| **Conviction** | $\text{Conv}(X \implies Y) = \frac{1 - P(Y)}{1 - \text{Conf}(X \implies Y)}$ | $[0, \infty]$ | Semakin tinggi, semakin kuat aturan tidak meleset |

---

## 🚀 Panduan Instalasi & Eksekusi

### 1. Clone Repositori
```bash
git clone https://github.com/ZidaneZaida/DM-Asosiation.git
cd DM-Asosiation
```

### 2. Buat Lingkungan Virtual (Opsional namun Disarankan)
```bash
python3 -m venv venv
source venv/bin/activate  # Di Linux/macOS
# venv\Scripts\activate   # Di Windows
```

### 3. Instal Dependensi
```bash
pip install -r requirements.txt
```

### 4. Jalankan Jupyter Notebook
```bash
jupyter notebook
```
Buka file notebook secara berurutan mulai dari `00_praktikum_modul.ipynb` hingga `04_tugas_4_studi_kasus_mandiri.ipynb`.

---

## 🛠 Teknologi yang Digunakan

- **Language**: Python 3.x
- **Data Manipulation**: `pandas`, `numpy`
- **Data Mining & Analytics**: `mlxtend` (`TransactionEncoder`, `apriori`, `fpgrowth`, `association_rules`)
- **Data Visualization**: `matplotlib`, `seaborn`
- **Interactive Environment**: Jupyter Notebook

---

## 👤 Kontributor

- **Repository Owner**: [ZidaneZaida](https://github.com/ZidaneZaida)
- **Topik**: Praktikum Data Mining — Association Rule Mining / Market Basket Analysis

---
*Dibuat untuk keperluan akademik dan dokumentasi analisis Data Mining.*
