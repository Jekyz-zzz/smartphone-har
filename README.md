# Klasifikasi Aktivitas Manusia dari Sinyal Akselerometer (WISDM v1.1)

Proyek UTS Pengenalan Pola, Kelompok Suki L. Membandingkan fitur manual + SVM dan Random Forest dengan 1D-CNN pada dataset WISDM v1.1 dengan pembagian data per subjek.

## Cara menjalankan
1. Unduh dataset WISDM Activity Prediction v1.1 dari https://www.cis.fordham.edu/wisdm/dataset.php, lalu ekstrak file `WISDM_ar_v1.1_raw.txt`.
2. Buka `UTSPengenolanPola_KelompokSukiL.ipynb` di Google Colab, lalu pilih Runtime → Change runtime type → T4 GPU.
3. Unggah `WISDM_ar_v1.1_raw.txt` ke Colab (tunggu sampai unggahan selesai), atau sesuaikan variabel `PATH` di sel 2.1.
4. Jalankan semua sel (Runtime → Run all). Semua tabel dan gambar hasil tersimpan di folder `hasil/`.

## Dependensi
Python 3.13, lihat `requirements.txt`. Semua pustaka sudah tersedia di Google Colab.

## Pembagian subjek
- Train (25 subjek): 1, 2, 3, 4, 5, 6, 7, 8, 10, 11, 14, 17, 18, 20, 23, 25, 26, 28, 30, 31, 32, 33, 34, 35, 36
- Validasi (5 subjek): 9, 13, 21, 24, 29
- Test (6 subjek): 12, 15, 16, 19, 22, 27

Daftar lengkap juga tersedia di `pembagian_subjek.csv`.

## Keterulangan
Semua pengulangan memakai seed 42, 7, 123, 2024, dan 99, dan determinisme TensorFlow diaktifkan di sel 2.2. Hasil SVM dan Random Forest akan sama saat dijalankan ulang. Hasil 1D-CNN seharusnya sama atau sangat dekat, karena beberapa operasi GPU bisa sedikit berbeda antarversi runtime Colab. Waktu komputasi dapat berbeda karena bergantung pada beban server. Angka di laporan berasal dari run yang outputnya tersimpan di notebook ini dan di file rekap hasil.

## Sumber data
Kwapisz, J. R., Weiss, G. M., & Moore, S. A. (2010). Activity recognition using cell phone accelerometers. SensorKDD-10, Washington DC.

## Hasil

Rata-rata ± simpangan baku dari 5 seed pada data test (6 subjek). SVM bersifat deterministik sehingga hasilnya sama di semua seed.

| Model | Masukan | Accuracy | Macro-F1 | Waktu latih (s) | Inferensi (ms/sampel) |
|---|---|---|---|---|---|
| SVM (RBF) | 79 fitur manual | 0.8745 | 0.8395 | 0.87 ± 0.02 | 0.2267 ± 0.0089 |
| Random Forest | 79 fitur manual | 0.9031 ± 0.0081 | 0.8359 ± 0.0179 | 21.19 ± 2.50 | 0.0888 ± 0.0003 |
| 1D-CNN | Segmen sinyal 128 × 3 | 0.8511 ± 0.0518 | 0.8061 ± 0.0567 | 48.32 ± 11.89 | 0.2429 ± 0.0079 |

SVM dan Random Forest dilatih di CPU (2 core), 1D-CNN di GPU Tesla T4. Waktu inferensi diukur di CPU, dan untuk SVM serta Random Forest sudah termasuk ekstraksi fitur.

## Rekap hasil

Rekap lengkap per seed, per kelas, ablasi kelompok fitur, dan tuning hyperparameter ada di [results/Rekap Hasil_Kelompok Suki L.xlsx](results/Rekap%20Hasil_Kelompok%20Suki%20L.xlsx). Confusion matrix dan kurva loss ada di folder [results/figures](results/figures).

## Tim

Kelompok Suki L, mata kuliah Pengenalan Pola, Teknik Informatika, Fakultas Ilmu Komputer, Universitas Sriwijaya (2026).

- Muhammad Zahy Riza
- Rahmat Hedo Alfikri
- Wahyu Pratama

## Lisensi

MIT, lihat [LICENSE](LICENSE).
