# 🚦 Akıllı Şehir & Ulaşım: METR-LA Trafik Veri Analizi

**Ad Soyad**   : Rabianur Becit  
**Öğrenci No** : 1306230084  
**Ders**       : Veri Bilimi  

---

## Proje Özeti

Bu proje, Los Angeles Metropolitan bölgesindeki **207 trafik sensöründen** toplanan araç hız verilerini analiz ederek şehir içi trafik örüntülerini anlamayı ve trafik sıkışıklığını tahmin etmeyi amaçlamaktadır.

---

## Proje Yapısı

```
Akıllı-Sehir-Trafik-EDA/
│
├── data/                     # Veri Setleri
│   ├── raw/                  
│   │   └── METR-LA.h5        # Ham veri seti (HDF5 formatı)
│   └── processed/            
│       └── METR-LA-temiz.h5  # Temizlenmiş veri seti
│
├── metr_la_analiz.ipynb      # Ana analiz notebook'u (veri yükleme → EDA → modelleme)
│
├── gorseller/                # Tüm görselleştirme çıktıları
│   ├── gorseller_saat_lineplot.png        # Saatlik hız analizi
│   ├── gorseller_hafta_boxplot.png        # Hafta içi/sonu karşılaştırması
│   ├── gorseller_gun_saat_heatmap.png     # Gün×Saat ısı haritası
│   ├── gorseller_dagilim.png              # Hız dağılımı
│   ├── gorseller_sensor_zaman.png         # Çoklu sensör zaman serisi
│   └── gorseller_confusion_matrix.png     # Model performans matrisi
│
├── README.md                 # Bu dosya
└── rapor.md                  # Proje raporu (PDF'e dönüştürülmüş hali teslim edilecek)
```

---

## Veri Seti

**Adı**    : METR-LA (Los Angeles Metropolitan Traffic Dataset)  
**Orijinal Kaynak** : [DCRNN GitHub — liyaguang/DCRNN](https://github.com/liyaguang/DCRNN)  
**Kaggle Linki** : [Kaggle - METR-LA Dataset](https://www.kaggle.com/datasets/annnnguyen/metr-la-dataset)  
**Lisans** : MIT License  
**İçerik** : 207 sensör, 5 dakikalık aralıklar, Mart–Haziran 2012  
**Boyut**  : 34.272 zaman adımı × 207 sensör  
**Birim**  : mil/saat (mph)  

---

## Projeyi Çalıştırma Talimatları

### 1. Gereksinimler
- Python 3.9+
- Git

### 2. Repoyu Klonla
```bash
git clone https://github.com/Rabianur1/Akilli-Sehir-Trafik-EDA
cd Akilli-Sehir-Trafik-EDA
```

### 3. Sanal Ortam Oluştur ve Aktifleştir
```bash
#Windows
python -m venv .venv
.\.venv\Scripts\activate

#macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Kütüphaneleri Yükle
```bash
pip install -r requirements.txt
```

### 5. Notebook'u Çalıştır
```bash
jupyter notebook metr_la_analiz.ipynb
```
> VS Code kullanıyorsanız: `metr_la_analiz.ipynb` dosyasını açınız, kernel olarak `.venv` seçiniz, **Run All** yapınız.

---

## Kullanılan Kütüphaneler

| Kütüphane | Versiyon | Kullanım Amacı |
|-----------|----------|----------------|
| `pandas` | 3.0.3 | Veri işleme ve analiz |
| `numpy` | 2.4.6 | Sayısal hesaplamalar |
| `matplotlib` | 3.11.0 | Görselleştirme |
| `seaborn` | 0.13.2 | İstatistiksel görselleştirme |
| `scikit-learn` | ≥1.0 | Random Forest modeli |
| `h5py` | ≥3.0 | HDF5 dosya okuma |
| `scipy` | ≥1.9 | KDE hesaplama |
| `tables` | 3.11.1 | HDF5 desteği |

---

## Araştırma Soruları ve Bulgular

SORU1: Günlük trafik ritmi nasıl? | En yavaş saat **17:00** (46.5 mph), en hızlı **03:00** (54.7 mph)  
SORU2: Hafta içi/sonu farkı? | Hafta sonu **+2.70 mph** daha hızlı  
SORU3: En yoğun gün/saat? | **Perşembe 17:00** (42.2 mph), en hızlı **Cumartesi 01:00** (62.8 mph)  

---

## Model Özeti

- **Yöntem:** Random Forest Sınıflandırıcı
- **Hedef:** Trafik sıkışıklığı tahmini (< 40 mph = sıkışık)
- **Özellikler:** `saat`, `haftanin_gunu`
- **Accuracy:** %60.83 | **Sıkışık Recall:** 0.58

---

## Notlar

- `METR-LA.h5` dosyası eski pandas formatında kaydedildiğinden `pd.read_hdf()` yerine `h5py` kullanılmıştır.
- `.venv/` klasörü Git'e dahil edilmemiştir. (`.gitignore` ile hariç tutulmuştur)
