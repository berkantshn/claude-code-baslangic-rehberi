# 6. Güvenlik: .env, secret, public/private

Bu bölüm, başına gelebilecek en pahalı hatayı önlemek içindir: bir şifreyi veya anahtarı internete açık hale getirmek.

## Secret nedir?

**Secret**, başkasının eline geçmemesi gereken bilgidir: şifre, **API anahtarı** (bir servisi senin adına kullanmaya yarayan uzun kod), **token** (süreli erişim anahtarı), veritabanı bağlantı bilgisi.

Secret, dükkânının anahtarı gibidir. Ele geçiren kişi senin adına işlem yapabilir, verine ulaşabilir veya sana fatura çıkarabilir.

## .env: Secret'ların yeri

**.env**, secret'ların tutulduğu ve Git'e girmeyen özel dosyadır. Örnek:

```dotenv
API_ANAHTARI=buraya-gercek-deger-gelir
```

Kod bu değeri dosyadan okur. Böylece değer kodun içine yazılmaz.

**.env.example** ise aynı değişkenlerin değersiz şablonudur ve Git'e eklenir. Projeyi başka bilgisayarda açtığında neyin gerektiğini gösterir:

```dotenv
API_ANAHTARI=
```

## .gitignore: Git'e girmeyecekler listesi

**.gitignore**, Git'in görmezden geleceği dosyaların listesidir. Bu rehberin kendi taban listesi şudur:

```gitignore
node_modules/
__pycache__/
.venv/
dist/
build/
*.log
.DS_Store
.env
.env.*
!.env.example
```

Son üç satır: `.env` ve `.env.local` gibi dosyalar Git'e girmesin, ama `.env.example` girebilsin.

Çalıştığını şöyle doğrula:

```bash
git check-ignore -v .env
```

Bir `.gitignore` satırı görüyorsan dosya hariç tutuluyor demektir. Çıktı boşsa koruma yok, commit etme.

## Altın kurallar

1. Secret'ı koda, README'ye, commit mesajına veya PR açıklamasına yazma.
2. Commit etmeden önce `git status` listesini oku.
3. Secret'ı sohbete yapıştırma. Yapıştırdıysan sızmış say ve yenile.
4. Hata mesajını veya ekran görüntüsünü paylaşmadan önce içinde secret olup olmadığına bak.
5. Claude'dan şunu iste: "Bu değeri koda yazma, .env'den oku ve .env.example dosyasını güncelle."

