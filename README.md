# Maaş Tahmini Karar Destek Sistemi

Bu proje, çalışanların performans skorları, deneyimleri, eğitim geçmişleri ve çalışma saatlerini analiz ederek, her bir çalışan için **"adil ve ideal maaş"** seviyesini tahmin eden bir makine öğrenmesi (Regresyon) çalışmasıdır.

##  Projenin Amacı

Şirket içi ücret dengesizliklerini gidermek ve veri odaklı bir zam politikası oluşturmak için geliştirilmiştir. Sistem şu temel sorulara yanıt verir:
- "Bu çalışan, mevcut performansı ve yetkinliklerine göre ne kadar maaş almalı?"
- "Hangi çalışanlar piyasa veya şirket ortalamasının altında kalarak 'kaybedilme riski' taşıyor?"
- "Yeni bir işe alımda adayın niteliklerine göre teklif edilmesi gereken ideal ücret nedir?"

##  Karar Destek Mekanizması Nasıl Çalışıyor?

1. **Veri Analizi ve Temizlik (LOF):** Maaş verilerindeki hatalı girişler veya uç değerler temizlenerek modelin tarafsız bir ücret skalası öğrenmesi sağlanır.
2. **Ücret Tahminleme Motoru:** Regresyon algoritmaları; performans puanı, eğitim yılı ve kıdem gibi faktörlerin maaş üzerindeki ağırlığını hesaplar.
3. **Sapma Analizi:** Modelin tahmin ettiği "İdeal Maaş" ile "Gerçek Maaş" karşılaştırılır. 
   - Gerçek Maaş < Tahmin edilen Maaş: **Düşük Ücret (Zam Önceliği)**
   - Gerçek Maaş ≈ Tahmin edilen Maaş: **Dengeli Ücret**

##  Veri Seti ve Değişkenler (`Calisan_Veri.csv`)

Model, aşağıdaki parametreleri girdi olarak kullanarak **Yıllık Gelir** tahmininde bulunur:

* **Bağımsız Değişkenler (Girdiler):**
    - `Performans_Skoru`: Çalışanın ölçümlenen başarı puanı.
    - `Calisma_Yili`: Toplam iş tecrübesi.
    - `Egitim_Yili`: Tamamlanan eğitim süresi.
    - `Haftalik_Calisma_Saati`: Mesai yoğunluğu.
    - `Yonetici_Puani`: Yöneticiden alınan sübjektif değerlendirme.
* **Hedef Değişken (Çıktı):**
    - `Yillik_Gelir_TL`: Tahmin edilen ideal yıllık brüt ücret.

##  Teknik Başarı ve Optimizasyon

9 farklı regresyon modeli (XGBoost, CatBoost, Random Forest vb.) arasından en düşük hata payına sahip olan algoritma seçilmiştir. `RandomizedSearchCV` ile yapılan optimizasyon sayesinde, maaş tahminlerinde yüksek doğruluk (R²) oranlarına ulaşılmıştır.

##  Kullanım Senaryoları

* **Dönemsel Zam Planlaması:** Bütçenin, performans ve hak edilen maaş dengesine göre dağıtılması.
* **Ücret Adaleti Denetimi:** Aynı işi yapan ve benzer yetkinlikteki çalışanlar arasındaki ücret farklarının tespiti.
* **Bütçe Projeksiyonu:** Gelecek dönem personel maliyetlerinin hesaplanması.

##  Nasıl Çalıştırılır?

Bu projeyi kendi yerel ortamınızda test etmek ve analizleri incelemek için aşağıdaki adımları izleyebilirsiniz:

1. Hazırlık
Öncelikle projeyi bilgisayarınıza indirin (Klonlayın) ve proje dizinine gidin

   ```bash
   ```bash
    git clone [https://github.com/yakubaltikardes/MaasTahminKDS.git](https://github.com/yakubaltikardes/MaasTahminKDS.git)
    cd MaasTahminKDS

2. Gerekli Kütüphanelerin Kurulumu
    ```bash
    pip install numpy pandas seaborn matplotlib scikit-learn xgboost lightgbm catboost

3. Analizi Başlatma
    ```bash
    jupyter notebook```

Açılan arayüzden Algoritma.ipynb dosyasını seçerek tüm hücreleri sırasıyla çalıştırabilirsiniz.

Önemli Not: Calisan_Veri.csv dosyasının, notebook dosyası ile aynı dizinde bulunduğundan emin olun. Model, veri setini bu dizinden otomatik olarak okuyacak şekilde yapılandırılmıştır.
