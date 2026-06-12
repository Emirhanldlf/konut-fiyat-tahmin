# 🏠 Konut Fiyat Tahmin Sistemi
### Ames Housing Veri Seti | CatBoost + SHAP + Gradio

[![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)](https://python.org)
[![CatBoost](https://img.shields.io/badge/Model-CatBoost-orange)](https://catboost.ai)
[![SHAP](https://img.shields.io/badge/XAI-SHAP-green)](https://shap.readthedocs.io)

---

## 📌 Proje Hakkında

Bu proje, **Ames Housing** veri setini kullanarak konut satış fiyatlarını tahmin eden uçtan uca bir makine öğrenmesi sistemidir. Proje; veri ön işleme, model karşılaştırma, hiperparametre optimizasyonu, açıklanabilir yapay zeka (XAI) analizi ve interaktif kullanıcı arayüzü aşamalarını kapsamaktadır.

**Kurs:** Python ile Yapay Zeka Uygulamaları  
**Öğrenci:** Emirhan Alim — Bursa Teknik Üniversitesi, Endüstri Mühendisliği  

---

## 📊 Model Performansı

| Metrik | Değer |
|--------|-------|
| Test R² | **0.933** |
| MAE | **~14,492 USD** |
| RMSE | **~21,935 USD** |
| MAPE | **%8.07** |

> 82 değişkenden SHAP tabanlı özellik seçimiyle **19 değişkene** indirilerek elde edilmiştir.

---

## 🔧 Kullanılan Teknolojiler

- **Veri İşleme:** Pandas, NumPy, Scikit-learn (Pipeline, ColumnTransformer)
- **Modelleme:** CatBoost, XGBoost, Gradient Boosting (10 model karşılaştırıldı)
- **Açıklanabilirlik:** SHAP (Global & Lokal analiz, Waterfall, Summary Plot)
- **Arayüz:** Gradio
- **Doğrulama:** 5-Fold Çapraz Doğrulama

---

## 🗂️ Proje Yapısı

```
housing-price-prediction/
│
├── notebook.ipynb          # Ana analiz ve modelleme notebook'u
├── app.py                  # Gradio arayüzü
├── requirements.txt        # Gerekli kütüphaneler
└── README.md
```

---

## ⚙️ Metodoloji

### 1. Veri Ön İşleme
- Eksik değer analizi; sayısal değişkenler için **medyan**, kategorik için **en sık değer** stratejisi
- Yüksek oranda eksik sütunlar elendi (Pool QC, Alley, Fence vb. — >%80 eksik)
- Hedef değişkende (SalePrice) **log1p dönüşümü** uygulandı
- Aykırı değerler için **%1–%99 Winsorization** — R² 0.885'ten 0.904'e yükseldi
- Kategorik değişkenler **One-Hot Encoding** ile dönüştürüldü

### 2. Model Karşılaştırması
10 farklı regresyon modeli **5-Fold çapraz doğrulama** ile kıyaslandı:
- Doğrusal: Linear Regression, Ridge, Lasso, ElasticNet
- Ağaç tabanlı: Decision Tree, Random Forest
- Boosting: **CatBoost ✓**, XGBoost, GBR, LightGBM

### 3. Hiperparametre Optimizasyonu
CatBoost, XGBoost ve GBR modelleri için `depth`, `learning_rate`, `l2_leaf_reg` parametreleri üzerinde arama yapıldı.

### 4. SHAP ile Model Açıklanabilirliği
- **Global analiz:** En etkili değişkenler → Overall Qual, Gr Liv Area, Total Bsmt SF
- **Lokal analiz:** Tekil tahminlerin Waterfall grafiğiyle yorumlanması
- **Özellik seçimi:** SHAP önem sıralamasıyla 82 → 19 değişken

### 5. Gradio Arayüzü
Kullanıcıdan konut özelliklerini alarak anlık fiyat tahmini üreten interaktif web uygulaması.

---

## 🚀 Kurulum ve Çalıştırma

```bash
# Depoyu klonla
git clone https://github.com/Emirhanldlf/housing-price-prediction.git
cd housing-price-prediction

# Gerekli kütüphaneleri yükle
pip install -r requirements.txt

# Gradio arayüzünü başlat
python app.py
```

---

## 📈 Öne Çıkan Sonuçlar

- **Overall Qual** (Genel Yapı Kalitesi) fiyat tahmininde en belirleyici faktör
- Winsorization ile aykırı değer temizliği model doğruluğunu **~%2 artırdı**
- SHAP özellik seçimi model karmaşıklığını **%77 azaltırken** performansı korudu
- Gradio arayüzü ile 12 farklı senaryo üzerinde gerçek zamanlı tahmin doğrulandı

---

## 👤 İletişim

**Emirhan Alim**  
Endüstri Mühendisliği, Bursa Teknik Üniversitesi  
📧 emirhanalim2004@hotmail.com  
🔗 [linkedin.com/in/emirhan-alim-11a864223](https://www.linkedin.com/in/emirhan-alim-11a864223)
