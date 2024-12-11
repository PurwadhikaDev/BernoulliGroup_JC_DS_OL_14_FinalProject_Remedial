# Bernoulii_JCDSOL_14_FinalProject_Remedial
# Hotel Booking Cancellations: A Predictive Approach

## Context

Bisnis perhotelan merupakan bisnis yang sangat kompetitif. Keberhasilan bisnis ini bergantung pada kepuasan pelanggan dan kualitas layanan yang diberikan kepada pelanggan. Bisnis perhotelan juga merupakan bisnis musiman dengan permintaan bervariasi sesuai musim nya. Pendapatan bisnis ini bergantung pada pemesanan setiap tamu dan pemesanan dapat berupa pemesanan langsung ke hotel atau travel agent baik yang konvensional ataupun online.

Selama dekade terakhir, telah terjadi peningkatan yang pesat dalam bisnis perhotelan yang dipicu dengan perkembangan industri pariwisata global. **Menurut data dari World Tourism Organization, peningkatan volume wisatawan internasional dari 25 juta pada tahun 1950 menjadi 1,4 miliar pada tahun 2019**. **(Source: [Link](https://www.e-unwto.org/doi/epdf/10.18111/9789284422456))**
Dataset ini berisi data pembatalan booking hotel-hotel di Portugal. Data tersebut berasa dari [Hotel Booking Demand dataset](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/data)

## Problem Statement

Pertumbuhan bisnis perhotelan ini juga menghadirkan tantangan baru bagi manajer hotel, terutama dalam hal mengelola `booking cancellation` yang dapat berdampak signifikan pada pendapatan dan efisiensi operasional. Proses manual dalam manajemen hotel, terutama dalam hal pengelolaan reservasi dan penentuan harga, sering kali menjadi hambatan signifikan di tengah dinamika industri yang cepat berubah. Dalam sebuah studi mengungkapkan bahwa hotel yang masih menggunakan metode manual untuk manajemen reservasi **mengalami rata-rata tingkat pembatalan sebesar 8%** , **pada pemesanan daring sebesar 17%**, **diikuti oleh pemesanan luring (12%)** dan **pemesanan travel agency (4%)**, sehingga berdampak negatif pada pendapatan dan efisiensi operasional. **(Source: [Link](https://www.emerald.com/insight/content/doi/10.1108/ijchm-08-2017-0509/full/html#:~:text=Evidence%20based%20on%20233%2C000%20bookings%20shows%20that%20the%20overall%20cancellation%20rate%20is%208%20per%20cent.%20Cancellation%20rates%20are%20highest%20for%20online%20bookings%20(17%20per%20cent)%2C%20followed%20by%20offline%20bookings%20(12%20per%20cent)%20and%20travel%20agency%20bookings%20(4%20per%20cent)))**. 

Dalam mengatasi masalah ini, penting untuk mengembangkan teknologi model machine learning yang dapat memperkirakan `booking cancellation`. Memprediksi `booking cancellation` dapat mencegah hotel kehilangan/pengurangan pendapatan (jika hotel memiliki ketentuan pembatalan booking yang dimana uang customer direfund full 100%), pengalokasian sumber daya yang tidak efisien, dan overbooking yang berujung pada ketidakpuasan pelanggan.

## Goals

1. Memprediksi apakah sebuah pemesanan bookingakan dibatalkan.
2. Mengidentifikasi faktor-faktor utama yang memengaruhi pembatalan pemesanan
   
## Stakeholder

1. Manajemen Hotel
   - Kendala : Kesulitan dalam merencanakan ketersediaan kamar dan pendapatan akibat pembatalan mendadak yang mengakibatkan kamar kosong dan penurunan pendapatan.
   - Benefit : Dapat merencanakan pengelolaan kamar dan memaksimalkan pendapatan melalui overbooking terkontrol.
  
## Analytic Approach

`1` : Canceled (Yes) --> Positive

`0` : Not Canceled (No) --> Negative

`Type 1 error : False Positive` --> **Resiko Biaya Operasional yang sia-sia + Kehilangan Pelanggan**. (Diprediksi Canceled, tetapi aktual nya Not Canceled)

`Type 2 error : False Negative` --> **Resiko Kekosongan Kamar + Overbooking**. (Diprediksi Not Canceled, tetapi aktual nya Canceled)

Berdasarkan konsekuensinya, `False Positive` memiliki dampak yang lebih merugikan dibandingkan dengan `False  Negative`. **Hal ini disebabkan oleh cost yang lebih tinggi dengan biaya operasional yang sia sia dan kehilangan pelanggan yang mempengaruhi kepuasaan pelanggan akibat yang kesalahan prediksi tamu membatalkan reservasi tetapi nyatanya tamu melakukan reservasi**. Kehilanggan pelanggan akan:

- Mengeluarkan biaya untuk mendapatkan pelanggan baru **(Customer Acquisition Cost)** 
- Berdampak secara jangka panjang akibat kepuasaan pelanggan yang dapat memutuskan untuk tidak memesan di hotel tersebut di masa mendatang **(Customer Lifetime Value Loss)**

Di sektor perhotelan, mengatasi tamu meskipun overbooking sangat beresiko karna mempengaruhi kepuasaan pelangga tetapi overbooking lebih mudah dikontrol dibandingkan dengan resiko kehilanggan loyalitas pelanggan yang dapat mempengaruhi pendapatan hotel dalam jangka panjang, karena tamu yang ingin tetap reservasi meskipun overbooking bisa diatasi dengan memberikan kompensasi kepada pelanggan akibat **[overbooking dengan tetap memaksimalkan pendapatan](https://www.channelrush.com/blog/what-is-overbooking-in-hotel-management#:~:text=By%20mastering%20this%20process%2C%20hotels%20can%20not%20only%20maximize%20their%20revenue%20potential%20from%20repeat%20guests%20but%20also%20maintain%20high%20levels%20of%20guest%20satisfaction%20despite%20the%20challenges%20posed%20by%20overbooking.)**. Oleh karena itu, penting untuk meminimalkan kesalahan `False Positive` untuk mengurangi kerugian operasional dan menjaga loyalitas pelanggan.

## Metric Evaluation 

Pada saat yang sama kedua kesalahan prediksi tersebut sama sama berdampak pada kehilangan pendapatan. Tetapi, dinilai berdasarkan konsekuensi nya `False Positive` berdampak pada kerugian yang lebih besar seperti **menambah biaya Customer Acquistion** dan juga **kehilangan Customer Lifetime Value**. Maka dari itu, perlu untuk menilai kinerja model dengan metrics yang seimbang dikeduanya dengan lebih menghindari `False Positive` yang berlebih. Pada kasus ini, kita dapat menggunakan **[F0.5 Score](https://mlexplained.blog/2023/01/09/when-to-use-f2-or-f0-5-score-f-beta-score/#:~:text=This%20enables%20one%20to%20choose%20an%20appropriate%20beta%20value%20to%20tune%20for%20the%20task%20at%20hand.%20If%20you%20want%20to%20minimize%20false%20positives%2C%20you%20want%20to%20increase%20the%20weight%20of%20precisions%2C%20so%20you%20should%20choose%20a%20value%20of%20beta%20less%20than%201%2C%20typically%200.5%20is%20chosen%20and%20is%20called%20F0.5%20score.)** untuk digunakan sebagai metrics kinerja model.

**`F.05 Method`**

**Evaluation berdasarkan F.05 Score** merupakan langkah untuk mengurangi sebanyak-banyaknya `False Positive` yang terjadi, sambil tetap mempertimbangkan recall. Menggunakan F0.5 score menjadi pilihan yang baik untuk mengevaluasi metrik hasil model prediksi dalam konteks `booking cancellation`, terutama ketika ingin mengurangi dampak dari pembatalan pemesanan pada detik-detik terakhir yang tidak terdeteksi oleh model. Jika F0.5 score rendah, ini menunjukkan bahwa banyak tamu yang diprediksi melakukan pembatalan tapi nyatanya melakukan reservasi pada menit-menit terakhir tanpa terdeteksi, yang dapat mengakibatkan hilangnya pelanggan dan pendapatan. Mengingat ketidakpastian perilaku tamu yang dinamis, **memaksimalkan F0.5 score menjadi bagian penting dari strategi manajemen hotel untuk memastikan bahwa cost dapat diminimalkan, dengan lebih fokus pada penghindaran kehilangan pelangga**n.

`F0.5 Score` --> mengukur proporsi rata-rata antara tamu yang benar-benar melakukan pembatalan booking dan melakukan reservasi, dengan penekanan pada kesalahan `False Positive`. Ini memberikan gambaran tentang seberapa baik model dalam menjaga keseimbangan antara precision dan recall, tetapi dengan lebih banyak perhatian pada precision.

$$
F0.5 = (1 + 0.5^2) \cdot \frac{\text{Precision} \cdot \text{Recall}}{(0.5^2 \cdot \text{Precision}) + \text{Recall}}
$$

Dengan F.05 Score yang tinggi, manajemen hotel memiliki kesempatan untuk mengambil tindakan proaktif untuk mencegah kehilangan pelanggan dengan menawarkan opsi rebooking atau reschedule. Hal ini membantu hotel dalam mempertahankan pendapatan dan loyalitas pelanggan, sehingga membuat model prediksi `booking cancellation` menjadi alat yang efektif untuk membuat strategi manajemen hotel.

## Research Questions
### Cancellation
  - How many bookings were canceled?
  - Which month have the highest number of cancelations?

### Guest 
  - Where do the guests come from?
  - Which are the most busy month?
  - How long do people stay at the hotels?

### Market Segment
  - Bookings by market segment?

## Description of Features

| Feature                 | Data Type | Description                                                                                                      |
|-------------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| hotel                         | Object    | Type of hotel (Resort Hotel or City Hotel)                                                                       |
| is_canceled                   | Integer   | Whether the booking was canceled (1) or not (0)                                                                  |
| lead_time                     | Integer   | Number of days between booking date and arrival date                                                             |
| arrival_date_year             | Integer   | Year of arrival date                                                                                             |
| arrival_date_month            | Object    | Month of arrival date (January - December)                                                                       |
| arrival_date_week_number      | Integer   | Week number of arrival date                                                                                      |
| arrival_date_day_of_month     | Integer   | Day of the month of the arrival date                                                                             |
| stays_in_weekend_nights       | Integer   | Number of weekend nights (Saturday and Sunday)                                                                   |
| stays_in_week_nights          | Integer   | Number of week nights (Monday to Friday)                                                                         |
| adults                        | Integer   | Number of adults                                                                                                 |
| children                      | Float     | Number of children                                                                                               |
| babies                        | Integer   | Number of babies                                                                                                 |
| meal                          | Object    | Type of meal booked (BB, HB, FB, SC)                                                                             |
| country                       | Object    | Country of origin of the customer                                                                                |
| market_segment                | Object    | Market segment designation (e.g., Direct, Corporate, Online TA)                                                  |
| distribution_channel          | Object    | Booking distribution channel (e.g., Direct, TA/TO)                                                               |
| is_repeated_guest             | Integer   | Whether the customer is a repeated guest (1) or not (0)                                                          |
| previous_cancellations        | Integer   | Number of previous cancellations                                                                                 |
| previous_bookings_not_canceled| Integer   | Number of previous bookings not canceled                                                                         |
| reserved_room_type            | Object    | Code of room type reserved                                                                                       |
| assigned_room_type            | Object    | Code for the type of room assigned to the booking                                                                |
| booking_changes               | Integer   | Number of changes made to the booking                                                                            |
| deposit_type                  | Object    | Type of deposit  to guarantee the booking (No Deposit, Non Refund, Refundable)                                   |
| agent                         | Float     | ID of the travel agency that made the booking                                                                    |
| company                       | Float     | ID of the company/entity that made the booking                                                                   |
| days_in_waiting_list          | Integer   | Number of days the booking was in the waiting list                                                               |
| customer_type                 | Object    | Type of booking (Contract, Group, Transient, Transient-Party)                                                    |
| adr                           | Float     | Average Daily Rate as defined by dividing the sum of all lodging transactions by the total number of staying nights|
| required_car_parking_spaces   | Integer   | Number of car parking spaces required                                                                            |
| total_of_special_requests     | Integer   | Total number of special requests made (e.g. twin bed or high floor)                                              |
| reservation_status            | Object    | Reservation last status (Canceled, Check-Out, No-Show)                                                           |
| reservation_status_date       | Object    | Date at which the last status was set                                                                            |

## Libraries Used

- `pandas`  
- `numpy`  
- `sklearn`  
  - `model_selection`  
    - `GridSearchCV`  
    - `StratifiedKFold`  
    - `train_test_split`  
    - `cross_validate`  
    - `cross_val_score`  
  - `preprocessing`  
    - `OneHotEncoder`  
    - `MinMaxScaler`  
    - `StandardScaler`  
    - `RobustScaler`  
  - `compose`  
    - `ColumnTransformer`  
  - `metrics`  
    - `classification_report`  
    - `confusion_matrix`  
    - `f1_score`  
    - `fbeta_score`  
    - `accuracy_score`  
    - `recall_score`  
    - `precision_score`  
    - `precision_recall_curve`  
    - `make_scorer`  
    - `roc_curve`  
    - `roc_auc_score`  
    - `RocCurveDisplay`  
    - `PrecisionRecallDisplay`  
  - `linear_model`  
    - `LogisticRegression`  
  - `tree`  
    - `DecisionTreeClassifier`  
  - `ensemble`  
    - `RandomForestClassifier`  
- `xgboost`  
  - `XGBClassifier`  
- `lightgbm`  
  - `lgb`  
- `imblearn`  
  - `over_sampling`  
    - `RandomOverSampler`  
    - `SMOTE`  
  - `under_sampling`  
    - `RandomUnderSampler`  
    - `NearMiss`  
  - `Pipeline`  
- `matplotlib`  
  - `pyplot`  
- `seaborn`  
- `plotly`  
  - `subplots`  
  - `express`  
  - `graph_objects`  
  - `colors`  
- `pycountry_convert`  
  - `pc`  
- `dython`  
  - `nominal`  
    - `associations`  
- `category_encoders`  
  - `OrdinalEncoder`  
  - `BinaryEncoder`  
- `joblib`  
- `warnings`


## Conclusion

### **1. Data Limitation**

Dalam analisis dan pengembangan model prediksi, batasan dataset diperlukan untuk meningkatkan relevansi dan keandalan. Lead time dibatasi antara 20-60 hari untuk fokus pada pemesanan reguler, menghapus data dengan **lead time lebih dari 60 hari**. **Zero occupancy (tamu = 0)** dihapus karena tidak logis dan tidak relevan. Untuk **ADR (Average Daily Rate), hanya data dengan nilai realistis (0-1000)** yang digunakan, menghindari kesalahan atau outlier. Batasan ini memastikan data yang konsisten dan relevan untuk menghasilkan prediksi yang akurat.
### **2. Machine Learning Model**
- Models: Random Forest Classifier

Random Forest adalah algoritma machine learning yang bekerja dengan membangun kumpulan pohon keputusan (decision trees) dan menggabungkan hasilnya untuk meningkatkan akurasi dan mengurangi risiko overfitting. Algoritma ini menggunakan teknik bootstrap sampling untuk membuat subset data pelatihan dan random feature selection untuk membangun setiap pohon, sehingga menghasilkan model yang lebih robust dan stabil. Random Forest juga mendukung evaluasi pentingnya fitur (feature importance) dan dapat menangani dataset dengan dimensi tinggi serta fitur kategori.

- Cara kerja pada kasus ini: 

Seperti yang ditunjukkan pada bagian eksperimen model, sebelum dilakukan tuning, model menggunakan Stratified Cross Validation untuk memastikan distribusi kelas yang seimbang dalam data pelatihan dan pengujian. Pada tahap ini, model mendapatkan hasil terbaik dengan menggunakan metrik F0.5 Score, yang lebih menekankan pada presisi dibandingkan recall.

Namun, setelah dilakukan tuning parameter, model mengalami overfitting, dengan perbedaan signifikan antara performa pada data pelatihan dan validasi. Hal ini menunjukkan bahwa meskipun model bekerja sangat baik pada data pelatihan, kemampuan generalisasi terhadap data baru menjadi kurang optimal. Regularisasi lebih lanjut mungkin diperlukan untuk mengatasi masalah ini.
### **3. Model Preprocess**

Dalam langkah-langkah preprocessing, berbagai teknik digunakan untuk memastikan data diproses secara optimal sebelum dimasukkan ke dalam model

- OneHotEncoder : Digunakan untuk fitur yang hanya memiliki kategori <5, mengubah data kategori menjadi bentuk numerik biner agar dapat diproses dengan efektif oleh model.
- BinaryEncoder : Digunakan untuk fitur kategori dengan banyak nilai unik (high-cardinality), mengubahnya menjadi format biner. Teknik ini membantu mengurangi dimensi data sambil tetap mempertahankan informasi yang ada.
- OrdinalEncoder : Digunakan untuk fitur kategori yang memiliki urutan atau hierarki nilai tertentu. Encoder ini mengonversi data kategori menjadi nilai numerik berdasarkan urutannya, sehingga model dapat mengenali hubungan antar kategori.
- RobustScaler: Digunakan untuk fitur numerik karena kemampuannya yang tahan terhadap outlier, sehingga model tidak terpengaruh oleh nilai ekstrem yang dapat menyebabkan bias.

Pemilihan teknik preprocessing ini bertujuan untuk memastikan bahwa data yang dimasukkan ke dalam model telah diproses secara optimal. Dengan demikian, model dapat belajar secara efektif tanpa dipengaruhi oleh outlier, dimensi data yang tinggi, atau kesalahan akibat kategori yang tidak dikenal.

### **4. Impact to Business**

Model dapat memitigasi kerugian dari pembatalan booking dari pelanggan sebesar dengan menggunakan model sebesar $1,086,151 atau sebesar 71,6% penurunan kerugian apabila model diimplemtasikan
## Dashboard

[Hotel Booking Demand Dashboard](https://public.tableau.com/app/profile/radif.ramadan/viz/DashboardRemedialFinproPurwadhika/Dashboard1?publish=yes)

## Contributors

- [Adam Tiova Budhiharjo](https://github.com)
- [Radif Ramadan](https://github.com/radifyadika)


