# 🚀 SpaceExplorer — Gerçek Zamanlı Uzay Keşif Platformu

SpaceExplorer, **uzayla ilgili güncel verileri tek bir platformda toplayan**,  
**NASA ve açık uzay API’leri ile entegre çalışan**,  
**otomatik zamanlayıcı (scheduler) altyapısına sahip modern bir Django web uygulamasıdır.**

Bu proje; **ISS canlı takibi**, **uzay haberleri**, **gezegenler**, **cüce gezegenler**,  
**asteroidler**, **gezegen uyduları**, **astronotlar** ve **SpaceX görevleri** gibi  
birçok uzay verisini **anlık olarak API’lerden çekerek kullanıcıya sunar.**

> 🌌 Tüm veriler manuel değil, **scheduler ile otomatik güncellenir.**  
> 🔄 Veri akışı: **API → Veritabanı (cache) → Kullanıcı arayüzü**

---
## 🎯 Projenin Amacı

SpaceExplorer projesinin temel amacı:

- Uzayla ilgili **dağınık halde bulunan API verilerini tek merkezde toplamak**
- Kullanıcılara **gerçek zamanlı ve güncel uzay verileri** sunmak
- API tabanlı veri toplama + otomatik güncelleme mimarisini uygulamalı göstermek
- Backend odaklı, **gerçek veri akışı olan profesyonel bir Django projesi** geliştirmek

Bu proje özellikle:

- Backend geliştirme
- API entegrasyonu
- Scheduler & otomatik veri yönetimi
- Veri modelleme
- Gerçek zamanlı sistem tasarımı

alanlarında güçlü bir örnek sunar.

---

## ✨ Proje Özellikleri

### 🛰️ ISS (International Space Station)
- Canlı ISS konum takibi (enlem/boylam)
- Uzaydaki kişi sayısı bilgisi
- API’den anlık veri çekimi
- JSON endpoint ile canlı veri sunumu

### 📰 Uzay Haberleri
- SpaceFlight News API entegrasyonu
- En güncel uzay haberleri (maks. 30 haber)
- Görsel destekli haber listesi
- Otomatik güncelleme + eski veriyi temizleme

### 🪐 Güneş Sistemi (Gezegenler)
- Gezegenlerin temel bilgileri:
  - Kütle, yerçekimi, yarıçap, uydu sayısı
- Le Systeme Solaire API üzerinden otomatik veri çekimi

### 🌙 Gezegen Uyduları
- Gezegenlere ait doğal uydular
- Keşif tarihi, keşfeden kişi
- Fiziksel özellikler
- Otomatik güncelleme (24 saatte bir)

### 🌌 Cüce Gezegenler
- Pluto, Ceres, Eris, Haumea, Makemake
- Özel görseller + fiziksel bilimsel veriler
- Uydu sayıları ve keşif bilgileri

### ☄️ Asteroidler
- Le Systeme Solaire API üzerinden asteroid verileri
- Fiziksel ölçümler + yörünge bilgileri
- Otomatik veri çekme sistemi

### 👨‍🚀 Astronotlar
- Uzayda bulunan aktif astronotlar
- Ajans bilgileri (NASA, ESA, Roscosmos, JAXA, CNSA)
- Görev/rol bilgisi + görseller
- Otomatik aktif/pasif güncelleme

### 🚀 SpaceX Görevleri
- En son SpaceX fırlatma bilgisi
- Görev tarihi, başarı durumu, detaylar
- Video bağlantısı ve patch görselleri
- Otomatik güncelleme (saatlik)

---
## 🧠 Sistem Mimarisi

SpaceExplorer, sade ama gerçek bir backend mimarisiyle geliştirilmiştir.

**Genel akış:**

Scheduler, uygulama ayağa kalktığında Uzay/apps.py içindeki ready() fonksiyonu ile başlar.

1. Harici uzay API’lerinden veri çekilir (`utils.py`)
2. Veriler Django modelleri ile veritabanına kaydedilir
3. APScheduler arka planda otomatik güncellemeleri yürütür
4. Kullanıcılar güncel verileri web arayüzü üzerinden görüntüler

Amaç:
> **Güncel veri + hızlı sayfa yükleme + sürdürülebilir sistem**

---

## 🔗 Kullanılan API Kaynakları

- **ISS Konum API**  
  http://api.open-notify.org/iss-now.json

- **Uzaydaki İnsanlar API**  
  http://api.open-notify.org/astros.json

- **SpaceX Son Fırlatma**  
  https://api.spacexdata.com/v4/launches/latest

- **Güneş Sistemi Verileri**  
  https://api.le-systeme-solaire.net/rest/bodies/

- **Uzay Haberleri API**  
  https://api.spaceflightnewsapi.net/v4/articles

---

## 🌍 Sayfalar ve URL Yapısı

