<a name="readme-top"></a>
# HASIL ANALISIS TUGAS BESAR PENGOLAHAN CITRA DIGITAL 

## Kelompok 13
### M. Ilham Abdul Shaleh (F1D022061)
### I Putu Raditya Satya Karsa Wardana (F1D022067)
### Muhammad Syahid Agil Assahbani (F1D022079)
### Nurul Qalbi Zahrani (F1D022150)
### Rahel Juliana Situmeang (F1D22320022)

# Judul _Project_ 
## "Identifikasi Tanaman Obat untuk Mendukung Pengobatan Tradisional bagi Dokter dan Masyarakat Awam"


## Latar Belakang
Pengobatan tradisional telah menjadi bagian integral dari praktik kesehatan di berbagai budaya selama berabad-abad. Dengan meningkatnya minat terhadap solusi kesehatan alami dan holistik, identifikasi tanaman obat menjadi semakin penting. Teknologi modern dapat memainkan peran kunci dalam memfasilitasi identifikasi yang akurat dan efisien, sehingga mempermudah dokter dan masyarakat awam untuk memanfaatkan tanaman obat dengan cara yang aman dan efektif.

Grey-Level Co-Occurrence Matrix (GLCM) adalah salah satu metode yang dapat digunakan untuk analisis tekstur dalam citra digital. Dengan menggunakan GLCM, kita dapat mengekstraksi fitur-fitur penting dari gambar tanaman obat, sehingga memungkinkan klasifikasi yang lebih akurat. Algoritma ini memberikan peluang untuk menggabungkan pengetahuan tradisional dengan teknologi canggih, menciptakan solusi yang dapat meningkatkan pengobatan tradisional.

Pemilihan topik ini didasarkan pada kebutuhan untuk mendukung pengobatan tradisional dengan alat modern yang dapat diakses oleh profesional medis dan masyarakat umum. Dengan memanfaatkan teknologi canggih seperti GLCM, kita dapat membantu dalam identifikasi tanaman obat yang lebih cepat dan akurat, mengurangi risiko kesalahan, dan meningkatkan efektivitas pengobatan.

## Batasan Masalah
1. Validasi Akurasi Identifikasi
    
    Penelitian ini akan fokus pada validasi kemampuan GLCM dalam mengidentifikasi tanaman obat dengan tingkat akurasi yang tinggi. Pengujian akan dilakukan menggunakan dataset citra tanaman obat yang terbatas namun representatif.

2. Keterbatasan Data
    
    Data yang tersedia untuk penelitian ini mungkin memiliki keterbatasan dalam jumlah dan variasi jenis tanaman obat. Analisis akan dibatasi pada tanaman obat yang dapat diakses dalam dataset yang tersedia.

3. Penanganan Variabilitas Citra
    
    Citra tanaman obat dapat memiliki kompleksitas latar belakang dan variasi kondisi pencahayaan. Oleh karena itu, GLCM harus diuji dan dioptimalkan untuk dapat mengatasi variasi ini dengan efektif.

## Data Understanding

Pada Project Analisis Tanaman Herbal ini digunakan kumpulan data (dataset) berupa gambar dari berbagai macam tanaman herbal yang diambil dari situs www.kaggle.com kemudian di dalamnya terdapat 7 label dengan total data 710. https://www.kaggle.com/datasets/trientran/oriental-medicinal-herb-images?select=Archive

## Data Loading

Pada tahapan ini akan dilakukan pembacaan dataset beserta labelnya dari folder. Nama sub-folder akan digunakan sebagai label kelas.

* Data Loading
    1. Buat script untuk memuat gambar dari folder dan menggunakan nama folder sebagai label.
    2. Simpan gambar dan label ke dalam variabel.

### Format Nama
Kami melakukan perubahan nama untuk setiap sub-folder dan citra untuk memudahkan dalam pendataan dan pemanggilan sampel. Nama sub-folder yang sebelumnya menggunakan kode "1676290699455" menjadi "averrhoa-carambola"
kemudian untuk citra yang sebelumnya menggunakan kode "7TX04L.c06f2a4d1f54.jpg" menjadi "averrhoa-carambola-01.jpg"


## Resizing 
Pada tahapan ini proses resizing dilakukan ke seluruh citra yang bertujuan untuk mengubah ukuran gambar ke dimensi yang diinginkan dengan cara membandingkan ukuran asli citra dengan ukuran target kemudian mengganti ukuran gambar dengan target yang diinginkan jika tidak sesuai.

