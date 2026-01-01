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
 **Veri Seti:** Beyin MR görüntülerinden oluşan ikili sınıflandırma veri seti  
  (Tumor / No Tumor).
  
**Veri Bölme Oranları:**
  - %70 Eğitim (Train)
  - %15 Doğrulama (Validation)
  - %15 Test
  
 **Ön İşleme:**
  - Scratch CNN modeli için: piksel normalizasyonu (`rescale = 1/255`)
  - Transfer learning modelleri için: backbone’a özgü `preprocess_input`
    
**Veri Artırma (Sadece eğitim seti):**
  - Döndürme (rotation)
  - Yatay/dikey kaydırma
  - Yakınlaştırma (zoom)
  - Yatay çevirme (horizontal flip)

---

## 3. Model Mimarisi ve Yaklaşımın Gerekçesi
Bu projede üç farklı model yaklaşımı kullanılmıştır:

**Scratch CNN**
   - Sıfırdan eğitilen konvolüsyonel sinir ağı
   - Özellik çıkarımı ve sınıflandırma katmanları birlikte öğrenilmiştir

**ResNet50 (Transfer Learning)**
   - ImageNet üzerinde önceden eğitilmiş model
   - Özellik çıkarıcı katmanlar dondurulmuştur
   - Ortak sınıflandırıcı başlık (head) kullanılmıştır

**DenseNet121 (Transfer Learning)**
   - ImageNet üzerinde önceden eğitilmiş model
   - ResNet50 ile aynı sınıflandırıcı başlık kullanılarak adil karşılaştırma sağlanmıştır

**Not:** Transfer learning modellerinde sınıflandırıcı başlık (Global Average Pooling + Dense + Dropout) scratch CNN modeli ile aynı tutulmuştur.
Böylece karşılaştırma yalnızca feature extractor mimarilerinin etkisine dayanmaktadır.

---

## 4. Çalıştırma Talimatları

Bu projede modellerin eğitimi ve çalıştırılması için aşağıdaki adımlar izlenmiştir:

1. **Gerekli Bağımlılıklar**

- Projede kullanılan tüm Python paketleri `requirements.txt` dosyasında tanımlanmıştır.
- Ortam kurulumu aşağıdaki komut ile yapılmaktadır:

pip install -r requirements.txt

2. **Çalışma Ortamı**

- Tüm modeller Jupyter Notebook ortamında eğitilmiştir.
- Kullanılan ana notebook dosyası:

notebooks/derin_ogrenme_final.ipynb

3. **Eğitim Süreci**

- Scratch CNN eğitimi
- ResNet50 transfer learning eğitimi
- DenseNet121 transfer learning eğitimi

Eğitim adımları notebook içerisinde hücre bazlı olarak detaylı şekilde yer almaktadır.


---

## 5. Model Çıktıları

Bu bölümde eğitilen modellerden elde edilen nicel sonuçlar ve görsel çıktılar sunulmaktadır.

1. **Nicel Metrikler**

- Accuracy  
- Precision  
- Recall  
- F1-score  
- AUC  

Bu metrikler kullanılarak modellerin performansı karşılaştırılmıştır.

2. **Örnek Test Çıktıları**

- Test verisi üzerindeki model tahminleri  
- Grad-CAM görselleri  

Bu çıktılar, model davranışlarının görsel olarak analiz edilmesini sağlamaktadır.

3. **Eğitim Süreci Grafikler**

- Eğitim ve doğrulama loss eğrileri  
- Eğitim ve doğrulama accuracy eğrileri  

Bu grafikler eğitim sürecinin kararlılığını değerlendirmek amacıyla kullanılmıştır.

---

## 6. Sonuçlar

Elde edilen deneysel sonuçlara göre transfer learning tabanlı modeller, scratch CNN
modeline kıyasla daha yüksek doğruluk ve daha iyi genelleme performansı göstermiştir.
Özellikle DenseNet121 modeli, farklı metrikler açısından en dengeli sonuçları sunmuştur.
Grad-CAM analizleri, modellerin karar verirken tümör bölgelerine anlamlı şekilde
odaklandığını göstermektedir.

---

## 7. Proje Sunumu

Projenin nihai sunum dosyası `presentation/` klasörü altında PDF formatında yer almaktadır.
Sunumda anlatılan tüm deneyler ve elde edilen sonuçlar, bu GitHub deposunda bulunan
notebook dosyaları ve model çıktıları ile birebir örtüşmektedir.

