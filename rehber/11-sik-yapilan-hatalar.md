# 11. Sık yapılan hatalar

Hepsi kısa bir alışkanlıkla önlenebilir.

## Çalışma biçimi

**1. Tek istekte koca proje istemek.** Sonuç kontrol edilemeyecek kadar büyür.
Çözüm: Küçük adımlarla ilerle, her adımı kontrol et. ([4. bölüm](04-iyi-istek-yazmak.md))

**2. "Bitti" sözüne güvenmek.** Claude eksik bir işi bitmiş sanabilir.
Çözüm: Sonucu kendin aç ve dene. Test çıktısını gör.

**3. Anlamadığını onaylamak.** Hızlanırsın ama direksiyonu bırakırsın.
Çözüm: Anlamadığın adımda dur ve sade açıklama iste.

**4. Aynı konuşmada sonsuza dek düzeltmek.** İki denemeden sonra verim düşer.
Çözüm: `/clear` ile temiz başla, daha iyi bir istek yaz.

**5. Bir konuşmada her işi yapmak.** İlgisiz bilgiler dikkat dağıtır.
Çözüm: İş değişince `/clear` kullan.

## Git

**6. Commit etmemek.** Geri dönecek sağlam bir nokta kalmaz.
Çözüm: Çalışan her adımdan sonra commit et.

**7. `git status` okumadan `git add .` yapmak.** İstenmeyen dosyalar girebilir.
Çözüm: Önce listeyi oku.

**8. Her şeyi `main` üzerinde yapmak.** Çalışan sürümü bozma riski artar.
Çözüm: Her iş için branch ve PR kullan. ([5. bölüm](05-git-ve-github.md))

**9. Push reddedilince force push yapmak.** Başka commit'leri silebilir.
Çözüm: Önce `git fetch` ile ne olduğunu anla.

## Güvenlik

**10. Secret'ı koda yazmak veya sohbete yapıştırmak.**
Çözüm: `.env` kullan. Yapıştırdıysan anahtarı yenile. ([6. bölüm](06-guvenlik.md))

**11. Silerek secret sorununu çözdüğünü sanmak.** Git geçmişinde kalır.
Çözüm: Önce anahtarı iptal et.

**12. Kontrolsüz public yapmak.** Bütün geçmiş açılır.
Çözüm: [Public yapmadan önce listesini](06-guvenlik.md#public-yapmadan-önce-kontrol-listesi) uygula.

**13. "Çok soruyor" diye onayları kapatmak.** Normal bilgisayarda `--dangerously-skip-permissions` kullanmak riskli.
Çözüm: Sık kullanılan güvenli komutlar için dar izin kuralları yaz. ([7. bölüm](07-onaylar-ve-riskli-komutlar.md))

**14. Auto modda olduğunu fark etmemek.** Her şeyin sorulacağını sanabilirsin.
Çözüm: Durum çubuğuna bak. Yeni başlıyorsan Manual modda çalış.

**15. Gerçek müşteri verisiyle denemek.** Telefon, adres veya kimlik bilgisi yanlış yere gidebilir.
Çözüm: Denemelerde sahte veri kullan: `ornek@example.com`, `0000 000 00 00`.

## Bağımlılık

**16. Önerilen her paketi kurmak.** Gereksiz paket, yeni risk ve bakım demektir. Yapay zekâ bazen var olmayan veya yanlış adlı bir paket önerebilir.
Çözüm: "Bu paket gerekli mi, onsuz yapılır mı?" diye sor. Adını ve yayıncısını kontrol et.

**17. Lock dosyasını yok saymak.** **Lock dosyası** (`pnpm-lock.yaml`, `package-lock.json` gibi) kurulan sürümleri kayıt altına alır, böylece proje her yerde aynı sürümlerle kurulur.
Çözüm: Commit et.

## Yayın

**18. Yapay zekânın yazdığı metni okumadan yayınlamak.** Uydurma tecrübe yılı, yanlış fiyat veya yorum olabilir.
Çözüm: Her cümleyi oku. Doğrulayamadığın iddiayı çıkar.

**19. Kullanıcı verisi toplayan özelliği hafife almak.** Form, üyelik veya ödeme, basit siteyi ciddi bir sisteme çevirir.
Çözüm: Bu özellikleri eklemeden önce uzmana danış.

**20. Bu rehbere körü körüne güvenmek.** Rehber de yanılabilir, ürün de değişir.
Çözüm: Kritik bilgileri [resmî dokümandan](https://code.claude.com/docs/en/overview) kontrol et.

---

[← Önceki: Bir şey bozulunca](10-bir-sey-bozulunca.md) · [İçindekiler](../README.md) · [Sonraki: Terimler sözlüğü →](12-terimler-sozlugu.md)

**Made By FALCREB**
