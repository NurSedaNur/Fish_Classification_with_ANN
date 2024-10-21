# Fish Classification with ANN

Bu model, balık türlerini sınıflandırmak için TensorFlow ve Keras kütüphaneleri kullanılarak oluşturulmuş bir derin öğrenme modelidir.

## 1. Veri Setinin Hazırlanması
- Veri seti, balık türlerinin resimlerinin bulunduğu klasörlerden alınmaktadır.
- Her bir balık türü için, resim dosyalarının dosya yolları ve etiketleri (fish_type) listelenmektedir. 
- Veri setini dinamik olarak keşfediyor ve etiketleri otomatik olarak alıyor. Bu, veri setinin genişliği açısından esnekliği artırıyor.

## 2. Veri Setinin İncelenmesi
- Pandas kullanılarak dosya yolları ve etiketlerle bir DataFrame oluşturulmuştur. Bu şekilde, veri setinin genel görünümü ve boyutu kolayca incelenmiştir.

## 3. Veri Setinin Ayrılması
- `train_test_split` fonksiyonu ile veri seti eğitim ve test setlerine ayrılmıştır. 
- `stratify` parametresi, her iki setin de sınıf dengesini korumasını sağlar. Veri seti %20'ye %80 şeklinde ayrılmıştır. Bu şekilde sınıf dengesini koruyarak, modelin öğrenme sürecini iyileştirebilir.

## 4. Veri Artırma (Data Augmentation)
- Eğitim verilerini artırmak için `ImageDataGenerator` kullanılmıştır. Bu, modelin genelleme yeteneğini artırabilir. 
- Veri artırma, aşırı öğrenmeyi azaltabilir ve modelin farklı koşullara daha iyi adapte olmasını sağlar.

## 5. Modelin Oluşturulması
- Model, `Sequential` yapısı kullanılarak oluşturulmuştur. 
- İlk katman, girdi şekli olarak 150x150 px boyutunda ve 3 kanallı (RGB) görüntü alır. 
- İki `Dense` katmanı ve `Dropout` katmanı ile birlikte çalışır. 

> **Not:** Dropout, derin öğrenme modellerinde aşırı öğrenmeyi önlemek için yaygın bir düzenleme (regularization) tekniğidir. Eğitim sırasında belirli bir oranda rastgele olarak bazı nöronların "devre dışı bırakılması" anlamına gelir.

## 6. Modelin Eğitimi
- Model, eğitim verileri ile 10 epoch boyunca eğitilmektedir. 
- `validation_data` parametresi, modelin doğrulama seti üzerindeki performansını izlemek için kullanılır.

## 7. Sonuçların Yorumlanması
- Modelin eğitim sırasında elde ettiği doğruluk oldukça düşüktür (yaklaşık %10 civarı).
- Eğitim ve doğrulama kaybı değerleri birbirine oldukça yakın ve yüksektir, bu da modelin öğrenme kapasitesinin yeterince iyi olmadığını göstermektedir.

### 7.1. Loss ve Accuracy Fonksiyonları
#### 7.1.1. Eğitim ve Doğrulama Kaybı (Loss)
- **Eğitim Kaybı (Training Loss):** Eğitimin her epoch'u boyunca kaybın nasıl değiştiğini gösterir.
- **Doğrulama Kaybı (Validation Loss):** Modelin doğrulama verisi üzerindeki kaybını gösterir.

> **Analiz:** Eğitim kaybı sürekli olarak düşüyorsa, modelin eğitim verisi üzerinde iyi bir öğrenme süreci geçirdiğini gösterir. Ancak doğrulama kaybı belirli bir noktadan sonra artıyorsa, aşırı öğrenme (overfitting) sorunu olduğunun bir işareti olabilir.

#### 7.1.2. Eğitim ve Doğrulama Doğruluğu (Accuracy)
- **Eğitim Doğruluğu (Training Accuracy):** Eğitim setindeki doğruluğu gösterir.
- **Doğrulama Doğruluğu (Validation Accuracy):** Doğrulama setindeki doğruluğu gösterir.

### 7.2. Classification Report (Sınıflandırma Raporu)
- **Precision, Recall ve F1-Score:** Tüm sınıflar için precision ve recall değerleri sıfır olan birçok sınıf var.
- **Support:** Her sınıf için 400 örnek var, bu da verilerin dengesiz olmadığını gösteriyor.
- **Accuracy:** Genel doğruluk oranı %11, bu da modelin çok düşük bir başarı oranına sahip olduğunu gösteriyor.
- **Macro ve Weighted Average:** Her iki durumda da modelin genel performansı oldukça zayıf.

## Sonuç
- Model herhangi bir öğrenme gerçekleştirememiştir ve veriyi sınıflandırmada başarılı olmamıştır.
- Veri artırma ve dropout uygulanmış ancak yeterli olmamıştır.

## Olası Sebepler ve Çözüm Yolları
1. **Yetersiz Model Kompleksitesi:** Modelin derinliği ve kapasitesi, sınıflandırma probleminin zorluk seviyesine göre düşük olabilir.
2. **Optimizasyon Problemi:** Öğrenme oranı (learning rate) çok düşük olarak seçilmiştir. Bu nedenle model çok yavaş öğrenmiş ve eğitim boyunca neredeyse hiç ilerleme kaydedememiştir.
3. **Veri Artırımı ve Dengesi:** Daha fazla veri artırımı (augmentation) uygulanabilir.

## Projenin Kaggle Linki
[Fish Classification Kaggle Projesi](https://www.kaggle.com/code/sedaekici/fish-classification)
