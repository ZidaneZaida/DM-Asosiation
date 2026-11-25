# Evaluasi Model Klasifikasi pada Deteksi Transaksi Fraud

Folder ini berisi pengerjaan praktikum dan empat tugas modul Data Mining mengenai evaluasi model klasifikasi pada data tidak seimbang (*imbalanced dataset*). Seluruh eksperimen dijalankan di [Praktikum_Evaluasi_Model_Klasifikasi.ipynb](Praktikum_Evaluasi_Model_Klasifikasi.ipynb) menggunakan data sintetis 500 transaksi pembayaran digital yang dibangkitkan secara deterministik (`random_state=42`).

## Kenapa Kasus Ini Menarik

Dari 500 transaksi yang dibuat, hanya 16 transaksi berlabel fraud (3.2%) dan 484 sisanya normal (96.8%). Jika sebuah model menebak semua transaksi sebagai normal tanpa melihat fitur apa pun, akurasinya langsung mencapai 96.67% pada data uji. Angka akurasi setinggi itu menipu karena tidak ada satu pun transaksi fraud yang tertangkap (Recall = 0%).

Saat `DecisionTreeClassifier` (`max_depth=4`, `class_weight='balanced'`) dilatih pada 350 data latih dan diuji pada 150 data uji (berisi 5 kasus fraud), akurasinya memang turun menjadi 76.67%, tetapi model mulai bisa menjaring 2 dari 5 fraud yang ada (Recall = 40%).

## Ringkasan Hasil Eksperimen

| Model / Skenario | Accuracy | Precision (Fraud) | Recall (Fraud) | F1-Score (Fraud) |
| :--- | :---: | :---: | :---: | :---: |
| Baseline (Tebak Normal Semua) | 96.67% | 0.000 | 0.000 | 0.000 |
| Decision Tree (Threshold 0.5) | 76.67% | 0.059 | 0.400 | 0.103 |
| Decision Tree (Threshold 0.2) | 76.67% | 0.059 | 0.400 | 0.103 |
| Decision Tree (Threshold 0.7) | 86.00% | 0.056 | 0.200 | 0.087 |

Pada pohon keputusan berlevel 4 dengan 150 sampel uji, probabilitas di daun pohon mengelompok sehingga menggeser ambang dari 0.5 ke 0.2 tidak mengubah pembagian prediksi (`TP=2, TN=113, FP=32, FN=3`). Begitu ambang dinaikkan ke 0.7, jumlah alarm palsu memang turun hampir separuhnya dari 32 menjadi 17, namun satu kasus fraud ikut lolos (`FN` naik dari 3 ke 4) dan Recall merosot ke 20%.

## Cakupan di Dalam Notebook

1. **Pembangkitan Dataset & Training (Bagian 4.1 hingga 4.2):** Simulasi fitur `amount`, `hour`, `new_device`, dan `foreign_ip`, lalu pembagian data 70:30 dengan `stratify=y`.
2. **Confusion Matrix & Verifikasi Metrik (Bagian 4.3 hingga 4.6):** Ekstraksi `[[113, 32], [3, 2]]`, perbandingan hitung manual melawan fungsi `scikit-learn` (selisih `0.0`), serta visualisasi heatmap.
3. **Uji Baseline & Threshold Tuning (Bagian 4.7 hingga 4.8):** Pembuktian *Accuracy Paradox* dan kurva trade-off Precision terhadap Recall di empat titik threshold (`0.2, 0.4, 0.5, 0.7`).
4. **Penyelesaian Tugas 1 sampai 4:** Hitung manual untuk matriks `TP=24, TN=156, FP=12, FN=8` (`Accuracy 90%`, `Precision 66.67%`, `Recall 75%`, `F1 70.59%`), verifikasi kode Python (`np.allclose = True`), analisis data tidak seimbang, dan argumen pemilihan threshold `0.2` saat biaya fraud lolos jauh lebih mahal daripada salah blokir sementara.

## Cara Menjalankan

Aktifkan virtual environment yang ada atau pakai Python 3.10+ dengan `numpy`, `pandas`, `scikit-learn`, dan `matplotlib`, lalu buka `Praktikum_Evaluasi_Model_Klasifikasi.ipynb` dan jalankan seluruh sel dari atas ke bawah.
