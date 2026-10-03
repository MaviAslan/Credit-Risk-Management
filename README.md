# Credit Risk Management

**Makine Öğrenmesi ile Kredi Riski Tahmini**

## 1. Proje Hakkında

Bu projede, müşterilerin önümüzdeki iki yıl içerisinde 90 gün ve üzeri ödeme gecikmesi yaşama durumlarını tahmin etmek amacıyla makine öğrenmesi modelleri geliştirilmiştir.

Çalışma kapsamında veri analizi, eksik ve anormal değerlerin incelenmesi, özellik mühendisliği, model karşılaştırması ve karar eşiği analizi gerçekleştirilmiştir. Seçilen model, geliştirme sürecinde kullanılmayan bağımsız bir test seti üzerinde değerlendirilmiştir.

Proje, kredi riski modelleme sürecini veri hazırlığından yeni müşteri tahminine kadar Jupyter Notebook üzerinde ele almaktadır.

## 2. Veri Seti

Çalışmada Kaggle tarafından yayımlanan [Give Me Some Credit](https://www.kaggle.com/c/GiveMeSomeCredit) veri seti kullanılmıştır.

Veri seti, müşterilerin demografik bilgilerini, gelir durumlarını, mevcut kredi yükümlülüklerini ve geçmiş ödeme gecikmelerini içermektedir.

Hedef değişken `SeriousDlqin2yrs`, müşterinin takip eden iki yıl içerisinde 90 gün veya daha fazla ödeme gecikmesi yaşayıp yaşamadığını göstermektedir.

150.000 gözlem içeren veri seti, hedef değişkenin sınıf dağılımı korunarak ikiye ayrılmıştır:

- Eğitim seti: %80 (120.000 gözlem)
- Test seti: %20 (30.000 gözlem)

Test seti, model geliştirme ve karar eşiği belirleme süreçlerinden ayrı tutulmuştur.

## 3. Çalışma Aşamaları

### 3.1. Keşifsel Veri Analizi

Değişkenlerin dağılımları, eksik değerleri, aykırı gözlemleri ve hedef değişkenle ilişkileri incelenmiştir.

Özellikle ödeme gecikmesi değişkenlerindeki sistemsel anormallikler, kredi kullanım oranındaki uç değerler ve gelir değişkenindeki eksik gözlemler değerlendirilmiştir.

### 3.2. Veri Ön İşleme ve Özellik Mühendisliği

Veri incelemesi sonucunda belirlenen ön işleme kararları doğrultusunda eksik değer ikamesi, anomali yönetimi, gösterge değişkenleri ve yeni özellikler oluşturulmuştur.

Özellik seçiminde Information Value (IV), korelasyon analizi ve Variance Inflation Factor (VIF) sonuçlarından yararlanılmıştır.

Ön işleme adımları, çapraz doğrulama sırasında veri sızıntısını önlemek amacıyla Scikit-learn Pipeline yapısına dahil edilmiştir.

### 3.3. Modelleme ve Karşılaştırma

Dört sınıflandırma algoritması değerlendirilmiştir:

- Logistic Regression
- Random Forest
- XGBoost
- LightGBM

Model karşılaştırmaları, 5-Fold Stratified Cross-Validation ve hiperparametre optimizasyonu kullanılarak gerçekleştirilmiştir.

Temel değerlendirme metrikleri ROC-AUC, Gini ve Average Precision olarak belirlenmiş; Recall, Precision ve F1-Score tamamlayıcı metrikler olarak incelenmiştir.

LightGBM daha yüksek çapraz doğrulama performansı göstermesine rağmen Logistic Regression, modelin yorumlanabilirliği dikkate alınarak seçilmiştir.

### 3.4. Karar Eşiği Analizi

Seçilen modelin eğitim verisi üzerindeki çapraz doğrulama tahminleri kullanılarak farklı karar eşikleri incelenmiştir.

0.25, 0.50 ve 0.75 eşiklerinde yanlış pozitif ve yanlış negatif sınıflandırmalar karşılaştırılmıştır. Çalışmanın devamında 0.50 çalışma eşiği kullanılmıştır.

### 3.5. Nihai Test Değerlendirmesi

Seçilen model, ön işleme adımları ve karar eşiği değiştirilmeden başlangıçta ayrılan 30.000 gözlemden oluşan test setinde değerlendirilmiştir.

| Metrik | Nihai test sonucu |
|---|---:|
| ROC-AUC | 0.8606 |
| Gini | 0.7212 |
| Average Precision | 0.3783 |
| Recall | %74.71 |
| Precision | %22.17 |
| F1-Score | 0.3419 |

0.50 karar eşiğinde model, test setindeki 2.005 gerçek riskli müşterinin 1.498'ini doğru sınıflandırmış, 507'sini ise tespit edememiştir. Riskli olmayan 27.995 müşterinin 5.259'u yanlışlıkla riskli olarak sınıflandırılmıştır.

Test sonuçları, çapraz doğrulama ortalamalarıyla karşılaştırıldığında belirgin bir performans kaybı göstermemiştir.

### 3.6. Tek Müşteri Risk Tahmini

Eğitilmiş Pipeline kullanılarak temsili bir müşterinin ham bilgileri üzerinden risk skoru ve sınıf tahmini üretilmiştir.

Modelin ürettiği skor, kalibre edilmiş temerrüt olasılığı olarak değerlendirilmemektedir.

## 4. Kullanılan Teknolojiler

- Python
- pandas ve NumPy
- Matplotlib ve Seaborn
- Scikit-learn
- Statsmodels
- XGBoost ve LightGBM
- Jupyter Notebook

## 5. Proje Yapısı

```text
Credit-Risk-Management/
│
├── notebooks/
│   └── Credit_Risk_Management.ipynb
│
├── data/
│   └── raw/
│
├── README.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

Ham veri dosyaları GitHub deposuna dahil edilmemiştir. Veri seti Kaggle üzerinden indirilebilir.

## 6. Projenin Çalıştırılması

1. Depoyu bilgisayarınıza indirin.
2. Projenin ana dizininde bir terminal açarak gerekli Python kütüphanelerini yükleyin.
    pip install -r requirements.txt
3. Give Me Some Credit veri setini Kaggle üzerinden indirin.
4. `cs-training.csv` dosyasını `data/raw/` klasörüne yerleştirin.
5. `notebooks/Credit_Risk_Management.ipynb` dosyasını Jupyter Notebook üzerinden açarak hücreleri sırasıyla çalıştırın.

## 7. Sınırlılıklar ve Geliştirme Alanları

Çalışmada kullanılan model, sınıf dengesizliğini dikkate alan ağırlıklandırma yöntemiyle eğitilmiştir. Bu nedenle model skorları doğrudan gerçek temerrüt olasılığı olarak yorumlanmamalıdır.

0.50 karar eşiği, farklı senaryoları değerlendirmek amacıyla belirlenen bir çalışma eşiğidir. Gerçek bir uygulamada karar eşiğinin kurumun risk iştahı ve yanlış sınıflandırma maliyetleri dikkate alınarak belirlenmesi gerekir.

İlerleyen çalışmalarda olasılık kalibrasyonu, dönem dışı doğrulama ve model performansının zaman içerisindeki değişiminin izlenmesi ele alınabilir.

Bu proje, veri bilimi ve kredi riski modelleme yöntemlerini uygulamak amacıyla hazırlanmış bir portföy çalışmasıdır. Doğrudan kredi onay veya ret süreçlerinde kullanılmak üzere geliştirilmemiştir.
