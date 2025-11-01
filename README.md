# Housing Prices Competition for Kaggle Learn Users

Bu repo, **[Housing Prices Competition for Kaggle Learn Users](https://www.kaggle.com/competitions/home-data-for-ml-course)** yarışması için hazırladığım çözümü içermektedir.

Bu yarışmada amaç, çeşitli sayısal ve kategorik değişkenleri kullanarak evlerin satış fiyatlarını tahmin etmektir.  
Bu proje; veri temizleme, özellik mühendisliği, makine öğrenmesi modeli kurma ve değerlendirme aşamalarını **Scikit-learn Pipeline** ve **XGBoost** kullanarak adım adım göstermektedir.

---

##  Proje Özeti

- **Yarışma:** [Kaggle Housing Prices (Learn Users)](https://www.kaggle.com/competitions/home-data-for-ml-course)  
- **Amaç:** Ev fiyatlarını, veri setindeki farklı sayısal ve kategorik değişkenler yardımıyla tahmin etmek.  
- **Yaklaşım:**
  - Eksik değerlerin ve özel durumların yönetimi için özel bir `HouseRules` sınıfı
  - Çarpıklığı yüksek olan sayısal değişkenlere log dönüşümü uygulanması
  - Kategorik değişkenler için **OrdinalEncoder** ve **OneHotEncoder** kullanımı
  - **GridSearchCV** ile model hiperparametre optimizasyonu
  - Model olarak **XGBoost Regressor**

---

##  Model Pipeline Yapısı

1. **Özel Dönüştürücü (`HouseRules`)**  
   - Var/yok türündeki kategorik değişkenleri `"None"` ile doldurur.  
   - Garajı veya bodrumu olmayan evlerde ilgili sayısal değişkenleri **0** yapar.  
   - `LotFrontage` değişkenindeki eksikleri mahalleye göre median değerle doldurur.  
   - `MSSubClass` değişkenini string’e çevirerek kategorik hale getirir.

2. **ColumnTransformer**  
   - **Numeric (log uygulanacaklar)** → Median ile doldurma + Log dönüşümü  
   - **Numeric (log uygulanmayacaklar)** → Median ile doldurma  
   - **Ordinal değişkenler** → OrdinalEncoder  
   - **Nominal değişkenler** → OneHotEncoder  

3. **Model:** `XGBRegressor`  
   - Hiperparametre ayarı GridSearchCV ile yapılmıştır.

---

## 🧾 Dosya Yapısı

| Dosya / Klasör | Açıklama |
|----------------|----------|
| `notebooks/house_prices_pipeline_final.ipynb` | Tüm veri işleme, modelleme ve değerlendirme adımlarını içeren notebook |
---