Yerel oturum kayıtları da düz metin olarak `~/.claude/projects/` altında varsayılan olarak 30 gün tutulur ([resmî bilgi](https://code.claude.com/docs/en/data-usage)). `/feedback` ile paylaşılan konuşma kayıtları 5 yıl saklanır. Oturum anketinden sonra kayıt paylaşmak isteyip istemediğin sorulabilir: **Yes** dersen bilinen anahtar kalıpları temizlense de kaynak kod ve dosya içerikleri olduğu gibi yüklenir. Hassas bir projede bunları paylaşma.

## Claude'un .env okumasını engellemek

`CLAUDE.md`'ye "`.env` okuma" yazmak bir ricadır, kesin engel değildir. Kesin kural için **deny** (yasak) izin kuralı kullan. Proje içindeki `.claude/settings.json`:

```json
{
  "permissions": {
    "deny": ["Read(./.env)", "Read(./.env.local)", "Read(./secrets/**)"]
  }
}
```

Resmî [en iyi uygulamalar](https://code.claude.com/docs/en/best-practices) sayfasına göre bu kural dosya okuma aracını ve `cat .env` gibi yaygın komutları da yakalar, ama dosyayı açan bir **betiği** (otomatik çalışan küçük program) yakalamaz. Yani önemli bir katman olsa da mutlak değildir.

## Public mi, private mı?

| | Private | Public |
|---|---|---|
| Kim görür? | Sen ve izin verdiklerin | İnternetteki herkes |
| Kim kopyalayabilir? | İzin verdiklerin | Herkes |
| Ne zaman? | Varsayılan tercih | Paylaşmaya karar verip kontrol ettikten sonra |

**Private, kasa değildir.** Yine de secret koyma: repoya erişim izni verilen kişi veya uygulama görebilir, sonradan public yapabilirsin.

**Public yapınca geçmiş de açılır.** Yalnız son hali değil, bütün commit'ler görünür.

## Public yapmadan önce kontrol listesi

- [ ] `git log --all --oneline -- .env` çıktısı boş mu? Boş değilse `.env` geçmişe girmiş demektir.
- [ ] Geçmişte secret var mı? Claude'dan tarama iste ve kendin de bak. Araçlar her şeyi bulamaz.
- [ ] Müşteri adı, telefon, adres, iç belge veya özel not var mı?
- [ ] Görsel, yazı tipi ve metinleri kullanma hakkın var mı?
- [ ] README doğru mu? Sana ait olmayan iddia içeriyor mu?
- [ ] Mümkünse bilen birine göster.

Claude Code'un `/security-review` komutu, mevcut branch'teki değişikliklerde güvenlik riski arar. Yardımcıdır ama garanti vermez. Kullanmak için `origin` adlı bir **remote** (reponun GitHub'daki kopyası) gerekir.

## Secret sızarsa ne yapmalı?

Panik yapma, ama hızlı davran. Sıra önemlidir:

### 1. Hemen iptal et veya yenile

Secret'ı aldığın servisin paneline gir, anahtarı **iptal et (revoke)** veya **yenile (rotate)**. GitHub'ın [resmî rehberi](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) de ilk adım olarak bunu söyler. Eski anahtar çalışmıyorsa ele geçiren de kullanamaz.

Silmek veya repoyu private yapmak tek başına yetmez: birisi çoktan kopyalamış olabilir.

### 2. Zarar var mı bak

Servisin kullanım, fatura ve giriş kayıtlarını kontrol et. Tanımadığın bir hareket varsa servisin destek ekibine yaz. Kişisel veri etkilendiyse hukuki destek al.

### 3. Yeni değeri güvenli yere taşı

Yeni değeri `.env` dosyasına koy ve kodun oradan okumasını sağla. `.env` kazara Git'e eklendiyse takipten çıkar:

```bash
git rm --cached .env
```

Bu komut dosyayı Git takibinden çıkarır, bilgisayarındaki dosyayı silmez. **Önceki commit'lerden silmez.** `.gitignore`'a eklemeyi unutma.

### 4. Geçmişi temizlemeyi değerlendir

Sonraki commit'te silmek geçmişten silmez. Geçmişi temizlemek için GitHub, `git-filter-repo` aracını önerir. Ama bu işlem **geçmişi yeniden yazar**, **force push** (GitHub'daki geçmişin üzerine zorla yazma) gerektirir ve riskleri vardır:

- Commit kimlikleri değişir.
- Başkalarının kopyalarından ve **fork**'lardan (reponun başka hesaplardaki kopyaları) veri otomatik silinmez.
- GitHub'daki önbelleğe alınmış görünümler için destek talebi gerekebilir.

Anahtar iptal edildiyse bu adım her zaman gerekmeyebilir. Karar vermeden önce GitHub'ın rehberini oku, emin değilsen deneyimli birinden yardım al. Claude'a yaptıracaksan önce plan iste ve force push'u bilinçli onayla.

## Otomatik korumalar

- **Push protection:** GitHub, [bilinen secret türlerini](https://docs.github.com/en/code-security/secret-scanning/introduction/about-push-protection) public repolara push ederken engellemeye çalışır. Kullanıcılar için varsayılan olarak açıktır, ama her secret'ı yakalayamaz.
- **Dependabot uyarıları:** Kullandığın kütüphanelerde bilinen güvenlik açığı varsa [uyarı](https://docs.github.com/en/code-security/dependabot/dependabot-alerts/about-dependabot-alerts) verir. **Bağımlılık (dependency)**, projenin çalışmak için ihtiyaç duyduğu dış paket demektir.

Bu araçlar yardımcıdır, kontrolün yerini almaz.

---

[← Önceki: Git ve GitHub](05-git-ve-github.md) · [İçindekiler](../README.md) · [Sonraki: Onaylar ve riskli komutlar →](07-onaylar-ve-riskli-komutlar.md)

**Made By FALCREB**
