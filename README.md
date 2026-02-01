# GastronomGöz: Mobil Uygulama Entegrasyonlu Akıllı Beslenme Takip Sistemi

GastronomGöz, bir yemeğin fotoğrafından türünü tanıyan, derinlik ve segmentasyon analizleriyle hacmini hesaplayan ve tahmini kalori değerini çıkaran yapay zeka destekli bir beslenme takip sistemidir. Web arayüzü ve mobil uygulama ile kullanıcıların sağlıklı beslenme alışkanlıklarını takip etmelerini sağlar.

## Temel Özellikler

- **101 Sınıflı Yemek Tanıma** - ResNet50 (Food-101 veri seti)
- **Görüntü Segmentasyonu** - U-2-Net ile yemek maskesi çıkarma
- **Derinlik Analizi ve Hacim Hesaplama** - MiDaS (DPT_Large)
- **Kalori ve Besin Değeri Tahmini** - gram × kalori/100g hesaplaması
- **Kullanıcı Yönetimi** - JWT tabanlı kimlik doğrulama
- **Analiz Geçmişi** - Günlük, haftalık, aylık istatistikler
- **Başarım Sistemi** - Kullanıcı motivasyonu için rozetler
- **Çok Dilli Destek** - Türkçe ve İngilizce

---

## Teknoloji Yığını

### Backend (Python/Flask)
| Teknoloji | Kullanım Alanı |
|-----------|----------------|
| Flask 3.1.0 | Web framework |
| SQLAlchemy | ORM / Veritabanı |
| Flask-JWT-Extended | Kimlik doğrulama |
| Bcrypt | Şifre güvenliği |
| Flask-Migrate | Veritabanı migration |

### Yapay Zeka / Makine Öğrenmesi
| Model | Kullanım Alanı |
|-------|----------------|
| ResNet50 (TensorFlow/Keras) | Yemek sınıflandırma |
| U-2-Net (PyTorch) | Görüntü segmentasyonu |
| MiDaS DPT_Large (PyTorch) | Derinlik tahmini |
| OpenCV, NumPy, Pandas | Görüntü işleme |

### Mobil Uygulama (Flutter)
| Teknoloji | Kullanım Alanı |
|-----------|----------------|
| Flutter 3.10+ | Cross-platform framework |
| Provider | State management |
| Dio | HTTP client |
| Flutter Secure Storage | JWT token saklama |
| FL Chart | Grafik ve istatistikler |

---

## Proje Yapısı

```
food_volume/
├── app.py                          # Legacy Flask web uygulaması
├── data_loader.py                  # Görüntü ön işleme
├── requirements.txt                # Python bağımlılıkları
│
├── backend/                        # RESTful API Backend
│   ├── app.py                      # Flask uygulama fabrikası
│   ├── config.py                   # Konfigürasyon
│   ├── api/                        # API endpoint'leri
│   │   ├── auth.py                 # Kimlik doğrulama
│   │   ├── prediction.py           # Yemek analizi
│   │   ├── history.py              # Analiz geçmişi
│   │   ├── notification.py         # Bildirimler
│   │   └── user.py                 # Kullanıcı yönetimi
│   ├── core/                       # İş mantığı
│   │   ├── ai_engine.py            # Model yükleme ve çıkarım
│   │   ├── image_processor.py      # Görüntü işleme
│   │   └── weight_calculator.py    # Ağırlık tahmini
│   ├── models/                     # Veritabanı modelleri
│   ├── ml_models/                  # AI model wrapper'ları
│   └── tests/                      # Birim testleri
│
├── mobile/
│   └── food_calorie_app/           # Flutter Mobil Uygulama
│       ├── lib/
│       │   ├── main.dart           # Uygulama giriş noktası
│       │   ├── screens/            # UI ekranları
│       │   │   ├── auth/           # Giriş/Kayıt
│       │   │   ├── camera/         # Kamera
│       │   │   ├── history/        # Geçmiş
│       │   │   ├── stats/          # İstatistikler
│       │   │   └── profile/        # Profil
│       │   ├── services/           # API servisleri
│       │   ├── providers/          # State yönetimi
│       │   └── generated/          # Lokalizasyon (TR/EN)
│       ├── android/                # Android platform
│       └── ios/                    # iOS platform
│
├── model/                          # ML model tanımları
│   └── u2net.py                    # U-2-Net mimarisi
│
└── weights/                        # Eğitilmiş model ağırlıkları
    ├── model_trained_101class.hdf5
    └── calories_per_101class_100g.csv
```

---

## Model Eğitimi (ResNet50)

### Veri Seti
- **Food-101**: 101 sınıfa ait 101.000 yemek görseli

### Model Mimarisi
```python
resnet50 = ResNet50(weights='imagenet', include_top=False)
x = resnet50.output
x = GlobalAveragePooling2D()(x)
x = Dense(128, activation='relu')(x)
x = Dropout(0.2)(x)
predictions = Dense(101, activation='softmax')(x)
model = Model(inputs=resnet50.input, outputs=predictions)
```

### Eğitim Parametreleri
- **Optimizer:** SGD (lr=0.0001, momentum=0.9)
- **Loss:** Categorical Crossentropy
- **Callbacks:** ModelCheckpoint, CSVLogger

---

## Kurulum

### Gereksinimler
- Python 3.9+
- Flutter 3.10+
- Node.js (opsiyonel)

### Backend Kurulumu

```bash
# Sanal ortam oluştur
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Bağımlılıkları yükle
pip install -r requirements.txt

# Model ağırlıklarını indir
# U-2-Net: https://github.com/xuebinqin/U-2-Net
# MiDaS: https://github.com/isl-org/MiDaS
```

### Mobil Uygulama Kurulumu

```bash
cd mobile/food_calorie_app

# Bağımlılıkları yükle
flutter pub get

# Uygulamayı çalıştır
flutter run
```

---

## Uygulamayı Çalıştırma

### Web Arayüzü (Legacy)
```bash
python app.py
# http://127.0.0.1:5000
```

### Backend API
```bash
cd backend
python app.py
# http://127.0.0.1:5000/api
```

### Mobil Uygulama
```bash
cd mobile/food_calorie_app
flutter run
```

---

## API Endpoint'leri

| Endpoint | Metod | Açıklama |
|----------|-------|----------|
| `/api/auth/register` | POST | Kullanıcı kaydı |
| `/api/auth/login` | POST | Kullanıcı girişi |
| `/api/predict` | POST | Yemek analizi |
| `/api/history` | GET | Analiz geçmişi |
| `/api/stats` | GET | İstatistikler |
| `/api/notifications` | GET | Bildirimler |

---

## Ekran Görüntüleri

### Segmentasyon Örneği
![Segmentasyon](static/uploads/mask_donut.png)

---

## Lisans

MIT License

---

## İletişim

**Filiz Çakır**
Bilecik Şeyh Edebali Üniversitesi
Bilgisayar Mühendisliği Bölümü

**Danışman:** Prof. Dr. Uğur Yüzgeç
