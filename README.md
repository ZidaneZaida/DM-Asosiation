# Kumpulan Praktikum & Tugas Data Mining

Repositori ini menyimpan seluruh catatan, kode eksperimen, dan penyelesaian tugas mata kuliah Data Mining (Universitas Negeri Padang, 2026). Tiap topik ditempatkan pada foldernya masing-masing supaya mudah ditelusuri dan terus bertambah seiring berjalannya perkuliahan.

## Daftar Modul dan Status

| Topik | Folder | Fokus Utama | Status |
| :--- | :--- | :--- | :---: |
| Association Rule Mining | [ARM/](ARM/README.md) | Market Basket Analysis, Apriori vs FP-Growth, studi kasus kedai kopi | Selesai |
| Evaluasi Model Klasifikasi | [evaluasi_model/](evaluasi_model/README.md) | Confusion Matrix, *Accuracy Paradox*, dan *threshold tuning* pada deteksi fraud | Selesai |

## Sorotan Tiap Topik

### 1. Association Rule Mining ([ARM/](ARM/README.md))
Mulai dari 60 transaksi toko kelontong sampai studi kasus mandiri 50 struk kedai kopi, bagian ini menguji bagaimana aturan asosiasi terbentuk ketika `min_support` dan `min_confidence` digeser. Di dalamnya juga ada verifikasi hitung manual metrik *Leverage* serta *Conviction*, plus adu cepat waktu eksekusi antara algoritma Apriori dan FP-Growth pada support rendah (`0.05`).

### 2. Evaluasi Model Klasifikasi ([evaluasi_model/](evaluasi_model/README.md))
Mengangkat simulasi 500 transaksi pembayaran digital dengan rasio fraud hanya 3.2%. Eksperimen di folder ini memperlihatkan kenapa model tebak normal bisa mencetak akurasi 96.67% padahal gagal total menangkap penipuan, sekaligus membandingkan efek pergeseran threshold (`0.2`, `0.4`, `0.5`, `0.7`) pada `DecisionTreeClassifier` terhadap nilai Precision dan Recall.

## Struktur Direktori

```text
.
├── ARM/
│   ├── 00_praktikum_modul.ipynb
│   ├── 01_tugas_1_ambang_batas.ipynb
│   ├── 02_tugas_2_analisis_aturan.ipynb
│   ├── 03_tugas_3_apriori_vs_fpgrowth.ipynb
│   ├── 04_tugas_4_studi_kasus_mandiri.ipynb
│   ├── coffee_shop_transactions.csv
│   ├── coffee_shop_rules.csv
│   ├── requirements.txt
│   └── README.md
├── evaluasi_model/
│   ├── Praktikum_Evaluasi_Model_Klasifikasi.ipynb
│   └── README.md
└── README.md
```

## Menjalankan Notebook Secara Lokal

Setiap folder punya kebutuhan pustaka yang ringan dan standar untuk olah data Python (`pandas`, `numpy`, `scikit-learn`, `matplotlib`, dan `mlxtend` untuk bagian ARM).

```bash
git clone https://github.com/ZidaneZaida/DM-Asosiation.git
cd DM-Asosiation
python3 -m venv .venv
source .venv/bin/activate
pip install -r ARM/requirements.txt scikit-learn matplotlib
```

Setelah dependensi terpasang, buka file `.ipynb` pada folder topik yang ingin dijalankan lewat Jupyter Notebook atau VS Code. Modul baru akan terus ditambahkan ke daftar di atas mengikuti jadwal praktikum berikutnya.
