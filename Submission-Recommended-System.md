# Laporan Proyek Machine Learning Terapan - Kurnivan Noer Yusvianto

- Project Overview

<p align="center">
  <img src="https://user-images.githubusercontent.com/72246401/137866422-f7eba1f6-e2b7-4f37-b2f2-d2c0df43cb97.png">
</p>

Pada proyek sistem rekomendasi, kita akan membuat sistem rekomendasi movie atau tv show di Netflix. 
Netflix adalah layanan streaming berbasis langganan yang memungkinkan anggota kami menonton acara TV dan film tanpa iklan di perangkat yang terhubung ke Internet[[1](https://help.netflix.com/id/node/412)]. Setiap hari Netflix dibanjiri oleh penggemar movie atau tv show untuk menonton movie atau tv show yang disukai. 

## Business Understanding

### Problem Statements
Berdasarkan latar belakang diatas, ada beberapa rincian masalah yang dapat diselesaikan pada proyek ini sebagai berikut.
- Bagaimana cara  melakukan pra-pemrosesan data agar dapat digunakan dengan baik pada model _machine learning_?
- Bagaimana cara membuat model _machine learning_ untuk mengklasifikasikan kisaran harga ponsel?

### Goals
Tujuan dari dibuatnya proyek ini sebagai berikut.
- Melakukan pra-pemrosesan data agar dapat digunakan dengan baik pada model _machine learning_.
- membuat model _machine learning_ untuk mengklasifikasikan kisaran harga ponsel yang memiliki tingkat akurasi > 80%.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini sebagai berikut.
- Untuk pra-pemrosesan dapat dilakukan beberapa teknik sebagai berikut.
    - Melakukan _Categorical Encoding_ yaitu proses mengubah data kategori menjadi data numerik dengan **_One-Hot Encoding_**
    - Melakukan **_Data Splitting_** berupa membagi dataset menjadi 2, yaitu data latih _(train data)_ dengan rasio 80% dan data test _(test data)_ dengan rasio 20%.
    - Melakukan **standardisasi data** pada fitur numerik dengan **StandarScaler**.
  Untuk pra-pemrosesan dilakukan pada tahap Persiapan Data _(Data Preparation)_.
- Untuk pembuatan model menggunakan algoritma **_Support Vector Machine (SVM)_** sebagai model _baseline_. Algoritma tersebut dipilih karena dimensi data tinggi, jumlah data hasil observasi banyak, dan cocok untuk kasus klasifikasi. **_Support Vector Machine (SVM)_** digunakan untuk mencari _hyperplane_ terbaik dengan memaksimalkan jarak antar kelas. _Hyperplane_ adalah sebuah fungsi yang dapat digunakan untuk pemisah antar kelas. Tujuan dari algoritma SVM adalah untuk menemukan _hyperplane_ terbaik dalam ruang berdimensi-N (ruang dengan N-jumlah fitur) yang berfungsi sebagai pemisah yang jelas bagi titik-titik data input. Untuk proyek kami menggunakan SVM Klasifikasi non Linear. Cara kerja **_Support Vector Machine (SVM)_** Klasifikasi non Linear sebagai berikut.
    - Memuat data.
    - Transformasikan data menjadi ruang baru sehingga batas linier dapat digunakan untuk memisahkan tupel.
    - Untuk pemisahan data menggunakan beberapa fungsi kernel berikut.
        - RBF (Radial Basis Function) atau Gaussian kernel
        
            ![gaussian-kernel](https://user-images.githubusercontent.com/72246401/137120936-2bec6b2b-0df2-4a3b-a94b-e95a7c93560b.png)
            
        - Polinomial
        
            ![polynomial-kernel](https://user-images.githubusercontent.com/72246401/137120934-9b86cf3e-ec68-4b4b-affd-52674ab3031d.png)
            
        - Sigmoid
        
            ![sigmoid-kernel](https://user-images.githubusercontent.com/72246401/137120935-4c1b263b-69f7-4709-9708-2283a2b3a833.png)
            
    - Proses pembelajaran:
        - Fase _training_:
            - Minimize:
              
                <img src="https://user-images.githubusercontent.com/72246401/137123514-dc434933-7f57-4f2f-87c4-d696478111ab.png" width="120">
                
            - Target:
            
                <img src="https://user-images.githubusercontent.com/72246401/137123516-74d6939e-37fb-486a-83c5-c284eb1e49f2.png" width="300">
                
        - Fase _testing_:
            
            <img src="https://user-images.githubusercontent.com/72246401/137123510-107b5ee1-a0ef-4a64-a420-457a7c4c504a.png" width="300">
   
   Selain itu, terdapat kelebihan dan kekurangan dari algoritma **_Support Vector Machine (SVM)_** sebagai berikut[[3](https://www.dqlab.id/perbandingan-support-vector-machine-dan-decision-tree)].
   - Kelebihan: Pengklasifikasi SVM menawarkan akurasi tinggi dan bekerja dengan baik dengan ruang dimensi tinggi. SVM pengklasifikasi pada dasarnya menggunakan subset dari poin pelatihan sehingga hasilnya menggunakan memori yang sangat sedikit.
   - Kekurangan: Mereka memiliki waktu pelatihan yang tinggi sehingga dalam praktiknya tidak cocok untuk kumpulan data yang besar. Lain kerugiannya adalah pengklasifikasi SVM tidak berfungsi dengan baik dengan kelas yang tumpang tindih.

## Data Understanding
![Data Understanding](https://user-images.githubusercontent.com/72246401/137133817-6e689b92-276b-4834-a367-c98b925ea28c.png)
Informasi dataset sebagai berikut.

| Jenis                   | Keterangan                                                                              |
| ----------------------- | --------------------------------------------------------------------------------------- |
| Sumber                  | Kaggle Dataset : [Mobile Price Classification](https://www.kaggle.com/iabhishekofficial/mobile-price-classification?select=train.csv)|
| Kategori                | Bisnis dan Klasifikasi                                                                  |
| Rating Penggunaan       | 7.1 (Gold)                                                                              |
| Jenis dan Ukuran Berkas | CSV (122.4 kB)                                                                          |

Pada berkas yang diunduh yakni train.csv terdapat 2.000 baris (records atau jumlah pengamatan) dan 21 kolom dalam dataset. Berdasarkan informasi dari dataset, variabel pada Mobile Price Classification sebagai berikut.

| Variabel | Deskripsi |
| :--- | :--- |
| battery_power | Energi total yang dapat disimpan baterai dalam satu waktu diukur dalam mAh |
| blue | Bluetooth atau tidak |
| clock_speed | Kecepatan di mana mikroprosesor mengeksekusi instruksi |
| dual_sim | Dual SIM atau tidak |
| fc | Resolusi kamera depan (mega piksels) |
| four_g | 4G atau tidak |
| int_memory | Memori internal (Gigabytes) |
| m_dep | Ketebalan ponsel (cm) |
| mobile_wt | Berat ponsel |
| n_cores | Jumlah core dalam processor |
| pc | Resolusi kamera utama (mega pixels) |
| px_height | Tinggi resolusi piksel |
| px_width | Lebar resolusi piksel |
| ram | Random Access Memory (mega byte) |
| sc_h | Tinggi layar ponsel (cm) |
| sc_w | Lebar layar ponsel (cm) |
| talk_time | Waktu terlama satu kali pengisian baterai akan bertahan saat Anda berada |
| three_g | 3G atau tidak |
| touch_screen | Layar sentuh atau tidak |
| wifi | Wifi atau tidak |
| price_range | Variabel target dengan nilai 0 (low cost), 1 (medium cost), 2 (high cost) dan 3 (very high cost) |

Untuk mengetahui deskripsi variabel seperti tipe data, sample unik, dan jumlah sample unik sebagai berikut.

![report](https://user-images.githubusercontent.com/72246401/137133814-115ca3f7-8819-478c-b661-a8c358383879.jpg)

Terdapat 7 data kategori bertipe object dan 14 data numerik bertipe int64 dan float64. Kemudian terdapat visualisasi data kategori sebagai berikut.

![categorical](https://user-images.githubusercontent.com/72246401/137133807-76a4f644-cb01-42c2-ad60-ead14f71ed60.png)

Visualisasi data numerik sebagai berikut.

![numerical](https://user-images.githubusercontent.com/72246401/137133956-b0eeb3bf-fc61-4c0d-a25e-4870f2ced5e1.png)

Visualisasi distribusi data pada kolom dengan fitur numerik dan antar fitur numrerik sebagai berikut.

![korelasi](https://user-images.githubusercontent.com/72246401/137133831-63f3a847-525c-43bd-8da3-10003aabccdc.png)

Visualisasi heatmap dari korelasi antar firut numerik sebagai berikut.

![heatmap](https://user-images.githubusercontent.com/72246401/137133827-598f6483-8ebb-4129-ae06-564485dbb2a2.png)

Keterangan heatmap:
- Semakin mendekati 1 maka semakin tinggi korelasi antar firut numerik
- Semakin mendekati 0 maka korelasi antar firut numerik mendekati netral
- Semakin mendekati -1 maka semakin rendah korelasi antar firut numerik

## Data Preparation
Persiapan Data _(Data Preparation)_ adalah proses mengubah atau mentransformasi fitur-fitur data ke dalam bentuk yang mudah diinterpretasikan dan diproses oleh model machine learning.

Seperti yang sudah dijelaskan pada bagian _Solution Statements_, berikut adalah tahapan dalam melakukan pra_pemrosesan.

- Melakukan _Categorical Encoding_ 

  _Categorical Encoding_ (Encoding fitur kategori) adalah proses mengubah data kategori menjadi data numerik. Untuk teknik Encoding fitur kategori menggunakan One-Hot Encoding. One-Hot Encoding untuk data nominal. Data nominal diklasifikasikan tanpa urutan atau peringkat. Untuk cara melakukan one-hot encoding dengan modul [pd.get_dummies](https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html) dari pandas.

  Sebelum One-Hot Encoding.
  
  ![Sebelum One-Hot Encoding](https://user-images.githubusercontent.com/72246401/137140342-29ea8b4a-d6fd-4cb9-842e-3e7d28ed4b7c.jpg)
  
  Setelah One-Hot Encoding.
  
  ![Sesudah One-Hot Encoding](https://user-images.githubusercontent.com/72246401/137140333-0d18c3ee-3003-4973-85f0-11b7c4ba3911.jpg)
  
  
-  Melakukan **_Data Splitting_**

  **_Data Splitting_** adalah pembagian dataset menjadi 2, yaitu data latih _(train data)_ dengan rasio 80% dan data test _(test data)_ dengan rasio 20%. data latih _(train data)_ berguna untuk pelatihan model dan data test _(test data)_ untuk menguji model. Pembagian dataset dilakukan modul [train_test_split](https://scikit-learn.org/0.24/modules/generated/sklearn.model_selection.train_test_split.html#sklearn.model_selection.train_test_split) dari scikit-learn.


- Melakukan **standardisasi data** pada fitur numerik

  Fungsi dari standarisasi nilai pada fitur numerik adalah untuk membuat numerical data pada varibel independen memiliki rentang nilai (scale) yang sama. Untuk melakukan standardisasi data, digunakan fungsi [StandardScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html). StandardScaler membuat mean menjadi 0 atau mendekati 0 dan 68% dari rentang data diantara -1 dan 0. StandarScaler mengubah distribusi data menjadi Distribusi Gaussian atau Distribusi Normal.
  
  ![Standardization](https://user-images.githubusercontent.com/72246401/137143994-61236a0b-ca40-49a8-bc94-9e2d9ea22cff.png)
  

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