| Sayfa | URL |
|------|-----|
| Ana Sayfa | `/` |
| ISS Takip | `/iss/` |
| Güneş Sistemi | `/solar-system/` |
| Uzay Haberleri | `/news/` |
| Gezegen Uyduları | `/planet-moons/` |
| Cüce Gezegenler | `/dwarf-planets/` |
| Asteroidler | `/asteroids/` |
| Astronotlar | `/astronauts/` |
| ISS Canlı API | `/api/iss-location/` |

---

## ⏱️ Otomatik Veri Güncellemeleri

APScheduler kullanılarak veriler arka planda düzenli olarak yenilenir.

| Veri | Güncelleme Süresi |
|------|------------------|
| SpaceX Fırlatma | 60 dakika |
| ISS Konumu | Anlık |
| Gezegen Verileri | 60 dakika |
| Uzay Haberleri | 60 dakika |
| Uydular | 24 saat |
| Cüce Gezegenler | 24 saat |
| Asteroidler | 24 saat |
| Astronotlar | 24 saat |

> Not: Geliştirme ortamı için scheduler `AppConfig.ready()` içerisinde başlatılmıştır.

---

## 🗃️ Kullanılan Veritabanı Modelleri

- `SpaceXLaunch` → SpaceX fırlatma bilgileri  
- `ISSLocation` → ISS konum geçmişi  
- `SolarSystemBody` → Gezegenler  
- `SpaceNews` → Uzay haberleri  
- `PlanetMoon` → Gezegen uyduları  
- `DwarfPlanet` → Cüce gezegenler  
- `Asteroid` → Asteroid verileri  
- `Astronaut` → Astronot bilgileri  

---
## 🔐 Veri Yönetimi Yaklaşımı

- Tüm veriler API üzerinden otomatik çekilir

- Veriler veritabanına cache amaçlı kaydedilir

- API hatası durumunda:

- Son başarılı veri kullanıcıya gösterilir

- Eski veriler belirli periyotlarla temizlenir

-Bu yapı sayesinde:

-✅ API limitleri korunur
-✅ Performans artar
-✅ Kullanıcı her zaman veri görebilir

## 🗂️ Uygulama Sayfaları (Routes) & Demo Görseller

- **`/` → Ana sayfa (ISS özet + gezegenler + son haberler + Son SpaceX Fırlatması)**
<img width="1517" height="906" alt="image" src="https://github.com/user-attachments/assets/b0b8f2ee-b8d7-492f-bd93-94cb4a58365a" />
<img width="1491" height="906" alt="image" src="https://github.com/user-attachments/assets/bdb09ebc-e7b4-48b3-84ad-f1889c05be72" />


- **`/iss/` → ISS takip ekranı**
<img width="1592" height="901" alt="image" src="https://github.com/user-attachments/assets/07b587af-19da-42ae-9ca9-fcd12747b1f5" />


- **`/astronauts/` → Astronotlar**
<img width="1540" height="903" alt="image" src="https://github.com/user-attachments/assets/e32f5fca-061b-4e97-893e-47c29b1f57b3" />


- **`/solar-system/` → Gezegenler**
<img width="1532" height="902" alt="image" src="https://github.com/user-attachments/assets/8b584267-1ea3-489a-a2dd-f7265eea65e7" />


- **`/planet-moons/` → Uydular**
<img width="1537" height="906" alt="image" src="https://github.com/user-attachments/assets/26af8a4e-0f14-46f9-b5db-4ff2cf49b310" />

- **`/dwarf-planets/` → Cüce gezegenler**
<img width="1542" height="906" alt="image" src="https://github.com/user-attachments/assets/5ae40a06-8d1c-49b9-a6c3-e4f568b02404" />


- **`/asteroids/` → Asteroidler**
<img width="1542" height="905" alt="image" src="https://github.com/user-attachments/assets/ee788268-b877-478d-aefb-9be2aea8149e" />


- **`/news/` → Uzay haberleri**
<img width="1536" height="907" alt="image" src="https://github.com/user-attachments/assets/43bbc08f-b1ba-4b13-a2ad-20ea59cc585d" />


---
## 🛠️ Kullanılan Teknolojiler

- Python 3.x  
- Django 5.0.8  
- SQLite  
- APScheduler  
- Requests  
- Django Template Engine  

> Projenin düzgün çalışması için gerekli kütüphaneleri de kurmanız gerekmektedir.
---

## ⚙️ Kurulum

```bash
git clone <repo-url>

python -m venv venv
venv\Scripts\activate   # Windows
# veya
source venv/bin/activate  # Linux / Mac

python manage.py makemigrations
python manage.py migrate

python manage.py runserver
```
---
## 👨‍💻 Geliştirici

**Yunus Güçlü**  
Software Engineer

---

## 📄 Lisans

Bu proje kişisel eğitim ve portföy amacıyla geliştirilmiştir.  
Ticari kullanım için geliştirici izni gereklidir.
