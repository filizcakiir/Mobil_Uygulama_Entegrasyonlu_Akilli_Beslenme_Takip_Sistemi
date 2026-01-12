# 📱 GastronomGöz Mobile App

GastronomGöz'ün mobil uygulaması - AI destekli yemek tanıma ve kalori hesaplama sistemi için Flutter tabanlı kullanıcı arayüzü.

## 🚀 Özellikler

- 📸 **Kamera & Galeri Entegrasyonu**: Yemek fotoğrafı çekme veya galeri seçimi
- 🍽️ **Yemek Analizi**: AI ile otomatik yemek tanıma ve kalori hesaplama
- 📊 **İstatistik Takibi**: Günlük, haftalık ve aylık kalori istatistikleri
- 📜 **Geçmiş Kayıtları**: Tüm analiz geçmişini görüntüleme
- 🔐 **Kullanıcı Yönetimi**: Kayıt, giriş ve profil yönetimi
- 🌍 **Çoklu Dil Desteği**: Türkçe ve İngilizce dil seçenekleri
- 🎨 **Modern UI/UX**: Material Design ile kullanıcı dostu arayüz

## 🛠️ Teknolojiler

- **Framework**: Flutter 3.10+
- **State Management**: Provider
- **HTTP Client**: Dio
- **Güvenli Depolama**: Flutter Secure Storage (JWT token)
- **Yerel Depolama**: Shared Preferences
- **Grafikler**: FL Chart
- **Lokalizasyon**: Flutter Intl

## 📁 Proje Yapısı

```
lib/
├── l10n/                    # Dil dosyaları (TR/EN)
├── models/                  # Veri modelleri
│   ├── user.dart
│   ├── food_analysis.dart
│   └── nutrition.dart
├── providers/               # State management
│   ├── auth_provider.dart
│   ├── language_provider.dart
│   └── analysis_provider.dart
├── screens/                 # Uygulama ekranları
│   ├── auth/               # Giriş/Kayıt ekranları
│   ├── camera/             # Kamera ekranı
│   ├── history/            # Geçmiş ekranı
│   ├── stats/              # İstatistik ekranı
│   └── profile/            # Profil ekranı
├── services/               # API servisleri
│   ├── api_service.dart
│   ├── auth_service.dart
│   └── storage_service.dart
└── main.dart               # Uygulama giriş noktası
```

## ⚙️ Kurulum

### Gereksinimler

- Flutter SDK 3.10 veya üzeri
- Dart 3.0 veya üzeri
- Android Studio / Xcode (platform bazlı)

### Adımlar

1. **Bağımlılıkları yükleyin**:
```bash
flutter pub get
```

2. **Dil dosyalarını oluşturun**:
```bash
flutter gen-l10n
```

3. **Uygulamayı çalıştırın**:
```bash
flutter run
```

## 🔧 Yapılandırma

Backend API URL'sini `lib/services/api_service.dart` dosyasında güncelleyin:

```dart
static const String baseUrl = 'http://YOUR_BACKEND_URL:5001';
```

## 📱 Platform Desteği

- ✅ Android (API 21+)
- ✅ iOS (12.0+)

## 🧪 Test

```bash
flutter test
```

## 📦 Build

### Android APK
```bash
flutter build apk --release
```

### iOS
```bash
flutter build ios --release
```

## 📄 Lisans

MIT License
