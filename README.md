# Brain Tumor Classification with CNN and Transfer Learning

Bu proje, beyin MR görüntülerinde tümör var/yok durumunu tespit etmek amacıyla
derin öğrenme tabanlı sınıflandırma modelleri geliştirmeyi ve karşılaştırmayı amaçlamaktadır.
Çalışmada sıfırdan eğitilen bir CNN modeli ile transfer öğrenme tabanlı ResNet50 ve
DenseNet121 modelleri karşılaştırılmıştır. Ayrıca model kararlarının açıklanabilirliğini
artırmak için Grad-CAM yöntemi kullanılmıştır.

---

## 1. Problem Tanımı
Beyin tümörlerinin erken ve doğru tespiti klinik açıdan büyük önem taşımaktadır.
Bu projede amaç, beyin MR görüntülerini kullanarak ikili sınıflandırma
(Tümör / Tümör Yok) problemi için etkili bir derin öğrenme yaklaşımı geliştirmek
ve farklı model mimarilerinin performansını karşılaştırmaktır.

---

## 2. Kullanılan Veri Seti ve Ön İşleme Adımları
- **Veri Seti:** Beyin MR görüntülerinden oluşan ikili sınıflandırma veri seti  
  (Tumor / No Tumor).
- **Veri Bölme Oranları:**
  - %70 Eğitim (Train)
  - %15 Doğrulama (Validation)
  - %15 Test
- **Ön İşleme:**
  - Scratch CNN modeli için: piksel normalizasyonu (`rescale = 1/255`)
  - Transfer learning modelleri için: backbone’a özgü `preprocess_input`
- **Veri Artırma (Sadece eğitim seti):**
  - Döndürme (rotation)
  - Yatay/dikey kaydırma
  - Yakınlaştırma (zoom)
  - Yatay çevirme (horizontal flip)

---

## 3. Model Mimarisi ve Yaklaşımın Gerekçesi
Bu projede üç farklı model yaklaşımı kullanılmıştır:

1. **Scratch CNN**
   - Sıfırdan eğitilen konvolüsyonel sinir ağı
   - Özellik çıkarımı ve sınıflandırma katmanları birlikte öğrenilmiştir

2. **ResNet50 (Transfer Learning)**
   - ImageNet üzerinde önceden eğitilmiş model
   - Özellik çıkarıcı katmanlar dondurulmuştur
   - Ortak sınıflandırıcı başlık (head) kullanılmıştır

3. **DenseNet121 (Transfer Learning)**
   - ImageNet üzerinde önceden eğitilmiş model
   - ResNet50 ile aynı sınıflandırıcı başlık kullanılarak adil karşılaştırma sağlanmıştır

> **Not:** Transfer learning modellerinde sınıflandırıcı başlık  
> (Global Average Pooling + Dense + Dropout) scratch CNN modeli ile aynı tutulmuştur.
> Böylece karşılaştırma yalnızca feature extractor mimarilerinin etkisine dayanmaktadır.

---

## 4. Çalıştırma Talimatları

### 4.1 Gerekli Bağımlılıklar

```bash
pip install -r requirements.txt

### 4.2 Model Eğitimi

Tüm modeller Jupyter Notebook ortamında eğitilmiştir.

Kullanılan notebook:
- `notebooks/derin_ogrenme_final.ipynb`

Notebook içerisinde:
- Scratch CNN eğitimi
- ResNet50 transfer learning eğitimi
- DenseNet121 transfer learning eğitimi  
adım adım yer almaktadır.

---

### 4.3 Model Değerlendirme

Modeller test seti üzerinde aşağıdaki metriklerle değerlendirilmiştir:
- Accuracy
- Precision
- Recall
- F1-score
- AUC

Değerlendirme adımları notebook içerisinde detaylı olarak sunulmuştur.

---

### 4.4 Grad-CAM Görselleştirme

Model kararlarının açıklanabilirliğini artırmak amacıyla Grad-CAM yöntemi kullanılmıştır.

Grad-CAM çıktıları:
- Orijinal test görüntüsü
- Isı haritası (heatmap)
- Görüntü + ısı haritası bindirmesi

şeklinde notebook içerisinde yer almaktadır.

---

## 5. Model Çıktıları

### 5.1 Nicel Metrikler
- Accuracy
- Precision
- Recall
- F1-score
- AUC

### 5.2 Örnek Test Çıktıları
- Test verisi üzerindeki model tahminleri
- Grad-CAM görselleri

### 5.3 Eğitim Süreci Grafikler
- Eğitim ve doğrulama loss eğrileri
- Eğitim ve doğrulama accuracy eğrileri

---

## 6. Sonuçlar

- Transfer learning modelleri, scratch CNN modeline kıyasla daha yüksek doğruluk
  ve daha iyi genelleme performansı göstermiştir.
- DenseNet121 modeli genel olarak en dengeli sonuçları sunmuştur.
- Grad-CAM sonuçları, modellerin tümör bölgelerine anlamlı şekilde odaklandığını
  göstermektedir.

---

## 7. Proje Sunumu

Projenin nihai sunum dosyası `presentation/` klasörü altında PDF formatında yer almaktadır.
Sunumda anlatılan tüm deneyler ve sonuçlar, bu GitHub deposundaki notebook ve
çıktılar ile birebir örtüşmektedir.



Projenin nihai sunum dosyası presentation/ klasörü altında PDF formatında yer almaktadır.
Sunumda anlatılan tüm deneyler ve sonuçlar, bu GitHub deposundaki notebook ve
çıktılar ile birebir örtüşmektedir.
