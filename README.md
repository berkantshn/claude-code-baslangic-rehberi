# Claude Code Türkçe Rehber

**Yazılımcı olmayanlar için sade, pratik ve dürüst bir Claude Code başlangıç rehberi.**

> **Bu, gayriresmî bir topluluk rehberidir. Anthropic ile bağlantılı değildir, Anthropic tarafından hazırlanmamış veya onaylanmamıştır.**

*English summary is [below](#english-summary).*

Elektrikçi, küçük işletme sahibi veya öğrenci olabilirsin. Kod bilmiyor ama gerçek bir proje yapmak istiyorsan bu rehber senin için. Terimlerden kaçmıyoruz, ama her birini ilk geçtiği yerde açıklıyoruz.

Rehberi, projelerini bu yöntemle geliştiren bir elektrik mühendisi hazırladı. Yazımında Claude Code'dan yardım alındı ve ürün bilgileri resmî dokümanlarla karşılaştırıldı.

## İçindekiler

| # | Bölüm | Ne öğreneceksin |
|---|---|---|
| 1 | [Claude Code nedir?](rehber/01-claude-code-nedir.md) | Ne yapar, ne gerektirir, sınırları neler |
| 2 | [Kurulum](rehber/02-kurulum.md) | Windows, macOS, Linux ve ilk giriş |
| 3 | [İlk proje](rehber/03-ilk-proje.md) | Adım adım küçük bir tanıtım sitesi |
| 4 | [İyi istek yazmak](rehber/04-iyi-istek-yazmak.md) | Claude'a işi doğru anlatmak |
| 5 | [Git ve GitHub](rehber/05-git-ve-github.md) | Commit, branch, PR ve merge |
| 6 | [Güvenlik](rehber/06-guvenlik.md) | `.env`, secret, public/private, sızıntıda ne yapılır |
| 7 | [Onaylar ve riskli komutlar](rehber/07-onaylar-ve-riskli-komutlar.md) | İzin modları ve dikkat edilecek komutlar |
| 8 | [CLAUDE.md](rehber/08-claude-md.md) | Kalıcı talimatlar ve kendi komutların |
| 9 | [Oturum devamlılığı](rehber/09-oturum-devamliligi.md) | Kaldığın yerden, başka bilgisayarda devam |
| 10 | [Bir şey bozulunca](rehber/10-bir-sey-bozulunca.md) | Durdurma, anlama ve geri alma |
| 11 | [Sık yapılan hatalar](rehber/11-sik-yapilan-hatalar.md) | 20 hata ve çözümü |
| 12 | [Terimler sözlüğü](rehber/12-terimler-sozlugu.md) | Rehberdeki terimler |

Sırayla okumanı öneririz. Acelen varsa en azından 2, 3, 6 ve 7. bölümleri oku.

## Beş temel kural

1. **Küçük adımlarla ilerle.** Her adımı dene ve Git ile kaydet.
2. **Yeni başlıyorsan Manual modda çalış.** Claude Code yeni sürümlerde auto modda başlar ve her şeyi sormayabilir. ([7. bölüm](rehber/07-onaylar-ve-riskli-komutlar.md))
3. **Secret'ları `.env` dosyasında tut.** Sızdıysa önce anahtarı iptal et. ([6. bölüm](rehber/06-guvenlik.md))
4. **Anlamadığını onaylama.** Reddetmek bir şey bozmaz, açıklama iste.
5. **Yayınlamadan önce kendin kontrol et.** Yapay zekâ yanılabilir.

## Dürüst olalım: Sınırlar

- Yapay zekâ yanılabilir, bilgi uydurabilir veya "bitti" deyip eksik bırakabilir. Bu rehber de hata içerebilir.
- Bu rehber profesyonel, hukuki, tıbbi veya güvenlik danışmanlığı değildir.
- Gerçek kullanıcıların kullandığı canlı sistemlerde, ödeme veya kişisel veri söz konusu olduğunda, güvenlik denetiminde ve hukuki ya da tıbbi açıdan kritik işlerde **bir uzmandan destek al.**

## Güncellik

Ürün bilgileri **2 Kasım 2026** tarihinde resmî dokümanlarla karşılaştırıldı. Claude Code hızlı değişiyor. Fark görürsen resmî doküman esastır. Fiyat vermiyoruz, güncel bilgi için [claude.com/pricing](https://claude.com/pricing).

Resmî kaynaklar:

- [Claude Code dokümantasyonu](https://code.claude.com/docs/en/overview)
- [Terminal rehberi](https://code.claude.com/docs/en/terminal-guide)
- [Claude Code 101 kursu](https://academy.claude.com/courses/claude-code-101)
- [GitHub dokümantasyonu](https://docs.github.com/)

## Tamamlayıcı proje

[**Safe Vibe Coding Kit**](https://github.com/berkantshn/safe-vibe-coding-kit): Yazılımcı olmadan Claude Code ile proje geliştirenler için hazır kural seti ve iki komut (`/yukle`, `/devam`). Bu rehber nedenini ve nasılını anlatır, kit ise hazır kuralları verir. Kurmadan önce [8. bölümü](rehber/08-claude-md.md#hazır-kural-seti-safe-vibe-coding-kit) oku.

## Katkı

Hata veya eskimiş bilgi görürsen issue aç. Mümkünse resmî kaynak bağlantısı ekle. Örneklere gerçek kişi, müşteri veya secret bilgisi yazma.

## Lisans

Rehber metni [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE) lisansı ile sunulur. Atıf: **FALCREB**.

"Claude" ve "Claude Code" Anthropic'e, "GitHub" ise GitHub, Inc.'e aittir. Bu adlar yalnızca ürünleri tanımlamak için kullanılmıştır.

---

## English summary

A beginner's guide to Claude Code, written in simple Turkish for people who are not developers, such as electricians, small business owners and students who want to build a real project. **This is an unofficial community guide. It is not affiliated with or endorsed by Anthropic.**

It has 12 short chapters: what Claude Code is, installation, a first small website, writing good requests, Git and GitHub, security (`.env`, secrets, leaks), permission modes and risky commands, `CLAUDE.md`, session continuity, recovering when things break, common mistakes and a glossary.

Product facts were compared with the official documentation on 2 November 2026 and may have changed since then. AI can be wrong, so review before publishing and get expert help for production, security, legal or medical-critical work. It is a companion to the [Safe Vibe Coding Kit](https://github.com/berkantshn/safe-vibe-coding-kit).

Licence: the guide text is licensed under [CC BY 4.0](LICENSE). Attribution: FALCREB.

## ⭐ Support this project

If this project helped you, please give it a ⭐ and [follow me on GitHub](https://github.com/berkantshn) for more.

İşine yaradıysa projeye ⭐ verip [beni GitHub'da takip edebilirsin](https://github.com/berkantshn).

---

**Made By FALCREB**
