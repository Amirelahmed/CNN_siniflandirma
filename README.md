# 📌 CNN Sınıflandırma Projesi

Bu proje, Makine Öğrenmesi dersi kapsamında **kendi çektiğim görüntüler** ile saat ve fare nesnelerini sınıflandırmak amacıyla geliştirilmiştir.  
Proje üç farklı modelden oluşmaktadır:  
- **Model1:** Transfer Learning (VGG16)  
- **Model2:** Temel CNN  
- **Model3:** Hiperparametre Optimizasyonu + Veri Artırımı  

---

# 🗂️ 1. Veri Seti

Aşağıdaki tablo proje verisetine ait genel bilgileri özetlemektedir:

| Özellik | Açıklama |
|--------|----------|
| **Veri Kaynağı** | Tamamen telefon kamerası ile tarafımdan çekildi |
| **Sınıf Sayısı** | 2 (Saat – Fare) |
| **Görüntü Adedi** | Her sınıf için ≥ 50 görsel |
| **Görüntü Boyutu** | 128×128 piksele yeniden boyutlandırıldı |
| **Çeşitlilik** | Farklı açılar, ışık koşulları, arka planlar |
| **Kullanım** | Eğitim – Doğrulama – Test |

📁 **Klasör Yapısı**


---

# ⚙️ 2. Model1 (Transfer Learning – VGG16)

Transfer learning kullanılarak VGG16 ağırlıkları üzerine ince ayar yapılmıştır.

### 📊 Model1 Özeti

| Özellik | Değer |
|--------|-------|
| Kullanılan Mimari | VGG16 (ImageNet ağırlıklı) |
| Öğrenme Yöntemi | Fine-Tuning |
| Epoch | 6 |
| Aktivasyon | ReLU + Softmax |
| Optimizasyon | Adam |
| Kullanılan Kütüphane | Keras |

### 🔍 Model1 Sonuçları

| Metrik | Sonuç |
|-------|--------|
| **Eğitim Doğruluğu** | %60–68 |
| **Doğrulama Doğruluğu** | %90 |
| **Test Doğruluğu** | %90 |
| **Gözlem** | Aşırı öğrenme yok, güçlü genel performans |

---

# 🧱 3. Model2 (Temel CNN Mimarisi)

Bu model, CIFAR-10 tarzı basit bir CNN yapısıdır.

### 📊 Model2 Yapısı

| Katman | Açıklama |
|--------|----------|
| Conv2D | 32 ve 64 filtre |
| MaxPooling | 2×2 |
| Flatten | — |
| Dense | 128 nöron |
| Çıkış | Softmax |

### 🔍 Model2 Sonuçları

| Metrik | Sonuç |
|-------|--------|
| **Test Doğruluğu** | Orta seviye |
| **Gözlem** | Basit mimari → düşük genel performans |

---

# 🚀 4. Model3 (Geliştirilmiş CNN + Augmentation)

Bu aşamada Model2 geliştirilmiş, hiperparametre optimizasyonu uygulanmış ve veri artırımı eklenmiştir.

### ⚙️ Model3 Hiperparametreleri

| Parametre | Değer |
|-----------|--------|
| Filtre Sayısı | 32 → 64 → 128 |
| Batch Size | 16 |
| Dropout | 0.4 |
| Epoch | 20 |
| Öğrenme Oranı | 0.0005 |
| Veri Artırımı | rotation=15°, shift=0.1, flip=True |

### 🔍 Model3 Sonuçları

| Metrik | Sonuç |
|-------|--------|
| **Test Doğruluğu** | **%100** |
| **Gözlem** | En iyi performans → Derinlik + Augmentation etkili |

---

# 📊 5. Deney Karşılaştırma Tablosu

Aşağıdaki tablo Model2 ve Model3 arasında yapılan deneyleri özetlemektedir:

| Deney No | Batch Size | Filtre Sayısı | Dropout | Epoch | Veri Artırımı | Test Accuracy | Notlar |
|---------|-------------|----------------|----------|--------|----------------|----------------|--------|
| **1** | 32 | 32-64-128 | 0.5 | 15 | Hayır | %93.33 | Temel CNN (Model2) |
| **2** | 16 | 32-64-128 (Derin mimari) | 0.4 | 20 | Evet | **%100** | İyileştirilmiş CNN + Augmentation (Model3) |

---

# 🧾 6. Sonuç ve Değerlendirme

| Model | Sonuç | Açıklama |
|-------|--------|-----------|
| **Model1 (VGG16)** | %90 | Transfer learning → güçlü başlangıç |
| **Model2 (Temel CNN)** | Orta seviye | Sığ mimari → düşük başarı |
| **Model3 (Geliştirilmiş CNN)** | **%100** | Hiperparametre + veri artırımı → en iyi performans |

**Genel Sonuç →** Model3 en başarılı modeldir.

---

# 📁 7. Proje Dosyaları
dataset/
saat/
fare/

| Dosya | Açıklama |
|-------|----------|
| **Model1.ipynb** | Transfer Learning modeli |
| **Model2.ipynb** | Temel CNN modeli |
| **Model3.ipynb** | Geliştirilmiş CNN modeli |
| **dataset/** | Saat & Fare görüntüleri |
| **README.md** | Proje dökümantasyonu |

---

# 👤 Hazırlayan  
**Ad Soyad:** Amir Elahmed  
**Ders:** BLG407 – Makine Öğrenmesi  
**Proje:** CNN Görüntü Sınıflandırma Sistemi  

---



