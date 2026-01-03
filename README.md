# 🦁 MaviAslan: End-to-End Credit Risk Management System

### 📊 Business Case (İş Problemi)
Bu proje, bankacılık sektöründeki "Default" (temerrüt) riskini minimize etmek amacıyla geliştirilmiştir. Hedef, kredi başvurusu yapan müşterilerin geri ödeme kapasitelerini makine öğrenmesi algoritmalarıyla analiz ederek, bankanın sermaye riskini optimize etmektir.

### 🎯 Key Objectives (Temel Hedefler)
- **Risk Tahmini:** Geçmiş veriler üzerinden kredi ödenmeme olasılığını tahmin etmek.
- **Explainability (XAI):** Karar verme sürecini SHAP değerleri ile şeffaf hale getirerek regülasyon uyumunu sağlamak.
- **Calibration:** Model skorlarını gerçek hayat olasılık frekanslarına kalibre etmek (Isotonic Regression).

### 🛠️ Tech Stack (Teknoloji Yığını)
- **Language:** Python 3.9+
- **Modeling:** Scikit-learn, XGBoost, LightGBM
- **Deployment:** FastAPI & Streamlit (Dashboard)
- **MLOps:** Git (Version Control), .gitignore for data privacy

### 📁 Project Structure (Proje Yapısı)
- `/notebooks`: EDA süreci, IV/WOE hesaplamaları ve model deneyleri.
- `/src`: Preprocessing ve Inference scriptleri.
- `/models`: Eğitilmiş ve kalibre edilmiş model dosyaları.

### 📈 Metrics (Başarı Kriterleri)
- **Primary Metric:** Gini Coefficient & Precision-Recall AUC (Dengesiz veri setine odaklı).
- **Secondary Metric:** Inference Latency (Milisaniye bazında tahmin hızı).
