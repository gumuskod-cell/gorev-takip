# 📱 Görev Takip — Kurulum ve Yayınlama Rehberi

## 📦 Proje Dosyaları Yapısı

```
GorevTakip/
├── app/
│   ├── _layout.js        ← Uygulama kök düzeni
│   └── index.js          ← Ana ekran
├── components/
│   ├── TaskCard.js        ← Görev kartı bileşeni
│   └── AddTaskModal.js    ← Görev ekleme ekranı
├── constants/
│   └── index.js          ← Renkler, kullanıcılar, kategoriler
├── utils/
│   ├── storage.js        ← Yerel veri saklama
│   └── notifications.js  ← Bildirim yönetimi
├── assets/               ← İkon ve görsel dosyalar (aşağıya bak)
├── app.json              ← Uygulama ayarları
├── eas.json              ← Build ayarları
├── package.json          ← Bağımlılıklar
└── babel.config.js       ← Babel ayarları
```

---

## 🛠️ 1. Adım: Gerekli Programları Kur

### Node.js (zorunlu)
1. https://nodejs.org adresine git
2. **LTS** sürümünü indir ve kur
3. Kurulumu doğrulamak için terminal/komut istemcisinde çalıştır:
   ```
   node --version
   ```

### Expo CLI
Terminalde şunu çalıştır:
```bash
npm install -g expo-cli eas-cli
```

---

## 📁 2. Adım: Proje Klasörünü Hazırla

1. İndirdiğin **GorevTakip** klasörünü istediğin bir yere koy (örn: Masaüstü)
2. Terminali aç ve klasöre git:
   ```bash
   cd ~/Desktop/GorevTakip
   ```
3. Bağımlılıkları yükle:
   ```bash
   npm install
   ```

---

## 🖼️ 3. Adım: İkon ve Görsel Dosyaları Ekle

`assets/` klasörüne şu dosyaları eklemen gerekiyor:

| Dosya                  | Boyut      | Açıklama              |
|------------------------|------------|-----------------------|
| `icon.png`             | 1024×1024  | Uygulama ikonu        |
| `splash.png`           | 1242×2436  | Açılış ekranı         |
| `adaptive-icon.png`    | 1024×1024  | Android adaptif ikon  |
| `notification-icon.png`| 96×96      | Bildirim ikonu        |

> 💡 **Kolaylaştırma:** https://www.canva.com adresinde ücretsiz ikon oluşturabilirsin.
> Geçici olarak aynı dosyayı farklı isimlerle 4 kez kopyalayabilirsin.

---

## 👥 4. Adım: Kullanıcıları ve Kategorileri Düzenle

`constants/index.js` dosyasını bir metin editörüyle aç ve şu kısımları düzenle:

```javascript
// Kullanıcılar - kendi ekibini buraya yaz
export const USERS = [
  'Ad Soyad 1',
  'Ad Soyad 2',
  // ...
];

// Kategoriler - kendi başlıklarını buraya yaz
export const CATEGORIES = ['YEĞİTEK', 'STEM', 'AR-GE', 'EĞİTİM', 'GENEL'];
```

---

## 📱 5. Adım: Telefonda Test Et (Ücretsiz)

### Expo Go ile Anında Test
1. Telefonuna **Expo Go** uygulamasını indir (App Store / Play Store)
2. Terminalde çalıştır:
   ```bash
   npx expo start
   ```
3. QR kodu telefonunla tara → Uygulama açılır! ✅

---

## 🏗️ 6. Adım: APK/IPA Oluştur (Gerçek Uygulama)

### Expo Hesabı Aç
1. https://expo.dev adresine git → **Sign Up** → Ücretsiz hesap aç
2. Terminalde giriş yap:
   ```bash
   eas login
   ```

### Projeyi Bağla
```bash
eas init
```
Bu komut sana bir **Project ID** verecek. `app.json` dosyasındaki
`"YOUR_EAS_PROJECT_ID"` yazan yere bu ID'yi yaz.

---

### 🤖 Android APK Oluştur (Ücretsiz)

```bash
eas build --platform android --profile preview
```

- Build başlar (Expo'nun sunucularında ~10-15 dk)
- Tamamlandığında **APK download linki** gelir
- APK'yı herhangi bir Android telefona kurabilirsin

**Google Play'e Yüklemek İçin:**
```bash
eas build --platform android --profile production
```
→ AAB dosyası oluşur → Google Play Console'a yükle

---

### 🍎 iOS IPA Oluştur

> ⚠️ iOS için **Apple Developer hesabı** gerekli ($99/yıl)

1. https://developer.apple.com adresinde hesap aç
2. `app.json` dosyasında `bundleIdentifier`'ı benzersiz bir şeye değiştir
3. Build başlat:
   ```bash
   eas build --platform ios --profile production
   ```

---

## 🔔 Bildirim Sistemi Nasıl Çalışır?

Görev eklendiğinde otomatik olarak şu bildirimler planlanır:

| Zaman          | Bildirim                              |
|----------------|---------------------------------------|
| 3 gün önce     | ⚠️ "Görev yaklaşıyor"               |
| 1 gün önce     | 🚨 "Yarın son gün"                   |
| Görev günü     | 🔴 "Bugün son gün"                   |

Tüm bildirimler saat **09:00**'da gelir (görev günü 08:00).

---

## ✏️ Sık Sorulan Değişiklikler

### Yeni kullanıcı eklemek:
`constants/index.js` → `USERS` dizisine ekle

### Yeni kategori eklemek:
`constants/index.js` → `CATEGORIES` dizisine ekle, `CATEGORY_COLORS`'a reng ekle

### Uygulama adını değiştirmek:
`app.json` → `"name"` alanını düzenle

### Bildirim saatini değiştirmek:
`utils/notifications.js` → `setHours(9, 0, 0, 0)` → saati değiştir

---

## ❓ Yardım

- Expo Docs: https://docs.expo.dev
- EAS Build: https://docs.expo.dev/build/introduction
- Destek Forum: https://forums.expo.dev