## Explorasi Data

Berdasarkan hasil "data loading" didapatkan beberapa informasi, yaitu :
1. Jumlah citra pada dataset adalah 710. Informasi ini berasal dari proses Data Loading saat proses pembacaan dan penelusuran gambar pada setiap sub-folder dataset.
2. Didapatkan informasi berupa nama label dan jumlah citra dari setiap sub-folder dataset, yaitu :
    
    a. averrhoa-carambola : 108

    b. cordyline-fruticosa : 120

    c. paedaria-tomentosa : 100

    d. piper-betle : 105

    e. piper-sarmentosum

    f. plyscias-fruticosa : 110

    e. stachytarpheta-jamaicensis : 100

## Sampel Data 
- Sampel Data pada percobaan untuk projek analisis tanaman herbal ini diambil dari setiap sub-folder dataset. Masing-masing dataset akan diambil 1 buah citra sebagai perwakilan dari 7 sub-folder untuk memastikan operasi-operasi yang akan dilakukan berhasil diimplementasikan ke semua citra.

## Distribusi Data
Berdasarkan teknik pengambilan citra pada dataset dengan konsep penelusuran untuk setiap sub-folder, didapatkan informasi berupa distribusi data dan total data untuk setiap sub-folder, yaitu :
Data Distribution:  {'averrhoa-carambola': 108, 'cordyline-fruticosa': 120, 'paedaria-tomentosa': 100, 'piper-betle': 105, 'piper-sarmentosum': , 'polyscias-fruticosa': 110, 'stachytarpheta-jamaicensis': 100}

## Data Preparation
## Preprocessing

Pada percobaan yang kami lakukan, Teknik Preprocessing yang digunakan adalah Resizing, Ubah Greyscale, Thresholding, Noise Reduction, Deteksi Tepi, Normalisasi

# Tahapan Preprocessing

1.	Resize: Mengubah ukuran gambar ke ukuran yang konsisten.
- Tujuan: Menyeragamkan dimensi gambar untuk mempercepat proses komputasi dan memastikan konsistensi input model.
- Dampak: Dapat meningkatkan akurasi dengan memberikan input yang seragam, namun jika ukuran terlalu kecil, detail penting bisa hilang.
2.	Convert to Gray: Mengubah gambar menjadi skala abu-abu.
- Tujuan: Mengurangi kompleksitas data dengan menghapus informasi warna, yang mungkin tidak relevan untuk identifikasi.
- Dampak: Dapat meningkatkan akurasi dengan fokus pada fitur bentuk dan tekstur, namun bisa menghilangkan informasi warna yang mungkin penting.
3.	Thresholding: Menerapkan ambang batas untuk memisahkan objek dari latar belakang.
- Tujuan: Meningkatkan kontras antara objek dan latar belakang, mempermudah deteksi fitur.
- Dampak: Dapat meningkatkan akurasi jika ambang batas dipilih dengan baik, namun bisa menurunkan akurasi jika detail penting hilang.
4.	Edge Detection: Mendeteksi tepi objek dalam gambar.
- Tujuan: Menyoroti kontur dan tepi yang penting untuk identifikasi objek.
- Dampak: Dapat meningkatkan akurasi dengan fokus pada bentuk dan kontur, namun bisa menambahkan noise jika deteksi tepi tidak tepat.
5.	Normalization: Menormalkan nilai piksel gambar.
- Tujuan: Menjaga nilai piksel dalam rentang tertentu untuk konsistensi input model.
- Dampak: Dapat meningkatkan akurasi dengan membantu model konvergen lebih cepat dan stabil.

## Analisis Masing-Masing Percobaan
**Analisis Hasil:**
Analisis Akurasi Berdasarkan Preprocessing:
1.	Percobaan

  	 Preprocessing: Resize, Convert to Gray, Edge Detection Normalization.
  	
  	 Accuracy: 0.58

Setelah melakukan percobaan dengan proses-proses yang ditentukan, didapatkan informasi dari Percobaan bahwa dengan semua tahapan preprocessing memberikan akurasi tertinggi, menunjukkan bahwa kombinasi dari semua langkah tersebut membantu model untuk lebih baik dalam mengenali tanaman herbal.

