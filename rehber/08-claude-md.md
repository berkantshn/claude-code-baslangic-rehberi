# 8. CLAUDE.md: Claude'un kalıcı talimatları

Her yeni Claude Code oturumu temiz bir hafızayla başlar. **CLAUDE.md**, her oturumun başında okunan talimat dosyasıdır. Yeni gelen bir çalışana verdiğin kısa kurallar kâğıdı gibi düşün: aynı şeyi her gün yeniden anlatmak zorunda kalmazsın.

**Markdown**, `#` başlık ve `-` liste gibi basit işaretlerle yazılan metin biçimidir. `.md` uzantısı buradan gelir.

## Nereye konur?

| Kapsam | Konum | Kim için |
|---|---|---|
| **Kullanıcı** | `~/.claude/CLAUDE.md` | Sen, bu bilgisayardaki tüm projeler |
| **Proje** | `./CLAUDE.md` veya `./.claude/CLAUDE.md` | Bu projede çalışan herkes (Git ile paylaşılır) |
| **Yerel** | `./CLAUDE.local.md` | Yalnızca sen, bu proje (`.gitignore`'a ekle) |

Kurumlar için bir de yönetilen politika dosyası vardır. Ayrıntı: [Claude projenizi nasıl hatırlar](https://code.claude.com/docs/en/memory).

## Hızlı başlangıç

Proje klasöründe, oturum içinde şunu yaz:

```text
/init
```

Claude projeyi inceleyip başlangıç dosyası önerir. Dosya zaten varsa üzerine yazmak yerine iyileştirme önerir. Sonra Claude'un kendi kendine bilemeyeceği kuralları ekle.

## Örnek proje dosyası

```markdown
# Örnek Elektrik sitesi

## İletişim
- Bana Türkçe ve sade anlat. Bir terimi ilk kullandığında kısaca açıkla.

## Proje
- Tek sayfalık statik site: index.html ve style.css
- Ek kütüphane eklemeden önce sor.

## Güvenlik
- Şifre ve API anahtarını koda yazma, .env kullan.
- .env dosyasını commit etme.
- Silme, force push ve repo görünürlüğü değişikliğinden önce sor.

## İş bitince
- Ne değiştiğini ve neyi nasıl kontrol edeceğimi madde madde yaz.
```

## İyi talimat nasıl yazılır?

Resmî dokümandan özet:

- **Kısa tut.** Dosya başına 200 satırın altı hedeflenir. Uzun dosyalar daha fazla yer kaplar ve daha az uyulur.
- **Somut yaz.** "Temiz yaz" yerine "Değişiklikten önce `git status` çalıştır" gibi.
- **Çelişme.** İki talimat çelişirse Claude birini rastgele seçebilir.
- **Tekrar eden düzeltmeleri ekle.** Aynı şeyi ikinci kez söylüyorsan dosyaya yazma zamanıdır.

## CLAUDE.md kesin kural değildir

Claude bu dosyayı **bağlam** (işi yaparken dikkate aldığı bilgi) olarak okur. Yani talimatlar genellikle uygulanır, ama kesin engel oluşturmaz. Olmazsa olmaz durumlar için [izin kurallarını](07-onaylar-ve-riskli-komutlar.md#kendi-kurallarını-yazmak) kullan.

## Dosyanın okunduğunu kontrol et

- `/context` yaz ve listede **Memory files** altında dosyanı gör.
- `/memory` ile dosyaları düzenleyebilirsin.
- Oturum sırasında CLAUDE.md'yi değiştirdiysen, değişiklik `/clear`, `/compact` veya yeniden başlatma sonrası devreye girer.

**Public repodaki CLAUDE.md herkese açıktır.** İçine secret, kişisel bilgi veya müşteri adı yazma.

## Auto memory

**Auto memory**, Claude'un düzeltmelerinden öğrenip kendi tuttuğu notlardır. Varsayılan olarak açıktır ve `~/.claude/projects/<proje>/memory/` altında durur. Bu notlar yalnızca o bilgisayardadır, diğer bilgisayarına geçmez. `/memory` ile görebilir ve kapatabilirsin.

## Kendi komutlarını yapmak

`/` ile başlayan kendi komutlarını oluşturabilirsin. Resmî dokümana göre komutlar artık **skill** (Claude Code'a eklenen talimat paketi) sistemiyle birleşmiştir ve iki biçim de çalışır:

| Biçim | Bu proje için | Tüm projelerin için |
|---|---|---|
| **Skill** (yeni işler için önerilen) | `.claude/skills/ozet/SKILL.md` | `~/.claude/skills/ozet/SKILL.md` |
| **Komut dosyası** (eski biçim) | `.claude/commands/ozet.md` | `~/.claude/commands/ozet.md` |

İkisi de `/ozet` komutunu oluşturur. Örnek `.claude/commands/ozet.md`:

```markdown
Bu projede son yapılanları sade Türkçeyle özetle: $ARGUMENTS
Hiçbir dosyayı değiştirme.
```

Kullanımı: `/ozet son 3 commit`. `$ARGUMENTS` yerine komuttan sonra yazdığın metin gelir. Ayrıntı: [Skills](https://code.claude.com/docs/en/skills).

## Hazır kural seti: Safe Vibe Coding Kit

Sıfırdan yazmak istemiyorsan [Safe Vibe Coding Kit](https://github.com/berkantshn/safe-vibe-coding-kit) reposuna bak. Bu rehberin tamamlayıcısıdır ve içinde şunlar var:

- Güvenlik, commit, branch + PR akışı ve onay gerektiren işlemler için genel `CLAUDE.md`
- Projeyi GitHub'a yükleyen `/yukle` komutu
- Nerede kaldığını salt okunur özetleyen `/devam` komutu

Kurmadan önce:

1. README'sini ve dosyaları oku. Başkasının kurallarını okumadan kurma.
2. Mevcut `~/.claude/CLAUDE.md` ve komutlarının **yedeğini al.** Kurulum aynı adlı dosyaların üzerine yazar.
3. Kuralları kendine göre düzenle. Kitin içinde sana ait olmayan tercihler olabilir.

Unutma: Bunlar yapay zekâ asistanına verilen talimatlardır, garanti değildir.

---

[← Önceki: Onaylar ve riskli komutlar](07-onaylar-ve-riskli-komutlar.md) · [İçindekiler](../README.md) · [Sonraki: Oturum devamlılığı →](09-oturum-devamliligi.md)

**Made By FALCREB**
