# 1. Claude Code nedir?

**Claude Code**, Anthropic şirketinin geliştirdiği, yazılım projelerinde çalışan bir yapay zekâ aracıdır. Resmî tanımıyla bir **ajandır** (agent: kendisine verilen işi adım adım yürüten yapay zekâ). Proje dosyalarını okur, değiştirir ve bilgisayarında komut çalıştırır.

Normal bir sohbet botu sana tarif verir, uygulamak sana kalır. Claude Code ise eline aleti alıp işi yapan bir yardımcı gibidir. Ama işin sahibi sensin: ne istediğini söylemek ve sonucu kontrol etmek senin görevin.

## Nerede çalışır?

| Yer | Kısaca |
|---|---|
| **Terminal** | Yazıyla komut verilen pencere. Bu rehber çoğunlukla bunu anlatır. |
| **Masaüstü uygulaması** | Terminal istemeyenler için görsel arayüz. Claude uygulamasındaki **Code** sekmesi. |
| **VS Code ve JetBrains** | Kod editörlerinin içinde. |
| **Tarayıcı** | [claude.ai/code](https://claude.ai/code) üzerinden bulutta çalışır. |

Güncel liste için: [Platformlar](https://code.claude.com/docs/en/platforms).

## Yazılımcı olmak gerekir mi?

Resmî [terminal rehberi](https://code.claude.com/docs/en/terminal-guide), daha önce terminal kullanmamış kişiler için yazılmıştır. Yani başlamak için yazılımcı olman gerekmez.

Yine de sihir beklememek gerekir. Kod yazmayı bilmesen de şunları öğrenmen gerekir:

- Ne istediğini net anlatmak
- Git ile çalışmanı kayıt altına almak
- Onay ekranlarını okumak
- Şifre gibi bilgileri korumak

Bu rehber tam olarak bunları anlatır.

## Ücretli mi?

Evet, kullanmak için uygun bir hesap gerekir. Resmî dokümana göre **ücretsiz claude.ai planı Claude Code içermez.** Şu hesaplardan biri gerekir:

- Pro, Max, Ultra, Team veya Enterprise aboneliği
- **Claude Console** hesabı (ön ödemeli kredi ile, kullandığın kadar öde)
- Şirketler için Amazon Bedrock, Google Cloud veya Microsoft Foundry erişimi

Fiyatlar ve planlar değişebildiği için burada rakam vermiyoruz. Güncel bilgi için: [claude.com/pricing](https://claude.com/pricing).

Kullanım miktarın için oturum içinde `/usage` yazabilirsin. Maliyet hakkında ayrıntı: [Maliyet yönetimi](https://code.claude.com/docs/en/costs).

Claude Code yalnızca [desteklenen ülkelerde](https://www.anthropic.com/supported-countries) kullanılabilir. Bu rehberin kontrol edildiği tarihte (2 Kasım 2026) Türkiye listededir.

## Neler yapabilir?

- Web sitesi, küçük uygulama, bot, hesap aracı veya otomasyon yazabilir.
- Projedeki bir hatayı arayıp düzeltebilir.
- Git işlemlerini senin yerine yapabilir.
- Mevcut bir projeyi sana sade dille açıklayabilir.

## Sınırları neler?

Bunu baştan bilmek en önemli konudur:

- **Yanılabilir.** Kendinden emin bir dille yanlış şey söyleyebilir, olmayan bir özelliği varmış gibi anlatabilir veya "bitti" deyip eksik bırakabilir.
- **Sonuçtan sen sorumlusun.** Resmî [güvenlik sayfası](https://code.claude.com/docs/en/security), önerilen kod ve komutları onaylamadan önce gözden geçirmenin kullanıcının sorumluluğu olduğunu açıkça yazar.
- **Bir şeyi yayınlamadan önce kontrol et.** Çalışıyor görünmek, güvenli olduğu anlamına gelmez.

### Ne zaman bir uzmana danışmalısın?

Aşağıdaki işlerde yapay zekâya ve bu rehbere tek başına güvenme, bir uzmandan destek al:

- Gerçek müşterilerin kullanacağı, durması zarar verecek sistemler
- Ödeme alan, kullanıcı girişi olan veya kişisel veri toplayan uygulamalar
- Güvenlik denetimi gerektiren işler
- Hukuk, vergi ve sözleşme konuları (Türkiye'de kişisel veriler için bkz. [KVKK](https://www.kvkk.gov.tr/))
- Sağlık konuları ve insan güvenliğini ilgilendiren hesaplar

## Verilerin ne oluyor?

Claude Code, işi yapmak için okuduğu içerikleri modele gönderir. Bu nedenle müşteri listesi veya kişisel veri içeren dosyaları olduğu gibi kullanmadan önce düşün.

Resmî [veri kullanım sayfasına](https://code.claude.com/docs/en/data-usage) göre:

- **Free, Pro, Max ve Ultra** hesaplarında verilerinin model eğitiminde kullanılıp kullanılmayacağı senin ayarına bağlıdır. Ayarı [gizlilik ayarları](https://claude.ai/settings/privacy) sayfasından görebilirsin.
- **Team, Enterprise ve API** (programların bir servise bağlandığı kapı) gibi ticari kullanımlarda, müşteri kendi isteğiyle katılmadıkça kod ve istemler model eğitiminde kullanılmaz.

Koşullar değişebilir, emin olmak için resmî sayfayı oku.

## Sıradaki adım

Bu rehberle birlikte kullanabileceğin hazır kural seti: [Safe Vibe Coding Kit](https://github.com/berkantshn/safe-vibe-coding-kit). Ayrıntısını [CLAUDE.md bölümünde](08-claude-md.md) anlatıyoruz.

---

[İçindekiler](../README.md) · [Sonraki: Kurulum →](02-kurulum.md)

**Made By FALCREB**
