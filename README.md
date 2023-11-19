# FinalProject
Final Project Bank Churn Prediction

## Step 1: EDA Summary

- Dapat terlihat bahwa customer churn kebanyakan berada di usia 26 - 45 (Adults) dan 46 - 65 (Elderly) dibandingkan dengan usia yang lebih muda. Hal ini bisa saja disebabkan oleh preferensi servis dari setiap kategori umur. Oleh karena itu, bank direkomendasi kan untuk me-review kembali targeted nasabah ini dan bisa membuat strategi khusus dapat berupa program atau promo khusus untuk nasabah tersebut
- Kebanyakan customer yang churn ialah customer yang bukan member yang aktif. Oleh karena itu, direkomendasikan untuk bank membuat sebuah program yang dimana dapat membuat member yang tidak aktif ini untuk menjadi aktif untuk menghindari customer menjadi churn
- Kebanyakan customer yang churn ialah customer yang female. Oleh karena itu, direkomendasikan untuk bank membuat sebuah program khusus untuk men-engage customer perempuan untuk mencegah customer menjadi churn

## Step 2: Pre-Processing Summary

### Data Cleansing:
  - **Handling missing value:** Pada dataset tidak ditemukan missing value, sehingga handling missing value tidak dilakukan.
  - **Handling missing value:** Pada dataset tidak ditemukan duplicated value, sehingga handling duplicated value tidak dilakukan.
    
### Feature Engineering:
  - Dilakukan analisa multikolinearitas antar feature 'NumOfProducts' dan 'Balance' karena kedua fitur tersebut memiliki korelasi yang moderat (-0.30) menggunakan VIF (Variance Inflation Factor). Hasil perhitungan menunjukkan nilai VIF yang relatif kecil (VIF<5) dan menunjukkan tidak ada bukti multikolinearitas feature 'NumOfProducts' dan 'Balance'. Oleh karena itu, kedua feature tersebut akan tetap digunakan.
  - **Feature Selection:** Dilakukan drop column terhadap kolom 'RowNumber', 'Surname', 'CustomerId', karena ketiga kolom tersebut dianggap redundant.
  - **Feature Extraction:** Dilakukan penambahan fitur baru yaitu:
      1. 'Balance_Category': mengkategorikan balance berdasarkan jumlah menjadi 'Low','Medium, 'High'
      2. 'CreditScore_Range': mengkategorikan credit score berdasarkan nilai menjadi 'Poor', 'Fair', 'Good', 'Excellent'
      3. 'Tenure_Category': mengkategorikan tenure berdasarkan lama periode menjadi 'Short Term', 'Medium Term', 'Long Term'
      4. 'Salary_Range': mengkategorikan salary berdasarkan jumlah menjadi 'Low', 'Medium', 'High','Very High'
  Pengkategorian 4 feature tersebut dilakukan berdasarkan nilai min, quartile 1, 2, 3, dan max pada masing-masing kolom.
  - **Feature Encoding:** Dilakukan encoding menggunakan one hot encoding pada feature 'Geography', dan menggunakan label encoding pada feature 'Gender','Group_Age','Balance_Category','CreditScore_Range', 'Tenure_Category', dan 'Salary_Range' untuk menjadikan datatype pada kolom tersebut menjadi numeric.
    
### Split Data to Train and Test:
  - Dilakukan pemisahan (split) data menjadi train dan test dengan rasio 80:20.
    
### Handle Outlier:
  - Dilakukan uji coba filter outlier dengan Z-Score dan IQR menggunakan dataset train. Dengan menggunakan Z-Score atau IQR, outlier berhasil difilter. Perbedaan jumlah data menggunakan Z-Score adalah 2.75% dan menggunakan IQR adalah 6.06% dari jumlah value pada dataset awal. Namun, pada tahap ini proses outlier removal tidak dilakukan karena outlier paling banyak berada di feature 'Age', yang mana distribusi age pada nasabah adalah hal yang wajar. Proses untuk tahap selanjutnya dapat menggunakan dataset yang telah displit.
    
### Feature Transformation:
  - Melakukan normalisasi dengan MinMaxScaling. Normalisasi dibandingkan dengan menggunakan standarisasi memang normaliasi kurang robust terhadap outlier, namun karena sudah dilakukan pengecekan outlier pada data, maka penggunaan motode transformasi normalisasi seharusnya tidak bermasalah.
    
### Handle Class Imbalance:
  - Pengecekan class distribution sebelum dilakukan handle class imbalance pada kolom target adalah 6356 No (0), dan 1644 Yes (1).
  - Pengecekan class distribution setelah dilakukan oversampling pada kolom target adalah 6356 untuk No (0), dan Yes (1).
  - Pengecekan class distribution setelah dilakukan undersampling pada kolom target adalah 1644 untuk No (0), dan Yes (1).
  - Diputuskan untuk menggunakan undersampling karena target prediksi category churn (value = 1) lebih sedikit, sehingga jika oversampling digunakan dapat menyebabkan bias (akibat jumlah data sintesis yang akan ter-generate akan relatif banyak).
    
### 4 Fitur Tambahan yang belum ada di dataset:
  1. Balance-to-Salary Ratio:
     Menghitung rasio antara saldo akun dan estimasi gaji pelanggan. Rasio ini dapat memberikan gambaran tentang seberapa besar bagian dari gaji yang disimpan atau diinvestasikan oleh pelanggan.
  2. Average Transaction Amount:
     Menghitung rata-rata jumlah transaksi per pelanggan. Ini dapat memberikan wawasan tentang seberapa sering pelanggan berinteraksi dengan produk atau layanan, dan seberapa besar nilai transaksi yang mereka lakukan.
  3. Tenure and NumOfProducts Interaction: 
    Fitur ini dapat memberikan model informasi tambahan tentang seberapa intensif pelanggan menggunakan produk atau layanan selama periode waktu tertentu. Dimana dapat diasumsikan bahwa semakin lama seseorang menjadi pelanggan dan semakin banyak produk yang mereka miliki, semakin kuat keterikatan mereka dengan layanan atau produk perusahaan tersebut.
  4. Salary to CreditScore Ratio:
     fitur ini mencerminkan seberapa besar pendapatan seseorang dibandingkan dengan skor kredit mereka. Rasio ini dapat memberikan wawasan tentang seberapa baik seseorang mengelola utang atau kredit relatif terhadap tingkat pendapatan mereka.



  
