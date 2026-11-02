# 4. İyi istek yazmak

Claude'a yazdığın isteğe **prompt** denir. Claude senin kafandakini, işletmeni veya müşterini bilemez. İyi bir istek, bu eksik bilgiyi tamamlar. Bir ustaya iş tarif eder gibi düşün: "Şurayı düzelt" yerine ne, nerede, ne zaman olmuş diye anlatırsın.

## Dört soruluk kalıp

1. **Ne istiyorum?** Sonuç ne olacak?
2. **Nerede?** Hangi dosya, sayfa veya bölüm?
3. **Sınırlar ne?** Neye dokunmamalı, ne eklememeli?
4. **Nasıl anlayacağız?** Bittiğini gösteren kontrol nedir?

## Örnekler

| Zayıf | Daha iyi |
|---|---|
| Siteyi düzelt. | Telefonda iletişim bölümü ekrandan taşıyor. `index.html` ve `style.css` dosyalarına bak, 360 piksel genişlikte taşmayacak şekilde düzelt. Başka bölümü değiştirme. |
| Hesap aracı yap. | Fatura tutarına KDV ekleyen tek sayfalık bir araç yap. Oran kutudan girilsin, sonuç anında görünsün. Sadece tarayıcıda çalışsın, veri kaydetmesin. Doğruluğu kontrol edebileceğim üç örnek hesap da göster. |
| Hata veriyor. | `pnpm dev` komutunda şu hatayı alıyorum: (hatanın tam metni). Son olarak kütüphane güncellemiştim. Önce nedenini anlat, onaylarsam düzelt. |

## Elindeki malzemeyi ver

- **Dosya:** `@` yazıp dosya yolunu seç, örneğin `@index.html`.
- **Ekran görüntüsü:** Hatanın veya beğendiğin düzenin görselini yapıştır.
- **Hata mesajı:** Özetleme, tam metnini kopyala. Ama içinde şifre veya anahtar varsa önce sil.

## Büyük işi böl

Tek istekte "tam bir uygulama yap" demek yerine işi parçalara ayır:

```text
1. Önce ana sayfayı yapalım.
2. Sonra hizmetler sayfasını ekleyelim.
3. En son iletişim bilgilerini ekleyelim.
Şimdilik sadece 1. adımı yap ve dur.
```

Her adım sonunda çalıştığını kontrol et ve [commit](05-git-ve-github.md) ile kaydet.

## Emin değilsen önce sor

Değişiklik yaptırmadan önce plan moduna geçebilirsin: `Shift + Tab` veya tek bir istek için `/plan`. Örnek sorular:

```text
/plan Siteye randevu sistemi eklemek istiyorum. Bana seçenekleri, riskleri ve maliyetleri sade dille anlat.
```

```text
Bu proje ne yapıyor ve klasörler ne işe yarıyor? Hiçbir dosyayı değiştirme.
```

```text
Bana bu işi yapmadan önce gerekli soruları sor.
```

## Claude'a kontrol imkânı ver

Resmî [en iyi uygulamalar](https://code.claude.com/docs/en/best-practices) sayfası, Claude'a sonucu geçti/kaldı şeklinde gösteren bir kontrol vermeyi önerir. Yazılımda buna **test** denir (kodun beklendiği gibi çalıştığını otomatik kontrol eden küçük program). Örnek:

```text
KDV hesabı için test yaz: 100 TL ve %20 için sonuç 120 TL olmalı. Testleri çalıştır ve çıktısını bana göster.
```

Claude "testler geçti" derse çıktıyı görmeden kabul etme. Tutarların doğru olup olmadığını da kendin kontrol et.

## Yoldan çıktığında

Resmî öneri basittir: ilk dakikayı izle, yoldan çıktığı anda `Esc` ile durdur. İki düzeltmeye rağmen hâlâ yanlışsa üçüncüyü yazma. `/clear` ile temiz bir konuşma aç ve öğrendiklerini içeren daha iyi bir istek yaz.

Birbiriyle ilgisiz işlere geçerken de `/clear` kullanmak iyi bir alışkanlıktır.

## Doğrulatmak için hazır cümleler

```text
Yaptığın değişiklikleri sade dille özetle. Neyi kontrol etmemi önerirsin?
```

```text
Bu çözümün riskleri ve zayıf yanları neler? Emin olmadığın noktaları açıkça söyle.
```

```text
Bu bilgiyi resmî dokümandan doğrula ve kaynağını göster.
```

Claude'un kendi işini değerlendirmesi de yanılabilir. Bu sorular kontrolü kolaylaştırır ama senin kontrolünün yerini almaz.

---

[← Önceki: İlk proje](03-ilk-proje.md) · [İçindekiler](../README.md) · [Sonraki: Git ve GitHub →](05-git-ve-github.md)

**Made By FALCREB**
