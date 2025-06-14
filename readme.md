# HR App

Bu doküman, Mid seviyede iOS geliştirici pozisyonu için hazırlanmış olup, projenin genel yapısını, teknik gereksinimlerini ve geliştirilmesi gereken özellikleri detaylı şekilde açıklamaktadır. Adayın proje kapsamını ve beklentileri net olarak anlaması amaçlanmıştır.

---

Modern İK ekipleri için geliştirilmiş, aday değerlendirme ve işe alım süreçlerini kolaylaştırmayı amaçlayan bir mobil uygulama.

## 👨‍💻 Geliştirici
**Rol:** Mid iOS Developer

---

## 📘 İçindekiler

- [📖 Giriş](#giriş)
- [⚙️ Gereksinimler](#gereksinimler)
- [✨ Nice to Have Özellikler](#nice-to-have-özellikler)
- [📂 API Örnekleri](#api-örnekleri)
- [🚀 Özellikler](#özellikler)
  - [🎬 Launch Screen](#launch-screen)
  - [💧 Splash Screen](#splash-screen)
  - [🛳️ Onboard](#onboard)
  - [🔐 Login](#login)
  - [🔢 OTP](#otp)
  - [🏠 Home](#home)
  - [⚙️ Settings](#settings)
  - [🍽️ Cafeteria](#cafeteria)

---

## 📖 Giriş

**HR App**, birden fazla markaya kolayca uyarlanabilecek esnek bir yapıda tasarlanmıştır. Amaç, yalnızca marka kimliğine uygun tasarımlar giydirilerek, minimum geliştirme ile farklı pazarlarda kullanılabilecek bir İnsan Kaynakları uygulaması sunmaktır.

---

## ⚙️ Gereksinimler

- **Mimari:** MVVM-R (Model-View-ViewModel - Router)
- **Branch Yapısı:**
  - `feature/hrapp-000-feature-name`
  - `bug/hrapp-000-fix-description`
  - **Commit Örneği:** `HRAPP-101 Login ekranı tasarlandı.`
- **Geliştirme:** Mevcut proje üzerinden devam edilecektir.
- **Swift Package Manager (SPM)** (Swift'in paket yönetim aracı)
- **Minimum iOS Sürümü:** iOS 15+
- **Dil Desteği:** Türkçe & İngilizce (JSON tabanlı lokalizasyon)
- **Karanlık Mod (Dark Mode)** desteği
- **Layout:** Auto Layout ile responsive tasarım
- **Geliştirme Yöntemi:** Programmatic veya XIB
- **Servis Katmanı:** DataProvider isim bir spm package içerisinde bulunmalıdır. (Alamofire ile bir alt yapı kurulmalıdır.)
- **SwiftLint Kurulumu:** Projede SwiftLint kurulumu yapılmalıdır.
- **Deeplink:** Uygulama içerisinde farklı ekranlara yönlendirme için deeplink mekanizması kullanılacaktır. (Scheme: loodosCase)
- **Firebase:** Remote Config, Crashlytics ve Analytics entegre edilmelidir.

---

## ✨ Nice to Have Özellikler
- Lottie animasyonları
- Dev / Preprod / Prod şema yapısı
- SwiftGen Kurulumu
- Github Actions Entegrasyonu

Not: Bu özellikler zorunlu olmamakla birlikte, projeye değer katacaktır.

---

## 📂 API Örnekleri

Proje içerisinde kullanılan API çağrıları için aşağıdaki CURL örnekleri referans alınabilir. Her özellik bölümünde tekrar eden CURL örnekleri yerine bu bölümdeki örnekler kullanılacaktır.

```bash
curl -X POST https://api.dev.hrapp.com/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "test.case",
    "password": "123123"
  }'
```

---

## 🚀 Özellikler

### 🎬 Launch Screen
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- **Task Kodu:** `HRAPP-000`
- Auto Layout uyumlu
- Dark Mode desteği
- Uygulama bu ekranla başlamalı

---

### 💧 Splash Screen
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- **Task Kodu:** `HRAPP-001`
- API örnekleri için bkz. "API Örnekleri" bölümü.
- Auto Layout ile tüm cihaz boyutlarına uyumlu tasarım
- Dark Mode desteği
- Launch sonrası gösterilir
- Genel Akış:
    - Uygulama Launch Screen sonrasında SplashViewController üzerinden başlar.
    - Yukarıdaki API örneği ile belirtilen API'ye istek göndererek ilgili JSON verisini alabilirsiniz.
    - Bu JSON dosyasındaki key–value verileri, lokalizasyon amaçlı kullanılacaktır.
    - Çekilen JSON dosyası cihazın yerel deposunda (örneğin UserDefaults veya dosya sistemi) saklanmalıdır.
    - Yönlendirme Kuralları:
        - Eğer kullanıcı onboard ekranlarını daha önce görmemişse, uygulama Onboard ekranına yönlendirilmelidir.
        - Kullanıcı giriş yaptıysa, doğrudan Anasayfa (Home) ekranına yönlendirilmelidir.
        - Kullanıcı giriş yapmadıysa, Login ekranına yönlendirilmelidir.
    - Uygulama açıldığında kullanıcının dil dosyasını çekebilmesi için dikkat edilmesi gerekenler:
        - Uygulama yüklendiğinde eğer cihaz dili Türkçe değilse en-US, eğer Türkçe ise tr-TR olarak localizable dosyası çekilmelidir.

---

### 🛳️ Onboard
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- **Task Kodu:** `HRAPP-002`
- API örnekleri için bkz. "API Örnekleri" bölümü.
- Auto Layout ile tüm cihaz boyutlarına uyumlu tasarım
- Dark Mode desteği
- Genel Akış:
    - Yukarıdaki API örneği ile belirtilen API'den alınan JSON verisi Splash ekranında çekilip Onboard ekranına aktarılmalıdır.
    - Resimler yüklenirken iOS native loading mekanizması kullanılmalıdır.
    - Görseller yüklenirken hata alınırsa, tasarımdaki placeholder görsel gösterilmelidir.
    - Resimler cache'lenmelidir; böylece kullanıcı Onboard ekranını tekrar gördüğünde yeniden indirilmelerine gerek kalmaz.
    - Kullanıcı Onboard ekranında geri butonunu kullanarak çıkış yapmamalıdır.
    - Kullanıcı "Devam Et" butonuna bastığında, bir sonraki Onboard sayfası gösterilmelidir.
    - Kullanıcı "Atla" (Skip) butonuna basarsa, doğrudan Login ekranına yönlendirilmelidir.
    - Kullanıcı son Onboard ekranındaysa ve "Devam Et" butonuna basarsa, Login ekranına yönlendirme yapılmalıdır.
    - Onboard ekranlarında her bir sayfa için belirli bir süre (örneğin 5 saniye) tanımlanmalı ve bu süre sonunda otomatik olarak bir sonraki sayfaya geçilmelidir. Bu süreyi yöneten bir timer mekanizması entegre edilmelidir. Kullanıcı manuel olarak "Devam Et" butonuna basarsa, timer sıfırlanarak bir sonraki sayfada yeniden başlatılmalıdır.
- **Nice to Have:**
  - Firebase Event Yollama (onboard_skipped, onboard_continue)

---

### 🔐 Login
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- **Task Kodu:** `HRAPP-003`
- **Test Kullanıcı Bilgileri:**  
  `username: test.case`, `password: 123123`
- API örnekleri için bkz. "API Örnekleri" bölümü.
- Tüm cihaz boyutlarına uyumlu Auto Layout tasarımı
- Dark Mode desteği

- Genel Akış:
  - Kullanıcı adı alanı minimum 3, maksimum 50 karakter olmalıdır.
  - Şifre alanı minimum 6, maksimum 20 karakter olmalıdır.
  - Tüm giriş alanlarında emoji kullanımı engellenmelidir.
  - Herhangi bir giriş alanında doğrulama hatası mevcutsa, "Giriş Yap" butonu pasif durumda olmalıdır.
  - Hatalı alanların altında kullanıcıya durumu açıklayan bilgilendirici metin gösterilmelidir.  
    Örnek: `Kullanıcı adı en az 3 karakter olmalıdır.`
  - Giriş başarılı olduğunda kullanıcı OTP ekranına yönlendirilmelidir.
  - Login isteğinden dönen response verileri OTP ekranına aktarılmalıdır.
    - Bu veri aktarımı ve yönlendirme işlemi için örnek bir kod parçası sağlanacaktır.
    - pushOTP(expiresIn: Int?) kullanılarak değeri taşıyabilirsiniz.

- **Nice to Have:**
  - Firebase üzerinden login başarılı/başarısız event'lerinin gönderilmesi
  - Giriş alanlarının yeniden kullanılabilir (reusable) component yapısında tasarlanması

---

### 🔢 OTP
- **Task Kodu:** `HRAPP-004`
- **Test Kullanıcı Bilgileri:**  
  `otp: 12345`
- Tüm cihaz boyutlarına uyumlu Auto Layout tasarımı
- Dark Mode desteği

- Genel Akış:
  - Kullanıcı, klavyedeki otomatik öneri (AutoFill) özelliğiyle tek kullanımlık kodu kolayca girebilmelidir.
  - Tasarıma uygun bir progress bar bulunmalı ve login yanıtında dönen `expiresIn` süresi kadar geri sayım yapmalıdır.
  - OTP alanına `"12345"` yazılıp "Giriş Yap" butonuna basıldığında işlem başarılı kabul edilir.
  - "Giriş Yap" butonu yalnızca tüm OTP input alanları doluysa aktif hale gelmelidir.
  - Kullanıcı, geri butonuyla Login ekranına dönebilmelidir.
  - Uygulama arka plana alındığında geri sayım durmamalı; örneğin, 30. saniyede arka plana alınıp 20 saniye sonra geri dönüldüğünde, sayaç 10. saniyeden devam etmelidir.
  - Giriş işlemi başarılı olduğunda kullanıcı Home ekranına yönlendirilmelidir.

 - **Nice to Have:**
  - Firebase üzerinden otp_success ve otp_error event’lerinin gönderilmesi
  - OTP input alanlarının yeniden kullanılabilir (reusable) bir component olarak tasarlanması

---

### 🏠 Home
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- **Task Kodu:** `HRAPP-005`
- API örnekleri için bkz. "API Örnekleri" bölümü.
- Tüm cihaz boyutlarına uyumlu Auto Layout tasarımı
- Dark Mode desteği
- CollectionView ile geliştirme yapılacaktır.
   - Banner 10 saniyede bir otomatik olarak scroll etmelidir.
   - Bannerlardaki görseller, kullanıcıya hızlı yüklenme hissi verecek şekilde optimize edilmelidir. Bu nedenle, sayfa ilk açıldığında yalnızca 0. indexteki görsel değil, aynı anda 1. ve 2. indexteki görseller de önceden yüklenmelidir.
   - Örneğin; kullanıcı 2. indexteki görseli görüntülerken, arka planda 3. ve 4. indexteki görsellerin yüklenmesi başlatılmalıdır.
   - Eğer son banner gösteriliyorsa, 10 saniye sonra tekrar en başa dönmelidir (sonsuz döngü).
- CollectionView Cell kullanılmamalıdır. Tarafınıza verilen özel sınıf kullanılarak entegrasyon yapılmalıdır.  
  Kullanılacak sınıf: `LCGenericCollectionViewCell`

  ```swift
  let cell: LCGenericCollectionViewCell<ExampleView> = collectionView.dequeueReusableCell(for: indexPath)
    let view = ExampleView()
    view.set(viewModel: cellModel)
    cell.cellView = cellView
  return cell
  ```
 - Kullanıcı Banner’a tıkladığında detay sayfasına yönlendirilmelidir.
 - Detay sayfasında kullanıcının tıkladığı resmi göstermek yeterli olacaktır.
 - Maslak Otopark bileşeni bir servis isteğiyle durumunu göstermelidir ("BOŞ" veya "DOLU").
   - Servis yanıtında dönen süre (örneğin 60 saniye) kadar bekleyip yeniden istek atılmalıdır.
   - Eğer servisten gelen süre “0” ise, tekrar istek atılmamalıdır (timer durdurulmalıdır).
 - Kullanıcı bu ekrandan geri dönüş yapmamalıdır.
 - Ekran, TabBar’da yer almalıdır. (MainTabBarViewController)

- **Nice to Have:**
  - Firebase click_banner, refresh_carpark, stop_timer, click_home_tab eventleri.

---

### ⚙️ Settings
- **Task Kodu:** `HRAPP-006`
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- TabBar’da erişilebilir bir sayfa olarak gösterilmelidir.
- Kullanıcı, "Dil Değiştir" butonuna tıkladığında bir sheet açılmalı ve buradan dil seçimi yapabilmelidir.
- Seçim yapıldığında bir loading göstergesi çıkarılmalı ve uygulama dili anlık olarak değişmelidir.
  - Bu değişiklik, kullanıcı Settings ekranından çıkmadan gerçekleşmelidir.
- Eğer cihaz dili Türkçe değilse, varsayılan dil İngilizce olarak ayarlanmalıdır.
- Kullanıcı "Çıkış Yap" butonuna bastığında, Login ekranına yönlendirilmelidir.

- **Nice to Have:**
  - Firebase logout event’i

---

### 🍽️ Cafeteria
- **Task Kodu:** `HRAPP-007`
- [Figma Linki](https://www.figma.com/design/MbORukxK22gzWuvYmP41Vv/Supa-Resume---Light---Dark--FREE-Resume-Cover-Letter---Community-?node-id=33-5366)
- API örnekleri için bkz. "API Örnekleri" bölümü.
- TabBar’da erişilebilir bir sayfa olarak gösterilmelidir.
- Sayfa açıldığında TabBar gizlenmelidir.
- Daily Menus ve food list apisinde gelen veriler tasarımda ki gibi tek bir sayfada listelenecektir.
- Kullanıcı, menü listesinde yer alan bir menü öğesinin yanındaki "+" butonuna tıkladığında, ekranda "Menüye tıklandı" mesajı gösteren bir toast bildirimi çıkmalıdır.
- Kullanıcı, herhangi bir yemek öğesinin yanındaki "+" butonuna tıkladığında ise, ekranda "Yemek sepete eklendi" mesajı gösteren bir toast bildirimi çıkmalıdır.
- Her iki toast bildirimi de kullanıcı etkileşiminden hemen sonra kısa süreli olarak gösterilmeli ve ardından otomatik olarak kaybolmalıdır.

- **Nice to Have:**
  - Firebase event: cafeteria_viewed, cafeteria_refreshed

## 📎 Ek Bilgi

- Localizasyon yaparken servisten gelen keylere gösterim yapacağız. Json dosyasında tüm textler hazır olacaktır, uygun keyi kullanmanız yeterli olacaktır. ("login_title" : "Hoşgeldiniz")
- Servislerden eğer 401 gelirse uygulama Logine yönlenmelidir ve kullanıcı bilgileri silinmelidir.

---

> Bu proje, minimum geliştirme ile farklı marka ihtiyaçlarına uyum sağlamayı hedefleyen, ölçeklenebilir ve modüler bir yapı üzerine kurulmuştur.

## 🛠 Yapılan İyileştirme ve Düzeltilen Buglar

Bu bölümde proje kapsamında geliştirilen iyileştirmeler ve tespit edilen/çözülen buglar listelenecektir. Eğer projede geliştirme sırasında fark ettiğiniz bug, performans sorunu veya başka bir problem varsa, lütfen buraya ekleyin.

- [ ] Örnek: Splash ekranında gereksiz API çağrısı kaldırıldı.
- [ ] Örnek: Onboard ekranında görsel cache mekanizması iyileştirildi.
- [ ] [Eklemek için buraya not alın...]
