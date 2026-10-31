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