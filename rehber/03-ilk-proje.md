# 3. İlk proje: Küçük bir tanıtım sitesi

Bu bölümde hayali "Örnek Elektrik" için tek sayfalık bir site yapacağız. Hiçbir veritabanı, ödeme veya form olmayacak. İlk proje için en güvenli başlangıç budur.

Claude'un yanıtları ve oluşturduğu dosyalar her seferinde biraz farklı olabilir. Önemli olan adımları anlamaktır.

## Adım 1: Proje klasörünü oluştur

Terminalde sırayla çalıştır:

```bash
mkdir ornek-site
cd ornek-site
```

`mkdir` klasör oluşturur, `cd` o klasöre girer. Klasör adında boşluk kullanmamak komut yazmayı kolaylaştırır.

## Adım 2: Plan moduyla başlat

```bash
claude --permission-mode plan
```

**Plan modu**, Claude'un önce araştırıp plan önerdiği, plan onaylanana kadar dosya düzenlemediği çalışma biçimidir. Marangoza "kesmeden önce ölçüp çizimi göster" demek gibidir.

Klasöre güvenip güvenmediğin sorulursa, az önce kendin oluşturduğun için kabul edebilirsin.

## Adım 3: İsteğini yaz

Aşağıdaki metni kendine göre değiştirip gönder:

```text
Küçük bir elektrik işletmesi için tek sayfalık tanıtım sitesi yapmak istiyorum.

İçerik:
- İşletme adı: Örnek Elektrik
- Hizmetler: ev tesisatı, arıza onarımı, pano bakımı
- Telefon: 0000 000 00 00
- E-posta: ornek@example.com

Kurallar:
- Sadece HTML ve CSS kullan. JavaScript ve ek kütüphane ekleme.
- Telefonda da düzgün görünsün.
- Benim vermediğim bilgileri uydurma: tecrübe yılı, müşteri yorumu, adres yazma.
- Metinler Türkçe olsun.

Bana sade anlat. Kullandığın terimleri kısaca açıkla.
```

**HTML** sayfanın iskeletini, **CSS** ise görünüşünü belirler. **Kütüphane**, başkasının yazdığı hazır kod paketidir. Her eklenen kütüphane, takip edilmesi gereken yeni bir parça demektir, bu yüzden gerekmedikçe ekletmiyoruz.

## Adım 4: Planı oku

Claude bir plan sunar ve nasıl ilerleyeceğini sorar. Seçenekler şuna benzer:

- **Yes, and use auto mode:** Onayla, Claude rutin onay sormadan ilerlesin.
- **Yes, manually approve edits:** Onayla, her düzenlemeyi tek tek onayla.
- **No, keep planning:** Planda kal ve neyi değiştirmek istediğini söyle.

İlk projede **Yes, manually approve edits** seçeneğini öneririz. Yavaştır ama ne olduğunu görerek öğrenirsin.

## Adım 5: Onayları oku

Her onay ekranında üç şeye bak: hangi dosya, hangi değişiklik, başka bir yere dokunuyor mu? Anlamadığın bir şey varsa reddetmekten çekinme ve şunu yaz:

```text
Bu adımı neden yapmak istediğini sade bir dille açıkla.
```

## Adım 6: Sonucu gör

Klasördeki `index.html` dosyasına çift tıklayabilirsin. Ya da yeni bir terminal penceresinden proje klasöründeyken:

| Sistem | Komut |
|---|---|
| Windows | `start index.html` |
| macOS | `open index.html` |
| Linux | `xdg-open index.html` |

## Adım 7: Küçük adımlarla geliştir

Her seferinde tek şey iste:

```text
Hizmetler bölümünü alt alta değil, geniş ekranda üç sütun göster.
```

```text
Telefon numarasına tıklanınca arama başlasın.
```

Beğenmediğin bir değişikliği geri almak için `/rewind` kullanabilirsin ([10. bölüm](10-bir-sey-bozulunca.md)).

## Adım 8: Kendin kontrol et

Claude "bitti" dese de şu listeye sen bak:

- [ ] Telefon, e-posta ve işletme adı doğru mu?
- [ ] Senin vermediğin bir bilgi eklenmiş mi?
- [ ] Bütün bağlantılar çalışıyor mu?
- [ ] Tarayıcı penceresini daralttığında sayfa düzgün mü?
- [ ] Türkçe karakterler doğru görünüyor mu?
- [ ] Görsel kullanıldıysa kullanım hakkın var mı?

## Adım 9: Çalışmanı kaydet

```text
Bu klasörde Git başlat, .gitignore ekle ve yaptıklarımızı açıklayıcı bir mesajla commit et.
```

**Commit**, projenin o anki halini açıklamasıyla kayda geçirmektir. Ayrıntısı [5. bölümde](05-git-ve-github.md). Çıkmak için `/exit` yazabilirsin.

## Adım 10: Yayınlamak (isteğe bağlı)

Bu adım dosyalarını herkese açar, bu yüzden acele etme:

1. Önce [güvenlik bölümünü](06-guvenlik.md) oku.
2. Sitede gerçek telefon veya adres varsa bunun herkese açık olacağını kabul et.
3. Bir yayın yöntemi seç:
   - **Hosting firması:** Site dosyalarını barındıran ücretli hizmet. İşletme siteleri için genelde en net yol budur.
   - **GitHub Pages:** GitHub'ın **statik site** (hazır dosyalardan oluşan site) yayınlama hizmeti. GitHub Free'de public repolarda, Pro ve üzeri planlarda private repolarda da kullanılabilir. Repo private olsa bile yayınlanan site [internete açıktır](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

GitHub Pages'in [kullanım sınırları](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits) vardır. GitHub bu hizmetin çevrimiçi işletme yürütmek veya ticari işlem yapmak için ücretsiz barındırma olarak kullanılmasına izin vermediğini yazar. Gerçek işletmen için kullanmadan önce bu sayfayı oku.

**Forma dikkat:** Siteye iletişim formu eklersen kişisel veri toplamaya başlarsın. Bu durumda verilerin nerede tutulduğu, güvenliği ve [KVKK](https://www.kvkk.gov.tr/) yükümlülükleri gündeme gelir. Gerekirse uzmana danış. Basit bir tanıtım sitesinde telefon ve e-posta bağlantısı çoğu zaman yeterlidir.

---

[← Önceki: Kurulum](02-kurulum.md) · [İçindekiler](../README.md) · [Sonraki: İyi istek yazmak →](04-iyi-istek-yazmak.md)

**Made By FALCREB**
