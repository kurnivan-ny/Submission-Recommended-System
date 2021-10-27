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
Setelah melakukan Persiapan Data _(Data Preparation)_, maka tahap selanjutnya modeling. Modeling untuk sistem rekomendasi _Content Based Filtering_ menggunakan CountVectorizer dan TF-IDF Vectorizer.

- CountVectorizer

  Count Vectorizer adalah cara untuk mengubah serangkaian string tertentu menjadi representasi frekuensi. Count Vectorizer dapat membantu dalam memahami jenis teks dengan frekuensi kata-kata di dalamnya. Namun mempunyai kelemahan sebagai berikut:
  - Ketidakmampuan dalam mengidentifikasi kata-kata yang lebih penting dan kurang penting untuk dianalisis.
  - Hanya mempertimbangkan kata-kata yang berlimpah di corpus sebagai kata yang paling signifikan secara statistik.
  - Tidak mengindentifikasi hubungan antar kata seperti kesamaan linguistik antar kata.
  Pada tahap ini, saya menggunakan modul dari scikit-learn yaitu [Count Vectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html).

- TF-IDF Vectorizer

  TF-IDF Vectorizer (Term Frequency -  Inverse Document Frequency) adalah statistik yang didasarkan pada frekuensi kata dalam korpus tetapi juga memberikan representasi numerik tentang betapa pentingnya sebuah kata untuk analisis statistik.
  TF-IDF lebih baik daripada Count Vectorizers karena tidak hanya berfokus pada frekuensi kata yang ada dalam korpus tetapi juga memberikan pentingnya kata tersebut. Kami kemudian dapat menghapus kata-kata yang kurang penting untuk analisis, sehingga membuat model bangunan kurang kompleks dengan mengurangi dimensi input.
  TF-IDF didasarkan pada logika bahwa kata-kata yang terlalu banyak dalam korpus dan kata-kata yang terlalu jarang keduanya tidak penting secara statistik untuk menemukan suatu pola. Faktor logaritma dalam TF-IDF secara matematis menghukum kata-kata yang terlalu banyak atau terlalu jarang dalam korpus dengan memberikan nilai TF-IDF yang rendah.
  Pada tahap ini, saya menggunakan modul dari scikit-learn yaitu [TF-IDF Vectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html).
  
Dari kedua Vectorizer tersebut kemudian akan dibuat sistem rekomendasi _content based filtering_ dengan menggunakan [_consine similiarity_](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.cosine_similarity.html). CountVectorizer dan TF-IDF Vectorizer dengan fungsi stop_words=’english’ berfungsi untuk menghilangkan kata semacam: i, you, the, a, this, is dan sejenisnya. Tujuannya sebelum menghitung cosine similarity, terlebih dahulu data diubah kedalam bentuk vektor.

- Hasil Prediksi
  
  Hasil rekomendasi yang diberikan, dibuat sebuah fungsi recomendation untuk memberikan rekomendasi terhadap suatu judul movie atau tv show yang diinputkan (pengalaman pengguna). Kemudian mengambil beberapa data yang memiliki kemiripan (similarity) dan selanjutnya dari bobot berupa tingkat kesamaan diurutkan dari terbesar ke terkecil dan dimasukkan ke variabel sim_scores. Kemudian ditampilkan rekomendasi berupa DataFrame yang berisikan Judul Movie atau TV Show dan _consine similiarity_. Input Movie atau TV Show adalah Story of Kale: When Someone's in Love.
  - Hasil Prediksi dari CountVectorizer
    
    ![countvectorizer](https://user-images.githubusercontent.com/72246401/139031507-4ebdb90e-d1de-4e2a-b984-330d3e411414.jpg)
    
  - Hasil Prediksi dari TF-IDF Vectorizer
  
    ![TF-IDF Vectorizer](https://user-images.githubusercontent.com/72246401/139031580-21dc596e-7f03-40fd-bcd6-ea7d3d58e745.jpg)
    

## Evaluation
Pada proyek ini, kami menggunakan evaluasi pada model sistem rekomendasi _Content Based Filtering_ dengan metric _Recommender System Precision_.

Precision adalah rasio prediksi benar positif (True Positif) terhadap keseluruhan hasil yang diprediksi positif. Untuk formula _Recommender System Precision_ dapat ditulis sebagai berikut[[2]](https://towardsdatascience.com/recommendation-systems-models-and-evaluation-84944a84fb8e).

![precision sr](https://user-images.githubusercontent.com/72246401/139031631-4a7fc2c8-7f71-4215-a8ab-c8a563345030.png)

Untuk penerapan pada kode dengan membuat fungsi precision yang terdapat 2 paramter yaitu banyak rekomendasi dan jumlah rekomendasi yang sesuai. Kemudian menggunakan _consine similiarity_ > 0.05.

- Precision dari CountVectorizer

  ![precision countvectorizer](https://user-images.githubusercontent.com/72246401/139031630-c3ece154-93d6-4eda-8d01-200e89e93e0f.jpg)
  
- Precision dari TF-IDF Vectorizer

  ![precision TF-IDF Vectorizer](https://user-images.githubusercontent.com/72246401/139031574-3fb050e2-7dbb-4e76-93f4-46f4f341075e.jpg)

Dari precision yang dilihat bahwa precision pada CountVectorizer lebih baik daripada TF-IDF Vectorizer. Precision pada CountVectorizer 1.0 artinya 100% sedangkan precision pada TF-IDF Vectorizer 0.6 atau 60%.

# Referensi:
[1] https://help.netflix.com/id/node/412
[2] https://towardsdatascience.com/recommendation-systems-models-and-evaluation-84944a84fb8e
