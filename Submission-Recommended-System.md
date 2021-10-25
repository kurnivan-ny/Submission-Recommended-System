# Laporan Proyek Machine Learning Terapan - Kurnivan Noer Yusvianto

- Project Overview

<p align="center">
  <img src="https://user-images.githubusercontent.com/72246401/137863762-394d381d-7312-4ece-806a-cdf8565baddf.png">
</p>

Pada proyek sistem rekomendasi, kita akan membuat sistem rekomendasi movie atau tv show di Netflix. 
Netflix adalah layanan streaming berbasis langganan yang memungkinkan anggota kami menonton acara TV dan film tanpa iklan di perangkat yang terhubung ke Internet[[1](https://help.netflix.com/id/node/412)]. Setiap hari Netflix dibanjiri oleh pengguna yang gemar movie atau tv show untuk menonton secara _streaming_ movie atau tv show yang disukai. Namun terlalu banyaknya movie atau tv show yang mengakibatkan kebingungan yang dihadapi oleh pengguna. Oleh karena itu, diperlukan sistem rekomendasi yang digunakan untuk memberikan rekomendasi movie atau tv show berdasarkan pengalaman pengguna sebelumnya.

## Business Understanding

### Problem Statements
Berdasarkan latar belakang diatas, ada beberapa rincian masalah yang dapat diselesaikan pada proyek ini sebagai berikut.
- Sistem rekomendasi apa yang diterapkan pada proyek kali ini?
- Bagaimana cara membuat sistem rekomendasi movie atau tv show untuk pengguna di Netflix?

### Goals
Tujuan dari dibuatnya proyek ini sebagai berikut.
- Membuat sistem rekomendasi movie atau tv show untuk pengguna di Netflix.
- Memberikan rekomendasi movie atau tv show yang kemungkinan disukai pengguna berdasarkan pengalaman pengguna sebelumnya.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini sebagai berikut.

![Untitled Diagram drawio (4)](https://user-images.githubusercontent.com/72246401/138665219-72ec8c91-055c-4926-8db7-aff3bd8196b7.png)

Solusi yang dapat dilakukan untuk memenuhi proyek ini sebagai berikut.

- Untuk bagian _Data Preparation_ dilakukan beberapa teknik sebagai berikut.
  - Features List berupa memilih fitur yang akan digunakan.
  - _Data Cleaning_ berupa mengisi data kosong pada kolom, membuang tanda baca, menyamakan ukuran huruf, dan ekstraksi kata kunci dengan RAKE (Rapid Automatic Keyword Extraction).
- Untuk bagian Model Sistem Rekomendasi menggunakan _content based filtering_ karena dataset tidak terdapat rating. Oleh karena itu, sistem rekomendasi dibuat untuk memberikan rekomendasi pada pengguna berdasarkan pengalaman pengguna sebelumnya.
- Untuk bagian Evaluasi Sistem Rekomendasi menggunakan _consine similiarity_. _Cosine similarity_ mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. _Cosine similarity_ dirumuskan sebagai berikut.

   ![consine similiarity](https://user-images.githubusercontent.com/72246401/138666015-487a70e2-d9c4-4159-a8ef-23fca8445c46.png)

## Data Understanding
![image](https://user-images.githubusercontent.com/72246401/137866422-f7eba1f6-e2b7-4f37-b2f2-d2c0df43cb97.png)
Informasi dataset sebagai berikut.

| Jenis | Keterangan |
| :--- | :--- |
| Sumber | Kaggle Dataset : [Netflix Movies and TV Shows](https://www.kaggle.com/shivamb/netflix-shows)|
| Lisensi | CC0: Public Domain |
| Kategori | movies and tv shows |
| Rating Penggunaan | 10.0 (Gold) |
| Jenis dan Ukuran Berkas | CSV (3.4 MB) |

Pada berkas yang diunduh yakni netflix_titles.csv terdapat 8.807 baris (records atau jumlah pengamatan) dan 12 kolom dalam dataset. Berdasarkan informasi dari dataset, variabel pada Netflix Movies and TV Shows sebagai berikut.

| Variabel | Deskripsi |
| :--- | :--- |
| show_id | id unik dari setiap pertunjukan |
| type | Kategori acara, bisa berupa Film atau Acara TV |
| title | Judul Film / Acara TV |
| director | Nama sutradara |
| cast | Nama aktor yang terlibat dalam film / pertunjukan |
| country | Negara tempat film / acara itu diproduksi |
| date_added | Tanggal saat acara ditambahkan di Netflix |
| release_year | Tahun rilis pertunjukan |
| rating | Tampilkan peringkat di Netflix |
| duration | Durasi waktu pertunjukan dalam menit |
| listed_in | Genre acaranya |
| description | Deskripsi ringkasan |

Untuk mengetahui deskripsi variabel seperti tipe data, sample unik, dan jumlah sample unik sebagai berikut.

![Screenshot (2005)](https://user-images.githubusercontent.com/72246401/138668317-36adc883-8fa0-4281-92c4-ec4b2d767289.png)

Visualisasi data numerik dari dataset yang digunakan sebagai berikut.

![newplot](https://user-images.githubusercontent.com/72246401/138670626-e9670235-18c6-4f69-9b01-543027b51953.png)

![newplot (1)](https://user-images.githubusercontent.com/72246401/138670624-f66477c9-c0a6-4685-97d3-0023ad516191.png)

![newplot (2)](https://user-images.githubusercontent.com/72246401/138670622-b6deee58-c30d-4a54-a1c8-2bd2801143d9.png)

![newplot (3)](https://user-images.githubusercontent.com/72246401/138670617-ab70c4ae-6dde-4b6d-8ed5-d390e11acd3c.png)

![newplot (4)](https://user-images.githubusercontent.com/72246401/138670633-e680c38e-2f36-423f-b775-da8d578ef273.png)

![newplot (5)](https://user-images.githubusercontent.com/72246401/138670630-b6cb27bf-0f00-45da-9075-56ce817a670b.png)

![newplot (6)](https://user-images.githubusercontent.com/72246401/138670628-8a1eff23-2528-4233-b7f6-880ab5b40b5a.png)

_Word Cloud_ merupakan salah satu metode untuk menampilkan data teks secara visual. Grafik ini populer dalam text mining karena mudah dipahami. Dengan menggunakan _word cloud_, gambaran frekuensi kata-kata dapat ditampilkan dalam bentuk yang menarik namun tetap informatif. Semakin sering satu kata digunakan, maka semakin besar pula ukuran kata tersebut ditampilkan dalam _word cloud_. _Word cloud_ dari dataset sebagai berikut.

- Variabel Title
![download (5)](https://user-images.githubusercontent.com/72246401/138671223-654f282b-82bb-4cde-b0ed-ecf4426b349b.png)

- Variabel Director
![download (6)](https://user-images.githubusercontent.com/72246401/138671218-545e42df-ba7f-48d9-bad8-003153880a41.png)

- Variabel Cast
![download (7)](https://user-images.githubusercontent.com/72246401/138671211-49059f19-34a0-4c93-b594-f46519efd7ae.png)

- Variabel Description
![download (8)](https://user-images.githubusercontent.com/72246401/138671230-45a3a30b-ce56-4ccb-9c36-f0e0cbe7ad9c.png)


## Data Preparation
Persiapan Data _(Data Preparation)_ adalah proses mengubah atau mentransformasi fitur-fitur data ke dalam bentuk yang mudah diinterpretasikan dan diproses oleh model machine learning.

Seperti yang sudah dijelaskan pada bagian _Solution Statements_, berikut adalah tahapan dalam melakukan _data preparation_.

- Features List berupa memilih fitur yang akan digunakan.

   Kami akan membuat daftar fitur yang akan kami gunakan. Kami hanya akan menggunakan fitur yang paling relevan bagi kami, mengingat masalah yang kami hadapi. Oleh karena itu, fitur yang kami pilih adalah title, type, director, cast, country, listed_in, description, dan rating.
- _Data Cleaning_

  Kami mengubah tipe data menjadi string dan melakukan sedikit preprocessing data dan mengganti setiap baris yang memiliki nilai NaN dengan spasi/string kosong, sehingga tidak menghasilkan kesalahan saat menjalankan kode.
  Kami menggunakan RAKE-NLTK. RAKE (Rapid Automatic Keyword Extraction) adalah algoritma ekstraksi kata kunci independen domain yang mencoba menentukan frasa kunci dalam tubuh teks dengan menganalisis frekuensi kemunculan kata dan kemunculannya bersama dengan kata lain dalam teks.
  Kemudian digabungkan fitur berupa type, director, cast, country, listed_in, description, dan rating menjadi satu yaitu key_notes dan title tetap menjadi fitur sendiri. Setelah itu, kami mengubah tipe data menjadi string dan membuang tanda baca seperti , & - . Dan menjadikan semua string menjadi huruf kecil dengan lower.


## Modeling
Setelah melakukan Persiapan Data _(Data Preparation)_, maka tahap selanjutnya modeling. Modeling menggunakan 2 model yaitu pembuatan model _baseline_ dan pembuatan model yang dikembangkan.

- Model _baseline_

  Pada tahap ini, saya membuat model dasar dengan menggunakan modul dari scikit-learn yaitu [SVC](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html) dengan parameter _default_. Kemudian dilakukan prediksi pada data test.

- Model yang dikembangkan

  Setelah melihat kinerja dari model _baseline_, untuk model dapat bekerja lebih optimal maka diperlukan _Hyper Parameter Tuning_. _Hyper Parameter Tuning_ digunakan untuk mencari parameter terbaik yang akan diterapkan pada model _baseline_. _Hyper Parameter Tuning_ menggunkan  [_Grid Search Cross Validation (CV)_](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html). _Grid Search Cross Validation (CV)_ adalah metode pemilihan kombinasi model dan hyperparameter dengan cara menguji coba satu persatu kombinasi dan melakukan validasi untuk setiap kombinasi. Tujuannya adalah menentukan kombinasi yang menghasilkan performa model terbaik yang dapat dipilih untuk dijadikan model untuk prediksi. Pada model SVC, parameter yang di _Grid Search CV_ adalah c, gamma, dan kernel. C merupakan parameter regularisasi, gamma merupakan koefisien kernel, dan kernel menggunakan rbf.
  
## Evaluation
Pada proyek ini, kami menggunakan _confusion matriks_ dan _classification report_ untuk mengevalusasi model.
- _Confusion Matriks_
  
  _Confusion matriks_ merupakan tabel untuk memvisualisasikan performa model prediksi. Setiap entri dalam _confusion matriks_ menunjukkan jumlah prediksi yang dibuat oleh model yang mengklasifikasikan kelas dengan benar atau salah.
  
  ![cf multiclass](https://user-images.githubusercontent.com/72246401/137152262-bec4eb6b-d394-4536-a0a1-0562479e0980.png)
  
  Keterangan:
    - True Positif: Ini mengacu pada jumlah prediksi di mana pengklasifikasi dengan benar memprediksi kelas positif sebagai positif.
    - False Positive: Ini mengacu pada jumlah prediksi di mana pengklasifikasi salah memprediksi kelas negatif sebagai positif.
    - False Negative: Ini mengacu pada jumlah prediksi di mana pengklasifikasi salah memprediksi kelas positif sebagai negatif.
    - True Negative: Ini mengacu pada jumlah prediksi di mana pengklasifikasi dengan benar memprediksi kelas negatif sebagai negatif.
  
  Berikut dibawah ini merupakan formula untuk mengukur parameter yang digunakan dalam menilai kinerja model.
  |  | Formula | Penjelasan |
  | :---: | :---: | :---: |
  | Accuracy | ![accuracy](https://user-images.githubusercontent.com/72246401/137153643-c8ef8b9e-8e90-4044-9393-e4b01dc5a24f.png) | Nilai ketepatan model dalam memprediksi data dengan data yang sebenarnya |
  | Precission | ![precision](https://user-images.githubusercontent.com/72246401/137153668-55d6752a-056e-491d-a108-efb468bf7b8a.png) | Menghitung seberapa baik model memprediksi label positif terhadap semua prediksi model berlabel positif |
  | Recall (Sensivity) | ![recall](https://user-images.githubusercontent.com/72246401/137153665-dfc779d7-cac1-4f23-af93-988e33fda6a5.png) |  Menghitung seberapa baik model memprediksi label positif terhadap semua label data positif |
  | F1 Score | ![F1-Score](https://user-images.githubusercontent.com/72246401/137153660-2a34b4bf-e121-4afa-93bd-ed3dd4f02400.png) | Menghitung seberapa baik hasil prediksi model (precision) dan seberapa lengkap hasil prediksinya (recall) |
  
 
 _Condusion Matriks_ pada model _baseline_ dan model yang dikembangkan dapat dilihat dibawah ini.
 
 - Model _baseline_

  ![cf_base model](https://user-images.githubusercontent.com/72246401/137133825-04434b83-0a32-4b59-b5f7-868ded7e9342.png)

- Model yang dikembangkan

  ![cf_best model](https://user-images.githubusercontent.com/72246401/137133824-3ae3c976-a96e-4a2b-9a0b-db9082ec6060.png)
  
  Dapat dilihat bahwa model _baseline_ memiliki _False Positif_ dan _False Positif_ yang lebih besar dibandingkan dengan model yang dikembangkan.

- _Classification Report_
  
  Classification report digunakan untuk mengukur kualitas prediksi dari algoritma klasifikasi. Classification report menampilkan nilai akurasi, _f1 score_, _recall_, dan _precision_ untuk model.

  Hasil dari model _baseline_ sebagai berikut.
  
  ![cf_model baseline](https://user-images.githubusercontent.com/72246401/137147015-29a593c9-99b4-43e4-9e43-9394135eeaa7.jpg)

  Hasil dari model yang dikembangkan sebagai berikut.
  
  ![cf_model best parameter](https://user-images.githubusercontent.com/72246401/137147006-0f45b597-acb4-44c0-b147-0508dd22f2f7.jpg)
  
Pada model _baseline_ memiliki nilai akurasi yang cukup baik yaitu 86,25% dan nilai _f1 score_, _recall_, serta _precision_ cukup baik. Setelah dilakukan _Hyper Parameter Tuning_ nilai akurasinya meningkat menjadi 95,25% dan nilai _f1 score_, _recall_, serta _precision_ meningkat dari model _baseline_.

Dari _confusion matriks_ dan _classification report_, dapat dilihat bahwa model yang dikembangkan dengan _Hyper Parameter Tuning_ memiliki nilai _false positif_ serta _false negatif_ di _confusion matriks_ dan nilai _f1 score_, _recall_, serta _precision_ di _classification report_ lebih baik dari model _baseline_. Maka dari itu, maka untuk proyek ini menggunakan model yang dikembangkan dengan _Hyper Parameter Tuning_.

# Referensi:
[1] https://techno.okezone.com/read/2014/05/13/57/984293/di-indonesia-smartphone-sudah-menjadi-kebutuhan-utama

[2] https://review.bukalapak.com/gadget/7-hal-yang-harus-diperhatikan-sebelum-membeli-smartphone-bekas-2292

[3] https://www.dqlab.id/perbandingan-support-vector-machine-dan-decision-tree


**---Ini adalah bagian akhir laporan---**
