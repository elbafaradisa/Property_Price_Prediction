# Capstone-Project-3 : California Housing Price Prediction
California merupakan negara bagian Amerika Serikat yang terpadat menurut kepadatan penduduk dan terbesar ketiga berdasarkan wilayah. California juga menjadi tempat impian untuk tinggal bagi banyak orang karena keindahan, pantai, dan status negara bagian itu yang dikenal sebagai salah satu ekonomi terbesar kelima di dunia. Bagi perusahaan di bidang properti tentunya hal tersebut dapat menjadi peluang yang sangat menguntungkan bagi bisnisnya. Walaupun bisnis properti di California memiliki peluang yang menjanjikan, namun terdapat hal yang sangat perlu untuk diperhatikan yaitu dalam penentuan harga properti. 

Biasanya dalam menentukan harga rumah dilakukan dengan cara membandingkan properti rumah yang ingin dijual dengan properti lain disekitar daerah tersebut dan terkadang harga yang dijual cenderung tinggi atau bisa saja terlalu rendah. Ketidakstabilan penentuan harga rumah ini sangat berisiko untuk agen properti karena akan berdampak terhadap penjualan. Jika harganya terlalu tinggi dibanding properti-properti lain dengan fitur sejenis di sekitar areanya, tentu akan terjadi penurunan penjualan. Sebaliknya, jika terlalu rendah, tentu penjual tidak akan mendapatkan profit yang sepadan. Banyak faktor yang dapat mempengaruhi harga rumah seperti lokasi, usia rumah, jumlah ruangan, jumlah kamar, populasi di sekitar lingkungan rumah, dan lain sebagainya yang perlu diperhatikan dalam menentukan harga rumah. 

### **Problem Satement**

Dalam menentukan harga rumah tidak cukup hanya dengan membandingkan harga dengan rumah-rumah yang ada di sekitarnya atau hanya dengan mengikuti harga pasar. Salah satu tantangan besar untuk sebuah perusahaan agen properti adalah memiliki bisnis yang dapat menguntungkan secara finansial bagi penjual rumah dan memberikan kepuasan bagi pembelinya. Semakin tingginya minat pembelian rumah di California, maka sangat penting untuk dapat menentukan harga rumah secara tepat agar kompetitif dengan harga jual rumah lainnya. 

### **Tujuan**

Berdasarkan permasalahan di atas, perusahaan agen properti memerlukan sebuah *"tool"* yang dapat membantu dalam memprediksi harga rumah dengan tepat. *Tool* ini dapat digunakan ketika seseorang ingin menjual rumahnya melalui agen properti sebagai perantara, kemudian *tool* tersebut digunakan untuk melakukan prediksi harga rumahnya berdasarkan faktor-faktor tertentu misalnya lokasi rumah, usia rumah, jumlah ruangan, jumlah kamar, populasi di sekitar lingkungan rumah, dan keadaan lingkungan rumah. 

Bagi perusahaan agen properti, *prediction tool* yang dapat memberikan prediksi harga rumah dengan tepat, tentu dapat meningkatkan jumlah penjualan nantinya.

### **Metric Evaluation**

Evaluasi metrik yang akan digunakan adalah Mean Absolute Error (MAE) dan Mean Absolute Percentage Error (MAPE). MAE adalah rataan nilai absolut dari error untuk mengetahui rata rata selisih harga akurat dengan harga prediksi dalam bentuk US Dollar. 
Sedangkan MAPE adalah rataan persentase error yang digunakan untuk melihat berapa persentase rata-rata error antar nilai aktual dengan nilai prediksi. Semakin kecil nilai MAE dan MAPE yang dihasilkan, artinya model yang digunakan semakin akurat dalam memprediksi harga rumah di California sesuai dengan limitasi fitur yang digunakan. 

### **Dataset**
- Dataset berisikan data listing rumah-rumah yang ada di California berdasarkan sensus data tahun 1990.
- Setiap baris data merepresentasikan informasi terkait rumah-rumah di California.

**Attributes Information**

