# 5220411370 | NINA KHARISMA

# Analisis Sentimen Twitter tentang Fish It Game Roblox dengan InSet Lexicon

## Deskripsi Proyek

Proyek ini bertujuan untuk melakukan analisis sentimen terhadap cuitan (tweet) dari Twitter yang berkaitan dengan **Fish It** salah satu map dari **Roblox**. Proses analisis menggunakan pendekatan **lexicon-based sentiment analysis** dengan memanfaatkan **InSet Lexicon** (Indonesian Sentiment Lexicon).

## Tahapan Proses

### 1. Pengumpulan Data

* Dataset dikumpulkan dari Twitter dengan kata kunci yang berkaitan dengan **Fish It**.
* Data berupa teks mentah (tweet) beserta metadata standar (id, waktu, dsb.).
* Data tersimpan sebagai **data.csv**

### 2. Pembersihan Data (Case Folding)

* Menghapus URL, hashtag, mention, angka, dan karakter khusus.
* Normalisasi teks (lowercase).
* Tokenisasi kata.
* Data tersimpan sebagai **data_casefolding**

### 3. Persiapan Lexicon

* Menggunakan **InSet Lexicon** dari repositori [fajri91/InSet](https://github.com/fajri91/InSet).
* Lexicon tersedia dalam format `positive.tsv` dan `negative.tsv`.
* File tersebut dikonversi ke format **JSON** (`inset_lexicon.json`) agar lebih mudah digunakan pada pipeline analisis.

  * Struktur JSON:

    ```json
    {
      "positive": {
        "bagus": 1.0,
        "luar_biasa": 1.0
      },
      "negative": {
        "buruk": -1.0,
        "gagal": -1.0
      }
    }
    ```

### 4. Skoring Sentimen

* Setiap token dalam tweet dibandingkan dengan kata pada lexicon.
* Jika token ada pada lexicon positif, nilainya ditambah dengan skor positif.
* Jika token ada pada lexicon negatif, nilainya ditambah dengan skor negatif.
* Nilai total menentukan label sentimen:

  * **Positive** jika skor > 0
  * **Negative** jika skor < 0
  * **Neutral** jika skor = 0

### 5. Pelabelan Sentimen

* Fungsi Python dibuat untuk membaca setiap teks, menghitung skor, dan mengembalikan label sentimen.
* Hasil label ditambahkan sebagai kolom baru pada dataset (`sentiment`).

### 6. Analisis Distribusi

* Distribusi jumlah tweet per kategori sentimen (positif, negatif, netral) dihitung.
* Distribusi ini divisualisasikan dalam bentuk grafik batang atau pie chart.

### 7. Evaluasi dan Perbaikan (Opsional)

* Untuk mengatasi masalah **class imbalance**, dapat dilakukan:

  * Penyesuaian threshold.
  * Penggunaan hybrid approach (lexicon + machine learning).

## Hasil

* Dataset Twitter bertema **Talon** berhasil diproses dengan pelabelan sentimen otomatis.
* Distribusi sentimen memberikan gambaran umum mengenai persepsi publik di Twitter terhadap topik tersebut.

## Referensi

* Fajri Koto. *InSet Lexicon: Indonesian Sentiment Lexicon.* [https://github.com/fajri91/InSet](https://github.com/fajri91/InSet)

---




