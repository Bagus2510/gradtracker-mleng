# GradTracker ML Future Roadmap

## 1. Latar Belakang
Sesuai masukan dari mentor (Mas Angga), fitur analisis mata kuliah spesifik sangat diminati untuk membantu Kaprodi mengetahui persis mata kuliah mana yang menyebabkan mahasiswa drop (terlambat lulus).

## 2. Kondisi Saat Ini (Model V1)
Model Machine Learning saat ini (`xgb_model_tuned.pkl`) menggunakan 6 fitur makro:
1. Umur
2. Status Menikah
3. Status Bekerja
4. Rata-rata IPS
5. IPS Drop (Penurunan antar semester terakhir)
6. Semester Saat Ini

Fitur-fitur ini **tidak memiliki granularitas tingkat mata kuliah**, sehingga model tidak bisa "menunjuk" mata kuliah spesifik (misal: Kalkulus 2, Algoritma Pemrograman) sebagai penyebab risiko.

## 3. Rencana Pengembangan (Model V2 - Course-Level Analysis)

### Fase 1: Pengumpulan Dataset Transkrip Historis
- **Kebutuhan Data**: Alih-alih agregat IPS, sistem butuh data transkrip lengkap mahasiswa historis (nilai A, B, C, D, E per mata kuliah).
- **Format Dataset**: `[NIM, Kode_MK, Nama_MK, SKS, Nilai_Huruf, Semester_Diambil, Status_Lulus_Tepat_Waktu]`.

### Fase 2: Eksplorasi Metodologi
Dua pendekatan yang bisa digunakan:
1. **Association Rule Mining (Apriori/FP-Growth)**: 
   Mencari aturan korelasi seperti "Jika mahasiswa mendapat C di Struktur Data dan D di Basis Data, kemungkinan terlambat lulus 80%".
2. **Feature Importance Classification**: 
   One-hot encoding setiap mata kuliah (misal fitur `Nilai_Kalkulus`, `Nilai_Alpro`). Lalu latih model (Random Forest / XGBoost) dan ambil fitur dengan SHAP Value / Importance tertinggi yang berkontribusi pada label "Terlambat".

### Fase 3: Integrasi dengan Sistem
- API ML akan menerima array nilai per mata kuliah.
- Output API akan menyertakan array `top_risk_courses` (mata kuliah yang paling menurunkan skor prediksi).
- Frontend akan menampilkannya di Dashboard Kaprodi sebagai rekomendasi penanganan (misalnya: "Mahasiswa X butuh bimbingan khusus di matkul Kalkulus").
