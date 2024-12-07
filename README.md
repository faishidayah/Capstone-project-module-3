# Capstone project module 3


## Business Problem Understanding
### 1. Background
California adalah salah satu pasar properti paling dinamis dan menarik di dunia. California memiliki ekonomi terbesar di Amerika Serikat dan merupakan salah satu ekonomi terkuat di dunia. beberapa sektor utama yang menjadi tulang punggung perekonomian di california adalah Teknologi, pertanian , hiburan dan media. dengan lebih dari 39 juta jiwa, permintaan akan properti baik untuk tempat tinggal maupun untuk tujuan komersial terus meningkat. tetapi juga menghadapi tantangan signifikan antara lain Kombinasi harga tinggi, peraturan ketat, dan risiko lingkungan oleh karena itu penentuan harga properti memerlukan strategi yang matang.
### 2. Problem Statement
perusahaan ingin menetapkan harga properti yang kompetitif dan menarik di pasar California dengan tetap memastikan margin keuntungan yang optimal, tetapi juga mempertimbangkan daya tarik pembeli
### 3. Goals
Berdasarkan permasalahan tersebut, perusahaan membutuhkan tool yang dapat membantu mereka untuk memprediksi harga rumah secara akurat. fitur-fitur yang dimiliki oleh sebuah rumah seperti lokasi rumah, usia rata-rata rumah, total ruangan, total kamar tidur dan lain-lain dapat menambah keakuratan prediksi harga rumah, sehingga bisa memberikan profit yang optimal bagi perusahaan serta harga yang menarik bagi pembeli.
### 4. Analitical Approach
Melakukan analysis data untuk mengetahui hubungan antar variabel dan menemukan pola dari fitur-fitur yang ada yang mejadi pembeda suatu rumah dengan rumah yang lain. kemudian membangun machine learning yang akan menjadi tool yang digunakan perusahaan untuk memprediksi harga rumah secara akurat
### 5. Metrics Evaluation
Evaluasi metrik yang akan digunakan antara lain sebagai berikut:
- MAE ==> Rata-rata nilai absolut error. Memberikan gambaran tentang seberapa besar rata-rata kesalahan dalam satuan yang sama dengan target.
- MAPE ==> Rata-rata persentase error absolut antara nilai aktual dan prediksi. Berguna untuk mengevaluasi performa model di berbagai skala.
- RMSE ==> Akar kuadrat dari Mean Squared Error. Mengukur rata-rata error dengan penalti untuk error besar.

## Data Understanding
Deskripsi Kolom:
longitude ==> Ukuran seberapa jauh ke barat sebuah rumah; nilai yang lebih tinggi berarti lebih jauh ke barat
latitude ==> Ukuran seberapa jauh ke utara sebuah rumah; nilai yang lebih tinggi berarti lebih jauh ke utara
housingMedianAge ==> Usia rata-rata sebuah rumah dalam satu blok; angka yang lebih rendah berarti bangunan yang lebih baru
totalRooms ==> Jumlah total kamar dalam satu blok
totalBedrooms ==> Jumlah total kamar tidur dalam satu blok
population ==> Jumlah total orang yang tinggal dalam satu blok
households ==> Jumlah total rumah tangga, sekelompok orang yang tinggal dalam satu unit rumah, untuk satu blok
medianIncome ==> Pendapatan rata-rata untuk rumah tangga dalam satu blok rumah (diukur dalam puluhan ribu Dolar AS)
medianHouseValue ==> Nilai rumah rata-rata untuk rumah tangga dalam satu blok (diukur dalam Dolar AS)
oceanProximity ==> Lokasi rumah sehubungan dengan laut/samudra

## Data Preprocesing
1. Missing value handling
2. Data duplikat
3. Outliers handling
4. feature engineering
   menambah 3 kolom yaitu:
   - rooms_per_household ==> rata-rata ruangan per rumah tangga
   - bedrooms_per_room ==> rata-rata kamar tidur per rumah tangga
   - pop_per_house ==> rata-rata populasi per rumah tangga
   menghapus kolom:
   - total_rooms
   - total_bedrooms
   - population
5. data correlation

## Modelling 
1. One hot encoding kolom ocean_proximity
2. Data Splitting
   - train size ==> 80%
   - test size ==> 20%
   - random state ==> 42
3. Model selection
   model yang digunakan adalah XGBoost karena mendapat score terbaik berdasarkan benchmarking
4. tuning
   hyperparameter tuning yang akan digunakan adalah:
   - max_depth ==> 7
   - learning rate ==> 0.1
   - n_estimators ==>  188
   - subsample ==> 0.9
   - gamma ==> 3
   - cosample_bytree 0.7
   - reg_alpha 0.05994842503189409
5. perbandingan score sebelum dan sesudah tuning:
   Setelah dilakukan tuning, score RMSE, MAE dan MAPE mengalami penurunan yang artinya model mengalami peningkatan performa meskipun tidak signifikan.
   - RMSE 42548.726617 ==> 41424.476807
   - MAE 28985.347693 ==> 27738.313086
   - MAPE 0.170032 ==> 0.161551
  
## Conclusion
- berdasarkan pemodelan yang sudah dilakukan, fitur __'ocean_proximity'__ dan __'median_income'__ merupakan fitur yang paling berpengaruh terhadap __'median_house_value'__
- Metrik evaluasi yang digunakan adalah MAE, MAPE dan RMSE. score MAE ==> 27738.31 dan MAPE ==> 16.1%, sehingga kita dapat menyimpulkan bahwa prediksi harga rata-rata model akan meleset sekitar 16% atau 27738.31 USD dari harga yang seharusnya. model yang dibuat ini digunakan untuk memprediksi harga properti/rumah yang ada di california tetapi memiliki limitasi yang mana model hanya bisa memprediksi __'median_house_value'__ pada rentang 14.999 hingga 480275.0 USD. 
- tetapi tidak menutup kemungkinan juga prediksi model meleset lebih jauh dari nilai aktual nya baik itu overestimation maupun underestimation. hal ini dikarenakan terbatasnya fitur yang terdapat pada dataset sehingga model hanya memiliki sedikit informasi penting yang dapat membantu menjelaskan nilai target.
  
## Recommendation
1. untuk dataset: 
- hanya ada sedikit fitur yang berkorelasi tinggi pada target, maka dari itu perlu ditambahkan beberapa fitur seperti __luas bangunan__, __luas tanah__, __fasilitas rumah__, dan jarak perumahan ke fasilitas umum (__pusat kota__, __bandara__, __mall__ dan lain-lain)
- dataset ini merupakan informasi dari sensus California tahun 1990. untuk memprediksi harga perumahan untuk saat ini dibutuhkan data yang lebih update. karena dataset sudah berusia 34 tahun yang pastinya harga perumahan sudah terkena dampak inflasi
2.  untuk model machine learning: 
- tuning menggunakan __GridSearch__ kamudian hyperparameter optimization menggunakan __Optuna__ atau __Bayesian Optimization__ untuk proses optimasi lebih cepat dan efisien
3.  untuk developer: 
- untuk keuntungan yang maksimal, developer perlu mempertimbangkan lokasi pembangunan rumah. semakin dekat lokasi rumah/properti dengan laut maka semakin tinggi harga rumah/properti tersebut.