## Modeling
Untuk proses hyperparameter tuning pada model, dilakukan dengan membagi data yang sudah dipilih fiturnya menjadi data training. Data tersebut dinormalisasi menggunakan min-max scaling agar setiap fitur memiliki skala yang sama, sehingga model machine learning dapat lebih efektif dalam belajar dari data. lalu menggunakan model berbeda: CNN, K-Nearest Neighbors (KNN), Support Vector Machine (SVM), dan Random Forest. Setiap model dilatih menggunakan data latih yang dinormalisasi, dan kemudian prediksinya diuji menggunakan data uji yang juga dinormalisasi.

## Evaluation
 
Hasil pengujian yang dilakukan pada model CNN menunjukkan adanya perbedaan signifikan dalam akurasi antara dataset original yang belum melalui proses preprocessing dan dataset yang telah mengalami tahap preprocessing. Dalam dataset original, akurasi yang diperoleh sebesar 58% menunjukkan keterbatasan dalam kemampuan model untuk mengenali pola dan fitur yang ada dalam data yang belum diolah. 

Terdapat beberapa faktor yang dapat menyebabkan hasil akurasi rendah pada dataset original. Pertama, dataset original belum melalui tahap preprocessing, yang berarti data tersebut belum mendapatkan perlakuan atau pemrosesan apapun sebelumnya. Hal ini dapat mengakibatkan keberadaan noise atau ketidakseimbangan kelas dalam data, yang mempersulit tugas model dalam mengenali pola yang relevan.

Selain itu, jumlah dataset yang kurang juga dapat menjadi faktor penyebab akurasi rendah pada dataset original. Semakin banyak data yang digunakan dalam pelatihan, semakin besar kemungkinan model untuk menemukan pola yang lebih umum dan menggeneralisasikan dengan lebih baik. Dengan jumlah dataset yang terbatas, model mungkin menghadapi kesulitan dalam mempelajari representasi yang cukup dari data yang ada.

Selanjutnya, hasil akurasi yang rendah pada dataset original juga dapat menunjukkan adanya fenomena underfitting pada model CNN yang digunakan. Underfitting terjadi ketika model terlalu sederhana atau memiliki kapasitas yang terbatas sehingga tidak dapat secara efektif mempelajari pola yang ada dalam data. Ini dapat mengakibatkan kurangnya kompleksitas dan fleksibilitas dalam model, sehingga akurasi yang diperoleh menjadi rendah.

Namun, hasil pengujian menunjukkan peningkatan akurasi yang signifikan pada dataset yang telah melalui tahap preprocessing. Akurasi sebesar 56% pada dataset hasil preprocessing menunjukkan bahwa langkah-langkah preprocessing yang dilakukan berhasil dalam meningkatkan kualitas data dan performa model. Preprocessing dapat mencakup langkah-langkah seperti penghilangan noise, normalisasi skala, atau penyeimbangan kelas yang tidak seimbang.

Meskipun demikian, perlu diperhatikan bahwa meskipun akurasi pada dataset hasil preprocessing meningkat, persentase akurasi yang diperoleh masih relatif rendah. Hal ini menandakan bahwa model CNN sederhana yang digunakan masih memiliki keterbatasan dalam memahami dan memodelkan hubungan yang lebih kompleks dalam data.

Untuk meningkatkan performa model, ada beberapa langkah yang dapat dipertimbangkan. Pertama, kompleksitas model CNN dapat ditingkatkan dengan menambahkan lebih banyak lapisan atau menggunakan arsitektur yang lebih canggih. Selain itu, pengumpulan lebih banyak data latihan yang berkualitas dapat membantu model mengenali variasi yang lebih banyak dan pola yang ada dalam data.

Selain itu, evaluasi fungsi kehilangan (loss function) yang digunakan selama pelatihan juga perlu dipertimbangkan. Pemilihan fungsi kehilangan yang sesuai dengan masalah yang dihadapi dapat mempengaruhi performa model secara signifikan.

Terakhir, penting untuk diingat bahwa analisis ini didasarkan pada metrik evaluasi tunggal yaitu akurasi. Namun, penting untuk melibatkan metrik evaluasi tambahan seperti presisi, recall, atau F1-score untuk mendapatkan gambaran yang lebih komprehensif tentang performa model Anda. Secara keseluruhan, hasil pengujian model CNN sederhana yang telah dilakukan menunjukkan perbedaan signifikan dalam akurasi antara dataset original dan dataset hasil preprocessing. Sementara langkah-langkah preprocessing berhasil meningkatkan akurasi, masih terdapat ruang untuk meningkatkan performa model dengan mengambil langkah-langkah yang telah disebutkan sebelumnya.
