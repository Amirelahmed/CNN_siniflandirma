# 🧠 CNN Tabanlı Görüntü Sınıflandırma (Taş – Mermer)

Bu proje, BLG407 Makine Öğrenmesi dersi kapsamında **kendi çektiğim görüntüler** kullanılarak geliştirilmiş bir görüntü sınıflandırma sistemidir.  
Amaç, iki sınıfı — **Taş** ve **Mermer** — yüksek doğrulukla ayırt edebilen bir CNN modeli oluşturmaktır.

Proje üç temel modelden oluşmaktadır:

- **Model1 → Transfer Learning (VGG16)**
- **Model2 → Temel CNN**
- **Model3 → Geliştirilmiş CNN + Hiperparametre Optimizasyonu + Veri Artırımı**

---

# 🗂️ 1. Veri Seti

Bu projede kullanılan veri seti tamamen tarafımdan **telefon kamerası ile çekilmiş 150 özgün görüntüden** oluşmaktadır.  
Veri seti iki sınıfa ayrılmıştır ve her sınıf için **75 adet görüntü** bulunmaktadır.

Aşağıdaki tablo veri setine ait genel bilgileri özetlemektedir:

| Özellik | Açıklama |
|--------|----------|
| **Toplam Görüntü Sayısı** | **150 adet** |
| **Taş Görselleri** | 75 görüntü |
| **Mermer Görselleri** | 75 görüntü |
| **Veri Kaynağı** | Tamamı telefon kamerası ile çekilmiştir |
| **Sınıf Sayısı** | 2 (Taş – Mermer) |
| **Görüntü Boyutu** | 128×128 piksele yeniden boyutlandırıldı |
| **Çeşitlilik** | Farklı açı, ışık ve arka plan çeşitliliği sağlandı |
| **Kullanım Şekli** | Eğitim – Doğrulama – Test olarak otomatik ayrıldı |

### 📁 Klasör Yapısı

```markdown
dataset/
├── tas/        # 75 görüntü
└── mermer/     # 75 görüntü
```


**Not:**  
Tüm görüntüler özgün olup internetten alınmamıştır. Farklı açılar ve ışık koşulları kullanılarak çeşitlilik artırılmıştır.

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

### 📈 Model1 Eğitim Grafikleri

<p align="center">
  <img src="https://github.com/Amirelahmed/CNN_siniflandirma/blob/903f43a3a41e07bfe062bc887f37fec820c3c06e/images/Model1/Accuracy.png" width="45%" />
  <img src="https://github.com/Amirelahmed/CNN_siniflandirma/blob/903f43a3a41e07bfe062bc887f37fec820c3c06e/images/Model1/Loss.png" width="45%" />
</p>
---

# 🧱 3. Model2 – Temel CNN Mimarisi

Bu model sıfırdan oluşturulmuş basit bir CNN yapısını temsil eder.

### 📌 Model2 Yapısı

| Katman | Açıklama |
|--------|----------|
| Conv2D | 32 ve 64 filtre |
| MaxPooling | 2×2 |
| Flatten | — |
| Dense | 128 nöron |
| Çıkış | Softmax |

### 📊 Model2 Sonuçları

| Metrik | Değer |
|-------|--------|
| **Test Doğruluğu** | **%96.67** |

### 📈 Model2 Eğitim Grafikleri

### 📈 Model2 Eğitim Grafikleri
<p align="center">
  <img src="https://github.com/Amirelahmed/CNN_siniflandirma/blob/903f43a3a41e07bfe062bc887f37fec820c3c06e/images/Model2/Accuracy.png" width="45%" />
  <img src="https://github.com/Amirelahmed/CNN_siniflandirma/blob/903f43a3a41e07bfe062bc887f37fec820c3c06e/images/Model2/Loss.png" width="42%" />
</p>
---

# 🚀 4. Model3 – Geliştirilmiş CNN + Veri Artırımı

Bu aşamada Model2 geliştirilmiş, model daha derin hale getirilmiş ve
veri artırımı ile genelleme kabiliyeti güçlendirilmiştir.


### 📌 Model3 Hiperparametreleri

| Parametre | Değer |
|-----------|--------|
| Filtre Sayısı | 32 → 64 → 128 |
| Batch Size | **32** |
| Dropout | 0.3 |
| Epoch | **20 (en iyi epoch: 19)** |
| Optimizasyon | Adam (LR = 0.0005) |
| Veri Artırımı | rotation=10°, width/height shift=0.05, zoom=0.1, horizontal flip=True |


### 📊 Model3 Sonuçları
| Metrik | Değer |
|-------|--------|
| **Test Doğruluğu** | **%100.00** |
| **Test Kaybı** | **~0.07** |
Model3’te yapılan hiperparametre optimizasyonları ve veri artırımı
sayesinde model performansı belirgin şekilde artmıştır.
En iyi doğrulama sonucu **Epoch 19**’da elde edilmiştir.

### 📈 Model3 Eğitim Grafikleri
<p align="center">
  <img src="https://github.com/Amirelahmed/CNN_siniflandirma/blob/f3b4c786203a8269fb75810d8bb02c749cc844fe/images/Model3/Accuracy.png" width="45%" />
  <img src="https://github.com/Amirelahmed/CNN_siniflandirma/blob/f3b4c786203a8269fb75810d8bb02c749cc844fe/images/Model3/Loss.png" width="42%" />
</p>
---

# 📈 5. Deney Karşılaştırma Tablosu

| Deney | Batch Size | Filtre Sayısı | Dropout | Epoch | Veri Artırımı | Test Accuracy | Not |
|------|------------|---------------|---------|-------|---------------|---------------|-----|
| 1 | 32 | 32-64-128 | 0.5 | 15 | Hayır | %96.67 | Model2 – Temel CNN |
| 2 | 16 | 32-64-128 | 0.3 | 20 | Evet (Yoğun) | %90.00 | Model3 – İlk Deneme |
| 3 | 32 | 32-64-128 | 0.3 | 20 | Evet (Optimize) | **%100.00** | Model3 – Optimize Edilmiş |

---

# 🧾 6. Genel Değerlendirme

| Model | Sonuç | Açıklama |
|-------|--------|-----------|
| Model1 (VGG16) | %83.33 | Transfer learning küçük veri setinde sınırlı avantaj sağlamıştır. |
| Model2 (Temel CNN) | %96.67 | Basit mimari ile yüksek performans elde edilmiştir. |
| Model3 (Geliştirilmiş CNN) | **%100.00** | Hiperparametre optimizasyonu ve veri artırımı sayesinde en iyi performans elde edilmiştir. |



➡ **Sonuç:**  
Model3, yapılan hiperparametre optimizasyonları ve veri artırımı
sayesinde Model2’ye kıyasla daha yüksek doğruluk elde etmiştir.
Bu nedenle Model3, nihai ve en başarılı model olarak seçilmiştir.

---


# 📁 7. Dosya Yapısı
```markdown
CNN_siniflandirma/
├── dataset/
│   ├── tas/
│   └── mermer/
│
├── images/                # Grafik görselleri buraya gelecek
│   ├── model1_acc.png
│   ├── model1_loss.png
│   ├── model2_acc.png
│   ├── model2_loss.png
│   ├── model3_acc.png
│   └── model3_loss.png
│
├── Model1.ipynb
├── Model2.ipynb
├── Model3.ipynb
└── README.md
```
---
# 👤 Hazırlayan
**Amir Elahmed**  
BLG407 – Makine Öğrenmesi  
CNN Görüntü Sınıflandırma Projesi