| **Nama Kolom** | **Tipe Data** | **Deskripsi** |
| --- | --- | --- |
| longitude | Float | Longitude coordinates |
| latitude | Float | Latitude coordinates |
| housing_median_age | Float | Median age of house in a block |
| total_rooms | Float | Total rooms in a block |
| total_bedrooms | Float | Total bedrooms in a block |
| population | Float | Number of people residing in a block |
| households | Float | A group of people residing within a house for a block |
| median_income | Float | Median income for households in a block (USD) |
| ocean_proximity | Object | Location of the house |
| median_house_value | Float | Median house value for households in a block |

### **Machine Learning**

**Hasil evaluasi algoritma**

| **Model** |	**Mean_MAE** | **Std_MAE** |	**Mean_MAPE** |	**Std_MAPE** |
| --- | --- | --- | --- | --- | 
| 0 |	Linear Regression |	-42895.847709 |	933.230803 | -0.244313 | 0.004216 |
| 1 | KNN Regressor |	-36878.775826 |	797.230200 |	-0.205670	| 0.004216 |
| 2 | DecisionTree Regressor |	-42698.282086	| 1141.359187 |	-0.244493 |	0.008969 |
| 3 |	RandomForest Regressor |	-30996.961569 |	652.838242 |	-0.174634 |	0.005542 |
| 4	| XGBoost Regressor |	-29947.200989 |	948.152987 |	-0.169561 |	0.006721 |

Berdasarkan evaluasi hasil dari lima model yang diuji terhadap data training, dilihat dari nilai MAE dan MAPE yang paling kecil, XGBoost adalah model yang paling baik. Kemudian dilakukan testing pada model XGBoost :

|  | MAE |	MAPE |
| --- | --- | --- |
| XGBoost |	29341.991996 |	0.175416 |

**Hyperparameter Tuning**

Sebelum tuning :

| | MAE |	MAPE |
| --- | --- | --- |
| XGBoost |	29341.991996 |	0.175416 |

Setelah tuning :
| | MAE	| MAPE |
| --- | --- | --- |
| XGB |	29154.068443 |	0.16986 |

Setelah dilakukan hyperparameter tuning, nilai MAE dan MAPE berkurang, hal ini menunjukkan bahwa performa model mengalami peningkatan walaupun sedikit.

### **Kesimpulan**
Berdasarkan pemodelan yang telah dilakukan dapat disimpulkan :
* XGBoost memiliki nilai MAE dan MAPE paling kecil mendekati nol sehingga dipakai sebagai model akhir untuk melakukan prediksi harga rumah.

* Fitur yang paling berpengaruh terhadap penentuan harga rumah (median_house_value) adalah fitur ocean_proximity dan median_income.

* Nilai MAPE yang dihasilkan oleh model setelah dilakukan hyperparameter tuning adalah ~16,9%. Jika model yang telah dibuat ini digunakan untuk memperkirakan harga rumah baru di California pada rentang nilai seperti yang dilatih terhadap   
  model (maksimal harga 480100 USD), maka perkiraan harganya rata-rata akan meleset kurang lebih sebesar 16,9% dari harga seharusnya. Namun, tidak menutup kemungkinan juga prediksinya akan meleset lebih jauh karena adanya bias yang dihasilkan model jika dilihat dari visualisasi antara harga aktual dan prediksi, selain itu dataset yang digunakan dalam melatih model adalah data dari tahun 1990.
  
  
### **Rekomendasi**
Hal-hal yang dapat dilakukan untuk meningkatkan model agar menjadi lebih baik lagi :
1. Mengecek prediksi mana saja yang memiliki nilai error yang tinggi, variabel mana saja dan aspek apa yang menyebabkan model menghasilkan error yang tinggi. Kemudian bisa dilakukan training ulang dengan menggunakan feature engineering lainnya.
<br><br>   
1. Melakukan penambahan fitur yang lebih korelatif dengan target ('median_house_value'), seperti luas tanah, luas bangunan, fasilitas rumah, jarak ke pusat kota dan fasilitas umum, serta fitur lainnya.
<br><br>  
3. Untuk memperoleh hasil yang maksimal pada model, tidak disarankan menggunakan data perumahan yang harganya diatas 480100 US Dollar karena akan berisiko memiliki error yang sangat tinggi dan harga tersebut merupakan limitasi untuk model yang telah dibangun.
<br><br>   
