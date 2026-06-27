# Proje Prompt Günlüğü

Bu doküman, Los Angeles Trafik (METR-LA) veri seti kullanılarak gerçekleştirilen veri bilimi projesinin oluşturulma sürecinde kullanılan yapay zeka prompt'larını içermektedir.

---

**Prompt 1: Proje Tanımı ve Yol Haritası Çıkarma**
Veri bilimi final projem için Akıllı Şehir ve Ulaşım teması altında Los Angeles Trafik(METR-LA) veri setini kullanacağım. Elimde 207 farklı trafik sensöründen 4 ay boyunca beser dakikalık periyotlarla toplanmış araç hız verilerini içeren "METR-LA.h5" adlı bir HDF5 dosyası var. Bu projede bir veri bilimi iş akışını (veri temizleme, EDA, modelleme) Jupyter notebook üzerinde uygulamam gerekiyor. Bunun için adım adım bir yol haritası çıkarır mısın?

**Prompt 2: Veri Yükleme ve İlk İnceleme**
İlk olarak veri yükleme ve inceleme ile başlayalım. METR-LA.h5 dosyasını pandas ve h5py kütüphaneleri ile okuyup bir dataFramee dönüştüren verinin boyutunu, ilk 5 satırını (head()) ve genel yapısını (info()) ekrana yazdıran kodu yazar mısın? Kodlara neyin neden yapıldığını açıklayan türkçe yorum satırları da ekle.

**Prompt 3: Veri Temizleme**
Veri yüklendi.Şimdi temizleme aşamasına geçelim. Zaman serisi verisi olduğu için veri setindeki eksik ve hatalı değerleri (NaN) tespit edip ffill ve bfill yöntemiyle temizleyen bir kod yazar mısın? Ayrıca 0-100 mph aralığı dışındaki mantıksız hız değerlerini aykırı değerleri kontrol etsin ve sonucu "METR-LA-temiz.h5" olarak kaydetsin.

**Prompt 4: Özellik Mühendisliği (Feature Engineering)**
Veri temizlendi. Veri setimizin indeksi Unix timestamp formatında. Modellemede ve veri analizinde kullanabilmek için bu indeksi pandas DatetimeIndex formatına çeviren ve bu indeksten saat (0-23) ve haftanin_gunu (0-6) adında iki yeni bağımsız değişken üreten python hücresini oluşturur musun?

**Prompt 5: EDA / Araştırma Sorularının Belirlenmesi**
Şimdi EDA aşamasına geçiyoruz. Los Angeles otoyollarındaki trafik akışını ve rush hour durumlarını analiz etmek istiyorum. Bu veri setini kullanarak cevaplayabileceğimiz 3 adet somut araştırma sorusu belirleyip bunları projede kullanabilmem için bir markdown hücresine yazar mısın?

**Prompt 6: EDA / Görselleştirme 1 ve 2 (Çizgi ve Kutu Grafikleri)**
Şimdi bu soruları görselleştirmeye başlayalım. Seaborn ve Matplotlib kullanarak güzel ve koyu temalı grafikler çizelim 1) günün saatlerine göre ortalama hızı gösteren bir çizgi grafiği 2) hafta içi ve hafta sonu hız dağılımlarını karşılaştıran bir kutu grafiği veya keman grafiği çizen kodları yazar mısın? Eksen etiketleri türkçe olsun.

**Prompt 7: EDA / Görselleştirme 3 ve 4 (Isı Haritası ve Dağılım)**
EDA'yı tamamlamak için 2 farklı görselleştirmeye daha ihtiyacım var 3) haftanın günlerine ve saatlere göre trafik yoğunluğunu gösteren bir ısı haritası 4) tüm veri setindeki genel hız dağılımını gösteren bir histogram + KDE grafiği yazar mısın? Grafikleri oluşturduktan sonra bulguları Los Angeles trafiği bağlamında kısaca yorumla.

**Prompt 8: Ekstra EDA Görseli:**
Ek olarak otoyoldaki farklı sensörlerin birbiriyle uyumunu görmek istiyorum. Veri setinden rastgele seçilmiş 5 farklı sensörün 1 haftalık hız değişimini aynı çizgi grafiği üzerinde gösteren ve bu sensörler arasındaki ortalama korelasyonu hesaplayan 5. bir görselleştirme için kod hücresi yazar mısın?

**Prompt 9: Modelleme Hazırlığı**
Şimdi Basit Modelleme aşamasına geçiyoruz. Amacımız sadece saat ve gün bilgisine bakarak trafiğin o an sıkışık olup olmayacağını tahmin etmek. Ortalama hız 40 mph'nin altındaysa "1" (Sıkışık), 40 mph ve üzerindeyse "0" (Akıcı) olacak şekilde trafik_durumu adında bir hedef değişken oluştur. Modelin çok uzun sürmemesi için tüm veriden rastgele %20'lik bir örneklem al.

**Prompt 10: Model Kurulumu ve Eğitimi (Random Forest)**
scikit-learn kütüphanesini kullanarak veriyi %80 eğitim ve %20 test seti olarak ayır. Bağımsız değişken olarak sadece saat ve haftanin_gunu sütunlarını kullan. Veri dengesiz olduğu için class_weight='balanced' parametresi ile bir Random Forest Classifier modeli kur ve test verisi üzerinde eğit.

**Prompt 11: Model Başarısının Değerlendirilmesi**
Model eğitildi. Şimdi modelin ne kadar başarılı olduğunu görmem lazım. Sınıflandırma raporunu (Accuracy, Precision, Recall, F1-Score) ekrana yazdıran ve Karmaşıklık matrisini bir seaborn grafiği olarak çizdirip projedeki gorseller klasörüne kaydeden kodu oluştur.Ek olarak veri setimiz çok dengesiz olduğu için hesaplanacak accuracy ve recall değerlerini yorumlarken nelere dikkat etmemiz gerektiğini kodun altına markdown olarak açıkla.

**Prompt 12: Model Yorumlanabilirliği**
Peki modelimiz trafiğin sıkışık olup olmayacağını tahmin ederken saat özelliğine mi yoksa haftanın_günü özelliğine mi daha çok güveniyor? Bunu görmek için Random Forest modelinin özellik önemi skorlarını yüzdelik olarak hesaplayıp ekrana yazdıran bir kod ekle.

**Prompt 13: Canlı Senaryo Testi**
Şimdi test edelim. Modelin çalışma mantığını gösterebilmek için 5 farklı günlük hayat senaryosu belirle mesela salı sabah 08.00, perşembe akşam 17.00 gibi bu saatleri modele verip tahmini durumu (akıcı/sıkışık) ve sıkışıklık olasılığı yüzdesini tablo şeklinde ekrana yazdıran bir kod hücresi yaz.

**Prompt 14: Hata/Mantık Kontrolü**
Classification report sonuçlarına göre modelimizin accuracysi fena değil ancak sıkışık sınıfını bulma oranı biraz düşük görünüyor. Sadece 2 özellik saat ve gün olarak kullandığımız için bu durum normal mi? Eğer bu modeli daha da iyileştirmek istiyorsak veri setine hangi özellikleri eklememiz gerekirdi bunu markdown olarak kısaca açıkla.