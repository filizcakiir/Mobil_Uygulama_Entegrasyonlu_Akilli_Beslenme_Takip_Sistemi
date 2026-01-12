# 🔧 GastronomGöz Backend API

GastronomGöz için Flask tabanlı RESTful API backend sistemi. AI modelleriyle yemek tanıma, hacim hesaplama ve kalori tahmini işlemlerini yönetir.

## 🚀 Özellikler

- 🤖 **AI Model Entegrasyonu**
  - ResNet50 ile yemek tanıma (101 sınıf)
  - U-2-Net ile segmentasyon
  - MiDaS ile derinlik haritası ve hacim hesaplama

- 🔐 **Güvenlik**
  - JWT tabanlı kimlik doğrulama
  - Bcrypt ile şifre hashleme
  - Token yenileme mekanizması

- 📊 **Veri Yönetimi**
  - SQLite veritabanı
  - SQLAlchemy ORM
  - Flask-Migrate ile veritabanı migrasyonları

- 📈 **Kullanıcı Özellikleri**
  - Kullanıcı kaydı ve girişi
  - Analiz geçmişi takibi
  - Günlük/haftalık/aylık istatistikler
  - Detaylı beslenme bilgileri

## 🛠️ Teknolojiler

- **Framework**: Flask 2.3+
- **ORM**: SQLAlchemy
- **Auth**: Flask-JWT-Extended
- **Database**: SQLite
- **AI/ML**: TensorFlow, PyTorch, OpenCV
- **Image Processing**: Pillow, NumPy
- **Models**: ResNet50, U-2-Net, MiDaS

## 📁 Proje Yapısı

```
backend/
├── api/                     # API endpoints
│   ├── auth.py             # Kimlik doğrulama
│   ├── analysis.py         # Yemek analizi
│   ├── history.py          # Geçmiş kayıtları
│   └── stats.py            # İstatistikler
├── core/                    # Çekirdek işlevler
│   ├── image_processor.py  # Görsel işleme
│   ├── volume_calculator.py # Hacim hesaplama
│   └── nutrition_calculator.py # Beslenme hesaplama
├── models/                  # Veritabanı modelleri
│   ├── user.py
│   ├── daily_log.py
│   └── food_analysis.py
├── ml_models/              # AI model yükleyicileri
│   ├── classifier.py       # ResNet50
│   ├── segmentation.py     # U-2-Net
│   └── depth.py            # MiDaS
├── middleware/             # Middleware'ler
│   └── auth.py            # JWT doğrulama
├── migrations/            # Veritabanı migrasyonları
├── app.py                 # Flask uygulaması
├── config.py              # Yapılandırma
└── requirements.txt       # Python bağımlılıkları
```

## ⚙️ Kurulum

### Gereksinimler

- Python 3.9 veya üzeri
- pip
- Virtual environment (önerilir)

### Adımlar

1. **Virtual environment oluşturun**:
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# veya
venv\Scripts\activate  # Windows
```

2. **Bağımlılıkları yükleyin**:
```bash
pip install -r requirements.txt
```

3. **Ortam değişkenlerini ayarlayın**:
```bash
cp .env.example .env
# .env dosyasını düzenleyin
```

4. **Veritabanını oluşturun**:
```bash
flask db upgrade
```

5. **AI modellerini indirin**:
- ResNet50 ağırlıkları (model_trained_101class.hdf5)
- U-2-Net ağırlıkları
- MiDaS DPT_Large ağırlıkları

6. **Uygulamayı başlatın**:
```bash
python app.py
```

API şu adreste çalışacak: `http://localhost:5001`

## 🔧 Yapılandırma

`.env` dosyasında aşağıdaki değişkenleri ayarlayın:

```env
FLASK_APP=app.py
FLASK_ENV=development
SECRET_KEY=your-secret-key
JWT_SECRET_KEY=your-jwt-secret-key
DATABASE_URL=sqlite:///database_dev.db
```

## 📡 API Endpoints

### Kimlik Doğrulama
- `POST /api/auth/register` - Yeni kullanıcı kaydı
- `POST /api/auth/login` - Kullanıcı girişi
- `POST /api/auth/refresh` - Token yenileme
- `GET /api/auth/profile` - Kullanıcı profili

### Analiz
- `POST /api/analysis/upload` - Yemek fotoğrafı analizi
- `GET /api/analysis/history` - Analiz geçmişi
- `GET /api/analysis/:id` - Tekil analiz detayı

### İstatistikler
- `GET /api/stats/daily` - Günlük istatistikler
- `GET /api/stats/weekly` - Haftalık istatistikler
- `GET /api/stats/monthly` - Aylık istatistikler

## 🧪 Test

```bash
pytest tests/
```

## 📊 Veritabanı Migrasyonları

Yeni migration oluşturma:
```bash
flask db migrate -m "Migration açıklaması"
```

Migration uygulama:
```bash
flask db upgrade
```

Migration geri alma:
```bash
flask db downgrade
```

## 🐛 Debug

Debug modu için:
```bash
export FLASK_ENV=development
flask run --debug
```

## 📄 Lisans

MIT License
