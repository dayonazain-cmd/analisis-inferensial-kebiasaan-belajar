# Analisis Inferensial Kebiasaan Belajar Mahasiswa

## Tentang Proyek
Repositori ini berisi implementasi **Analisis Statistik Inferensial** untuk menguji hipotesis pada data kebiasaan belajar mahasiswa (n = 30). 

Proyek ini mendemonstrasikan penggunaan berbagai uji statistik parametrik dan non-parametrik, mulai dari estimasi interval (Confidence Intervals), uji perbedaan (t-Test, ANOVA), uji hubungan (Korelasi Pearson, Chi-Square), hingga pemodelan prediktif (Regresi Linear Berganda).

## Struktur Repositori
- `analisis_inferensial_kebiasaan_belajar.ipynb` : Jupyter Notebook utama berisi kode pengujian statistik dan visualisasi.
- `Rekap Data Wawancara.xlsx` : Dataset mentah yang digunakan (n=30).
- `PANDUAN_ANALISIS_INFERENSIAL.md` : Dokumentasi lengkap mengenai metodologi dan formula statistik yang digunakan.
- `INTEGRASI_KE_LAPORAN.md` : Panduan cara menuliskan hasil output Python ke dalam laporan formal.
- `QUICK_REFERENCE_INFERENSIAL.txt` : Cheat sheet ringkas untuk memilih uji statistik yang tepat.

## Uji Statistik yang Dilakukan
1. **Confidence Intervals (95% CI):** Estimasi parameter populasi.
2. **One-Sample & Independent t-Test:** Uji perbedaan rata-rata.
3. **One-Way ANOVA & Post-Hoc Tukey HSD:** Uji perbandingan multi-grup (berdasarkan IPK).
4. **Linear Regression:** Pemodelan prediksi Kepuasan Belajar berdasarkan Jam Belajar, Frekuensi, dan Distraksi.
5. **Pearson Correlation & Chi-Square:** Analisis hubungan antar variabel kontinu dan kategorikal.

## Cara Menjalankan Proyek
1. Unduh file `.ipynb` dan `.xlsx` dari repositori ini.
2. Buka file `.ipynb` menggunakan Google Colab.
3. Unggah file `.xlsx` ke dalam *session storage* Google Colab.
4. Klik menu Runtime > Restart and Run All.
