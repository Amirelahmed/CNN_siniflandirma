# 🧠 CNN Tabanlı Görüntü Sınıflandırma (Taş – Mermer)

Bu proje, BLG407 Makine Öğrenmesi dersi kapsamında **kendi çektiğim görüntüler** kullanılarak geliştirilmiş bir ikili sınıflandırma sistemidir.  
Amaç, taş ve mermer nesnelerini ayırt edebilen bir CNN modeli oluşturmaktır.

Proje üç aşamadan oluşmaktadır:

- **Model1 → Transfer Learning (VGG16)**
- **Model2 → Temel CNN**
- **Model3 → Geliştirilmiş CNN + Hiperparametre Optimizasyonu + Veri Artırımı**

---

# 📂 1. Veri Seti Bilgileri

| Özellik | Açıklama |
|--------|----------|
| **Sınıflar** | Taş – Mermer |
| **Veri Kaynağı** | Tümü telefon kamerasıyla tarafımdan çekildi |
| **Her sınıf için görsel sayısı** | ≥ 50 |
| **Toplam veri** | ≥ 100 görüntü |
| **Görüntü Boyutu** | 128×128 piksel |
| **Çeşitlilik** | Farklı açı, ışık, arka plan |
| **Klasör Yapısı** | dataset/taş, dataset/mermer |

---

# ⚙️ 2. Model1 – Transfer Learning (VGG16)

Bu aşamada ImageNet üzerinde eğitilmiş **VGG16** modeli kullanılmış, üst katmanları çıkarılarak kendi veri setime göre ince ayar (fine-tuning) yapılmıştır.

### 📌 Model1 Özellikleri

| Parametre | Değer |
|-----------|--------|
| Mimari | VGG16 (ImageNet ağırlıklı) |
| Eğitim Yöntemi | Fine-Tuning |
| Epoch | 10 |
| Aktivasyon | ReLU + Softmax |
| Optimizasyon | Adam |
| Kütüphane | Keras |

### 📊 Model1 Sonuçları

| Metrik | Değer |
|-------|--------|
| **Eğitim Doğruluğu** | ~%75–79 |
| **Doğrulama Doğruluğu** | **%83.33** |
| **Test Doğruluğu** | **%83.33** |
| **Gözlem** | Transfer learning iyi başlangıç sağladı ancak veri seti küçük olduğu için tam genelleşemedi. |

---

# 🧱 3. Model2 – Temel CNN Mimarisi

Bu model sıfırdan oluşturulmuş basit bir CNN mimarisidir.

### 📌 Model2 Yapısı

| Katman | Detay |
|--------|--------|
| Conv2D | 32, 64 filtre |
| MaxPooling | 2×2 |
| Flatten | — |
| Dense | 128 nöron |
| Çıkış | 2 sınıf – Softmax |

### 📊 Model2 Sonuçları

| Metrik | Değer |
|-------|--------|
| **Test Doğruluğu** | **%96.67** |
| **Doğrulama Başarısı** | Yüksek ve stabil |
| **Gözlem** | Küçük veri setinde temel CNN beklenenden yüksek performans gösterdi. |

---

# 🚀 4. Model3 – Geliştirilmiş CNN + Veri Artırımı

Bu aşamada Model2 geliştirilmiş, model daha derin hale getirilmiş, veri artırımı eklenmiş ve hiperparametreler optimize edilmiştir.

### 📌 Model3 Hiperparametreleri

| Parametre | Değer |
|-----------|--------|
| Filtre Sayısı | 64 → 128 → 256 → 256 |
| Batch Size | 8 |
| Dropout | 0.3 (ek olarak 0.2 + 0.1 kombinasyon denendi) |
| Epoch | 15 |
| Öğrenme Oranı | 0.0005 |
| Veri Artırımı | rotation=15°, shift=0.1, flip=True |

### 📊 Model3 Sonuçları

| Metrik | Değer |
|-------|--------|
| **Test Doğruluğu** | **%100** |
| **Test Kaybı** | 0.01 |
| **Gözlem** | En yüksek performans: Veri artırımı + derin mimari etkisi belirgin. |

---

# 📈 5. Deney Karşılaştırma Tablosu

| Deney | Batch Size | Filtre Sayısı | Dropout | Epoch | Veri Artırımı | Test Accuracy | Not |
|------|-------------|----------------|----------|-------|----------------|----------------|-----|
| **1** | 32 | 32-64-128 | 0.5 | 15 | Hayır | **%96.67** | Model2 – Temel CNN |
| **2** | 8 | 64-128-256-256 | 0.2 + 0.1 | 15 | Evet | **%100** | Model3 – Geliştirilmiş CNN |

---

# 🧾 6. Genel Değerlendirme

| Model | Performans | Açıklama |
|-------|------------|-----------|
| **Model1 (VGG16)** | %83.33 | Transfer learning başlangıç için güçlü fakat aşırı uyum göze çarpıyor. |
| **Model2 (Temel CNN)** | %96.67 | Basit mimari olmasına rağmen veri setine iyi uyum sağladı. |
| **Model3 (Geliştirilmiş CNN)** | **%100** | Daha derin yapı + augmentation → En iyi sonuç |

➡ **Sonuç: Model3 açık ara en başarılı modeldir.**

---

# 📁 7. Dosya Yapısı
CNN_siniflandirma/
│
├── dataset/
│ ├── tas/
│ └── mermer/
│
├── Model1.ipynb
├── Model2.ipynb
├── Model3.ipynb
├── README.md


---

# 👤 Hazırlayan
**Amir Elahmed**  
BLG407 – Makine Öğrenmesi  
CNN Görüntü Sınıflandırma Projesi

