# 📊 PANDUAN LENGKAP: ANALISIS INFERENSIAL KEBIASAAN BELAJAR MAHASISWA

**Dokumen:** Analisis Statistik Inferensial  
**Dataset:** Rekap_Data_Wawancara.xlsx (n=31 responden)  
**Tools:** Python 3 dengan scipy, statsmodels, pandas  
**Tanggal:** Juni 2026

---

## 📋 DAFTAR ISI

1. [Overview Analisis Inferensial](#overview)
2. [Metodologi Statistik](#metodologi)
3. [Komponen Analisis](#komponen)
4. [Interpretasi Hasil](#interpretasi)
5. [Rekomendasi](#rekomendasi)

---

## <a name="overview"></a>1. OVERVIEW ANALISIS INFERENSIAL

### Apa itu Analisis Inferensial?

**Analisis Inferensial** adalah teknik statistik untuk membuat kesimpulan tentang **populasi** berdasarkan **sampel** data yang dikumpulkan. 

Berbeda dengan deskriptif yang hanya menggambarkan data, inferensial memungkinkan kita untuk:
- ✓ Menguji hipotesis (hypothesis testing)
- ✓ Membuat estimasi parameter populasi (confidence intervals)
- ✓ Mengidentifikasi hubungan signifikan antar variabel
- ✓ Melakukan prediksi

### Tujuan Analisis Inferensial pada Penelitian Ini

1. **Menjawab pertanyaan penelitian** dengan tingkat keyakinan statistik
2. **Generalisasi hasil** dari sampel 31 mahasiswa ke populasi lebih luas
3. **Menguji asumsi** tentang kebiasaan belajar mahasiswa
4. **Membangun model prediktif** untuk kepuasan belajar

---

## <a name="metodologi"></a>2. METODOLOGI STATISTIK

### 2.1 Level Signifikansi (α)

```
α = 0.05 (5%)  → Standar dalam ilmu sosial
Interpretasi: Kami rela berbuat salah 5% dari waktu (Type I Error)
```

### 2.2 Tingkat Kepercayaan (Confidence Level)

```
95% CI (Confidence Interval)
→ Jika kami mengambil 100 sampel, 95 di antaranya akan mencakup parameter sebenarnya
```

### 2.3 Jenis Kesalahan

| Jenis | Definisi | Simbol | Dampak |
|-------|----------|--------|--------|
| **Type I Error** | Menolak H₀ padahal benar | α | Positive False |
| **Type II Error** | Gagal menolak H₀ padahal salah | β | Negative False |
| **Power** | Probabilitas mendeteksi efek nyata | 1-β | ~0.80 ideal |

---

## <a name="komponen"></a>3. KOMPONEN ANALISIS INFERENSIAL

### BAGIAN 1: CONFIDENCE INTERVALS & PARAMETER ESTIMATION

#### 1.1 Apa itu Confidence Interval?

**Definisi:** Range nilai yang kemungkinan besar mengandung parameter populasi sebenarnya.

**Formula untuk Mean:**
```
CI = X̄ ± (t* × SE)

Dimana:
  X̄    = Sample mean
  t*   = Critical t-value (tergantung α dan df)
  SE   = Standard Error = s / √n
```

#### 1.2 Interpretasi CI untuk Jam Belajar

Jika output menunjukkan: **CI = [1.45, 2.35] jam/hari**

**BENAR:** "Kami 95% yakin bahwa rata-rata jam belajar populasi terletak antara 1.45-2.35 jam/hari"

**SALAH:** "Ada 95% probabilitas rata-rata individual terletak dalam interval ini"

---

### BAGIAN 2: HYPOTHESIS TESTING — ONE-SAMPLE TESTS

#### 2.1 One-Sample t-Test

**Tujuan:** Menguji apakah rata-rata sampel berbeda signifikan dari nilai ekspektasi.

**Hipotesis:**
```
H₀: μ = μ₀  (rata-rata sama dengan nilai ekspektasi)
H₁: μ ≠ μ₀  (rata-rata berbeda dari nilai ekspektasi)
```

**Formula:**
```
t = (X̄ - μ₀) / (s / √n)

Dimana:
  X̄    = Sample mean
  μ₀   = Hypothesized mean
  s    = Sample standard deviation
  n    = Sample size
```

**Keputusan:**
- Jika **p < 0.05** → Tolak H₀ (signifikan)
- Jika **p ≥ 0.05** → Gagal tolak H₀ (tidak signifikan)

**Contoh Kasus:**
```
H₀: Rata-rata jam belajar = 2.5 jam/hari
H₁: Rata-rata jam belajar ≠ 2.5 jam/hari

Hasil: t = -1.234, p = 0.226
Kesimpulan: p > 0.05 → Tidak signifikan
Interpretasi: Jam belajar mahasiswa TIDAK berbeda signifikan dari 2.5 jam/hari
```

---

### BAGIAN 3: HYPOTHESIS TESTING — TWO-SAMPLE TESTS

#### 3.1 Independent t-Test

**Tujuan:** Membandingkan rata-rata dua grup independen.

**Hipotesis:**
```
H₀: μ₁ = μ₂  (kedua grup punya rata-rata sama)
H₁: μ₁ ≠ μ₂  (kedua grup punya rata-rata berbeda)
```

**Asumsi:**
1. ✓ Data normal (Shapiro-Wilk test)
2. ✓ Varians sama (Levene test)
3. ✓ Sampel independen

**Formula:**
```
t = (X̄₁ - X̄₂) / √(sp² × (1/n₁ + 1/n₂))

Dimana:
  sp² = Pooled variance
```

**Effect Size (Cohen's d):**
```
d = (X̄₁ - X̄₂) / sp

Interpretasi:
  |d| < 0.2  = Negligible
  |d| < 0.5  = Small
  |d| < 0.8  = Medium
  |d| ≥ 0.8  = Large
```

**Contoh: Jam Belajar by Jenis Kelamin**
```
Laki-laki:  Mean = 2.1 jam, SD = 1.2
Perempuan:  Mean = 2.3 jam, SD = 1.0

t = -0.654, p = 0.517, df = 29
Cohen's d = -0.18

Kesimpulan: TIDAK signifikan (p > 0.05), effect size negligible
Interpretasi: Tidak ada perbedaan jam belajar antara laki-laki dan perempuan
```

---

### BAGIAN 4: ANOVA — PERBEDAAN MULTIGRUP

#### 4.1 One-Way ANOVA (Analysis of Variance)

**Tujuan:** Membandingkan rata-rata ≥3 grup.

**Hipotesis:**
```
H₀: μ₁ = μ₂ = μ₃ = ... = μₖ  (semua grup sama)
H₁: Setidaknya ada satu μᵢ yang berbeda
```

**Logika:**
```
Apakah variasi ANTAR grup > variasi DALAM grup?

F-ratio = MS_between / MS_within

Semakin besar F → Semakin signifikan perbedaan antar grup
```

**ANOVA Table:**
```
Source        SS           df      MS          F           p
Between    SS_between    k-1    MS_b        F = MS_b/MS_w
Within     SS_within     N-k    MS_w
Total      SS_total      N-1

Dimana:
  k = jumlah grup
  N = total sample size
```

**Effect Size (Eta-squared):**
```
η² = SS_between / SS_total

Interpretasi:
  η² < 0.01  = Small
  η² < 0.06  = Medium
  η² ≥ 0.06  = Large
```

**Post-Hoc Test: Tukey HSD**

Jika ANOVA signifikan, lanjutkan dengan Tukey HSD untuk menemukan **pasangan grup mana yang berbeda**.

```
Tukey HSD = q* × √(MS_w / n)

Jika perbedaan mean > HSD → Pasangan signifikan
```

---

### BAGIAN 5: LINEAR REGRESSION

#### 5.1 Simple Linear Regression

**Tujuan:** Memprediksi variabel dependen (Y) dari variabel independen (X).

**Persamaan:**
```
Ŷ = β₀ + β₁X + ε

Dimana:
  β₀ = Intercept (nilai Y ketika X=0)
  β₁ = Slope (perubahan Y per unit X)
  ε  = Error term (residual)
```

**Interpretasi Koefisien:**
```
β₁ = 0.35 berarti:
→ Setiap kenaikan X sebesar 1 unit, Y meningkat 0.35 unit
(holding other variables constant)
```

**Model Fit Statistics:**

| Statistik | Rumus | Interpretasi |
|-----------|-------|--------------|
| **R²** | SS_reg / SS_total | % variasi Y dijelaskan X |
| **Adj. R²** | 1 - (1-R²)(n-1)/(n-p-1) | R² yang disesuaikan dengan jumlah prediktor |
| **F-statistic** | MS_regression / MS_residual | Overall model significance |
| **RMSE** | √(SS_residual / n) | Rata-rata error prediksi |

#### 5.2 Multiple Linear Regression

**Persamaan:**
```
Ŷ = β₀ + β₁X₁ + β₂X₂ + ... + βₖXₖ + ε
```

**Asumsi Regresi (GAUSS):**
```
1. Linearity    → Hubungan linear X dan Y
2. Autonomy     → Observations independen
3. Uniformity   → Homoscedasticity (varians konstan)
4. Specification→ Tidak ada overfitting
5. Sample       → Ukuran sample adequate
```

**Diagnostik Residual:**
1. **Residuals vs Fitted** → Homoscedasticity check
2. **Q-Q Plot** → Normality check
3. **Histogram** → Distribution check
4. **Scale-Location** → Variance stability check

---

### BAGIAN 6: CORRELATION SIGNIFICANCE TESTS

#### 6.1 Pearson Correlation (r)

**Rumus:**
```
r = Σ((xᵢ - x̄)(yᵢ - ȳ)) / √(Σ(xᵢ-x̄)² × Σ(yᵢ-ȳ)²)

Range: -1 ≤ r ≤ +1
```

**Interpretasi Kekuatan:**
```
|r| < 0.1   = Negligible
0.1 ≤ |r| < 0.3 = Weak
0.3 ≤ |r| < 0.5 = Moderate
0.5 ≤ |r| < 0.7 = Strong
|r| ≥ 0.7   = Very Strong
```

**Signifikansi Test:**
```
t = r × √(n-2) / √(1-r²)

Jika p-value < 0.05 → Korelasi signifikan
```

**Coefficient of Determination (R²):**
```
R² = r²
→ Persentase varian bersama antara X dan Y

Contoh: r = 0.60 → R² = 0.36 → 36% shared variance
```

---

### BAGIAN 7: CHI-SQUARE TEST (Kategorik)

#### 7.1 Chi-Square Test of Independence

**Tujuan:** Menguji independensi dua variabel kategorikal.

**Hipotesis:**
```
H₀: Variabel 1 dan Variabel 2 independen
H₁: Variabel 1 dan Variabel 2 tidak independen (ada asosiasi)
```

**Formula:**
```
χ² = Σ((O - E)² / E)

Dimana:
  O = Observed frequency
  E = Expected frequency (under independence)
```

**Expected Frequency:**
```
E(i,j) = (Row Total × Column Total) / Grand Total
```

**Effect Size (Cramér's V):**
```
V = √(χ² / (n × min(k-1, r-1)))

Dimana:
  n = total sample size
  k = jumlah kolom
  r = jumlah baris

Interpretasi (untuk df=1):
  V < 0.10 = Small
  V < 0.30 = Medium
  V ≥ 0.30 = Large
```

---

## <a name="interpretasi"></a>4. INTERPRETASI HASIL

### Template Interpretasi Standar

#### ONE-SAMPLE t-TEST
```
"One-sample t-test menunjukkan bahwa rata-rata [VARIABEL] (M = X.XX, SD = X.XX) 
secara signifikan BERBEDA/TIDAK BERBEDA dari nilai ekspektasi X [t(df) = X.XX, 
p = X.XXX]. Dengan confidence interval 95%, parameter populasi berkisar 
[X.XX, X.XX]."
```

#### INDEPENDENT t-TEST
```
"Rata-rata [VARIABEL] untuk grup [A] (M = X.XX, SD = X.XX) secara signifikan 
LEBIH TINGGI/RENDAH daripada grup [B] (M = X.XX, SD = X.XX), t(df) = X.XX, 
p = X.XXX, d = X.XX (effect size: SMALL/MEDIUM/LARGE)."
```

#### ONE-WAY ANOVA
```
"One-way ANOVA menunjukkan perbedaan signifikan dalam [VARIABEL] antar 
kelompok [KATEGORI], F(k-1, N-k) = X.XX, p = X.XXX, η² = X.XX. 
Post-hoc Tukey test mengindikasikan perbedaan signifikan antara 
grup [A] vs [B] (p < 0.05)."
```

#### SIMPLE LINEAR REGRESSION
```
"Hasil regresi linear menunjukkan bahwa [X-VARIABLE] secara signifikan 
memprediksi [Y-VARIABLE], b = X.XX, t(df) = X.XX, p = X.XXX. 
Setiap kenaikan X sebesar 1 unit memprediksi peningkatan Y sebesar X.XX unit. 
Model menjelaskan X.X% varians dalam [Y-VARIABLE] (R² = X.XXX)."
```

#### PEARSON CORRELATION
```
"Ada korelasi [positif/negatif] yang [signifikan/tidak signifikan] dan 
[STRENGTH] antara [X] dan [Y], r = X.XXX, p = X.XXX, R² = X.XXX. 
Ini berarti X.X% shared variance antara kedua variabel."
```

---

## <a name="rekomendasi"></a>5. REKOMENDASI ANALISIS LANJUTAN

### 5.1 untuk Laporan Skripsi/Tugas

✓ **WAJIB INCLUDE:**
- Confidence intervals untuk semua parameter utama
- Normality tests (Shapiro-Wilk) sebelum parametric tests
- Hypothesis testing dengan effect sizes
- Regression model dengan diagnostik residual
- Correlation matrix dengan signifikansi

✓ **OPTIONAL (untuk nilai tambah):**
- Post-hoc power analysis
- Model comparison (AIC/BIC)
- Mediation analysis
- Moderator analysis
- Structural equation modeling

### 5.2 Analisis Tambahan yang Bisa Dilakukan

#### A. Time Series / Longitudinal
```python
# Jika data dikumpulkan berkali-kali
from scipy import signal
trend = signal.savgol_filter(data, window_length=5, polyorder=2)
```

#### B. Clustering Analysis
```python
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=3)
clusters = kmeans.fit_predict(data)
```

#### C. Predictive Modeling
```python
from sklearn.ensemble import RandomForestRegressor
model = RandomForestRegressor(n_estimators=100)
model.fit(X_train, y_train)
```

#### D. Bayesian Analysis
```python
from pymc3 import Model, Normal, find_MAP
# Lebih robust untuk small samples
```

---

## 📝 CHECKLIST UNTUK LAPORAN

- [ ] Semua confidence intervals dihitung dan dilaporkan
- [ ] Normalitas data diuji (Shapiro-Wilk)
- [ ] Asumsi parametric tests diverifikasi
- [ ] Hypothesis testing dengan p-values dilakukan
- [ ] Effect sizes dilaporkan (Cohen's d, η², r)
- [ ] Interpretasi hasil dalam konteks penelitian
- [ ] Limitation dan threats to validity didiskusikan
- [ ] Regression assumptions dicheck (residual plots)
- [ ] Confidence intervals untuk regression coefficients ada
- [ ] Conclusion ditulis dengan tepat dan hati-hati

---

## 🔗 REFERENSI

1. **Field, A.** (2013). *Discovering Statistics Using IBM SPSS Statistics* (4th ed.)
2. **Cohen, J., Cohen, P., West, S. G., & Aiken, L. S.** (2013). *Applied Multiple Regression/Correlation Analysis*
3. **Kline, R. B.** (2015). *Principles and Practice of Structural Equation Modeling* (3rd ed.)
4. **Statology** - Comprehensive Statistics Guide
5. **UCLA IDRE Statistics** - Statistical Methods & Interpretation

---

**Document Version:** 1.0  
**Last Updated:** Juni 2026  
**Prepared by:** Data Analyst (Professional)
