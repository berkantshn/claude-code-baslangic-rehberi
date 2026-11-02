# 9. Oturum devamlılığı

**Oturum (session)**, belirli bir klasöre bağlı, kaydedilen konuşmadır. Bilgisayarı kapatsan da kaldığın yerden devam edebilirsin. Ama birkaç sınırı bilmek gerekir.

## Kaldığın yerden devam etmek

Terminalde, proje klasöründeyken:

| Komut | Ne yapar |
|---|---|
| `claude --continue` (veya `claude -c`) | Bu klasördeki son oturumu açar |
| `claude --resume` (veya `claude -r`) | Oturum listesini açar |
| `claude --resume isim` | Adı verilen oturumu açar |

Oturum içinde:

| Komut | Ne yapar |
|---|---|
| `/resume` | Başka bir oturuma geçer |
| `/rename isim` | Oturuma ad verir, örneğin `/rename iletisim-bolumu` |

Ayrıntı: [Oturumları yönetmek](https://code.claude.com/docs/en/sessions).

## Bağlam: Claude'un masası

**Bağlam penceresi (context window)**, Claude'un o an aklında tutabildiği bilgi miktarıdır. Çalışma masası gibi düşün: masa doluyken ilgisiz kâğıtlar işi zorlaştırır.

| Komut | Ne yapar | Ne zaman |
|---|---|---|
| `/context` | Masanın doluluğunu gösterir | Merak edince |
| `/compact` | Konuşmayı özetleyerek yer açar | Aynı işe devam ederken |
| `/clear` | Boş bağlamla yeni konuşma açar | İlgisiz yeni işe geçerken |

`/clear` kullansan da eski konuşmaya `/resume` ile dönebilirsin. Konuşma temizlenince dosyaların değişmez.

## Sınırları

Oturum kayıtları kalıcı arşiv değildir:

- Oturum kayıtları **senin bilgisayarında** tutulur. Evdeki bilgisayarda açtığın konuşma kendiliğinden iş bilgisayarına geçmez. (Bulut oturumları ayrı çalışır: [resmî sayfa](https://code.claude.com/docs/en/claude-code-on-the-web).)
- Yerel kayıtlar varsayılan olarak **30 gün** sonra temizlenir.
- Auto memory notları da yalnızca o bilgisayardadır.

Bu yüzden önemli bilgi konuşmada kalmamalı. **Kalıcı olanı dosyaya yaz, kodu Git'e kaydet.**

## Pratik yöntem: PROGRESS.md

Burada anlatılan yöntem Claude Code'un özelliği **değildir**, kullanıcıların kurduğu basit bir alışkanlıktır. Projede `PROGRESS.md` adında bir not dosyası tutarsın, commit edersin ve başka bilgisayarda da okursun. Vardiya defteri gibi.

Örnek şablon:

```markdown
### 2 Kasım 2026

- **Yapılanlar ve kararlar:** İletişim bölümü eklendi. Form yerine telefon bağlantısı seçildi.
- **Son commit:** abc1234 feat: iletisim bolumu eklendi
- **Aktif branch:** main
- **Sıradaki ilk iş:** Hizmetler bölümündeki metinleri gözden geçirmek
- **Bilinen sorunlar:** Dar ekranda başlık biraz büyük
```

(`abc1234` örnek bir commit kimliğidir.) **Public repoda bu dosya da herkese açıktır.** Secret, müşteri bilgisi veya özel not yazma.

Oturum sonunda:

```text
PROGRESS.md dosyasını bugünkü işlerle güncelle, secret veya kişisel bilgi yazma.
```

Yeni oturum başında:

```text
PROGRESS.md dosyasını ve git durumunu oku. Nerede kaldığımı özetle. Hiçbir şeyi değiştirme.
```

Bilgi eski olabilir. Claude'dan notları gerçek Git durumuyla karşılaştırmasını da iste.

[Safe Vibe Coding Kit](https://github.com/berkantshn/safe-vibe-coding-kit) içindeki `/devam` komutu bu okuma işini, `/yukle` komutu ise yükleme akışını otomatikleştirir.

## Başka bilgisayarda devam etmek

1. Eski bilgisayarda: işini commit ve push et.
2. Yeni bilgisayarda: Repoyu al veya güncelle.

```bash
gh repo clone kullaniciadi/ornek-site
```

Daha önce aldıysan proje klasöründe:

```bash
git fetch
git status
git pull --ff-only
```

3. `.env` dosyası Git'te olmadığı için yeni bilgisayarda yeniden oluştur. Hangi değişkenlerin gerektiğini `.env.example` gösterir. Değerleri mesajla veya e-postayla düz metin göndermek yerine güvenilir bir şifre yöneticisi kullan.
4. `claude` ile başlat ve `PROGRESS.md`'yi okut.

---

[← Önceki: CLAUDE.md](08-claude-md.md) · [İçindekiler](../README.md) · [Sonraki: Bir şey bozulunca →](10-bir-sey-bozulunca.md)

**Made By FALCREB**
