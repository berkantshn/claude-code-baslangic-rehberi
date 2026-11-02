# 5. Git ve GitHub'ın sade anlatımı

**Git**, bilgisayarında çalışan ve projenin geçmişini tutan programdır. **GitHub** ise bu projeleri internette saklayan ve paylaşan hizmettir. Git bir proje defteriyse, GitHub o defterin güvenli yedeği ve ortak çalışma masasıdır.

## Terimler bir arada

Bir elektrik projesinin revizyonlarını düşün:

| Terim | Anlamı | Benzetme |
|---|---|---|
| **Repo (repository)** | Projenin dosyaları ve tüm geçmişi | Projenin klasörü ve arşivi |
| **Commit** | O anki halin açıklamasıyla kaydı | "Rev. 3: Mutfak hattı eklendi" |
| **Branch (dal)** | Ana hattan ayrı çalışma kolu | Asıl çizime dokunmadan kopyasında çalışmak |
| **main** | Çoğu projede ana branch'in adı | Onaylı çizim |
| **Remote** | Reponun uzaktaki kopyası (GitHub) | Ofisteki arşiv |
| **Push** | Commit'leri GitHub'a göndermek | Arşive teslim etmek |
| **Pull** | GitHub'daki yenilikleri almak | Arşivden son hali almak |
| **Clone** | Reponun kopyasını indirmek | Arşivden kopya çıkarmak |
| **PR (pull request)** | "Bu değişiklikleri ana hatta alalım" talebi | Revizyon onay talebi |
| **Merge** | Branch'teki değişiklikleri başka bir branch'e işlemek | Revizyonu onaylı çizime işlemek |

## Git'i Claude'a yaptırabilirsin

Resmî [Quickstart](https://code.claude.com/docs/en/quickstart), Git işlerinin sohbetle yapılabildiğini gösterir. Örnekler:

```text
Hangi dosyaları değiştirdim?
```

```text
Değişikliklerimi açıklayıcı bir mesajla commit et.
```

```text
feature/iletisim adında yeni bir branch aç.
```

```text
Son 5 commit'i bana sade dille özetle.
```

Yine de aşağıdaki komutları tanı. Claude'un onay ekranında ne istediğini anlamanı sağlar.

## İlk kurulum (bir kez)

Commit'lerin üzerinde adın ve e-postan yazar. Public repolarda bunu herkes görebilir, bu yüzden GitHub'ın gizli **noreply** adresini kullanmak iyi bir tercihtir. Adresini [GitHub e-posta ayarlarında](https://github.com/settings/emails) bulabilirsin. Ayrıntı: [Commit e-postası ayarlama](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address).

```bash
git config --global user.name "Adın Soyadın"
git config --global user.email "ID+kullaniciadi@users.noreply.github.com"
```

İkinci satırı GitHub'ın sana gösterdiği kendi adresinle değiştir.

Claude'un veya senin GitHub'a komutla erişebilmesi için **GitHub CLI**'ı ([cli.github.com](https://cli.github.com/)) kurup bir kez giriş yap:

```bash
gh auth login
```

## Projeyi ilk kez kaydetmek

Önce [.gitignore dosyanı](06-guvenlik.md#gitignore-gite-girmeyecekler-listesi) hazırla. Sonra:

```bash
git init -b main
git status
git add .
git status
git commit -m "feat: ilk sayfa eklendi"
```

- `git init -b main`: Bu klasörde `main` branch'iyle Git'i başlatır.
- `git status`: Durumu gösterir. Listede `.env` veya tanımadığın bir dosya varsa **devam etme**.
- `git add .`: Tüm değişiklikleri commit'e hazırlar.
- `git commit -m "..."`: Kaydı oluşturur.

## GitHub'a yüklemek

```bash
gh repo create ornek-site --private --source=. --push
```

Bu komut hesabında **private** (gizli) bir repo oluşturur ve commit'lerini yükler. Yeni bir projeye private başlamak daha güvenlidir. Public yapmadan önce [6. bölümdeki](06-guvenlik.md#public-yapmadan-önce-kontrol-listesi) listeye bak.

## Günlük akış: Branch, PR, merge

Her iş için ayrı branch açmak, çalışan sürümü korur. Bir hata olsa bile `main` etkilenmez.

```bash
git switch -c feature/iletisim      # yeni branch aç
# ... değişiklikleri yap veya Claude'a yaptır ...
git status                          # neler değişti
git diff                            # satır satır farklar
git add index.html                  # dosyayı hazırla
git commit -m "feat: iletisim bolumu eklendi"
git push -u origin HEAD             # branch'i GitHub'a gönder
gh pr create --fill                 # PR aç
gh pr view --web                    # PR'ı tarayıcıda incele
gh pr merge --merge --delete-branch # merge et ve branch'i sil
git switch main                     # main'e dön
git pull --ff-only                  # son hali al
```

`--ff-only`, yalnızca sorunsuz ileri sarılabiliyorsa günceller. Sarılamıyorsa hata verip durur, yani otomatik birleştirme yapmaz.

Yalnız çalışsan bile PR faydalıdır: merge etmeden önce değişikliklerin toplu halini görürsün ve gerektiğinde tek hamlede geri alabilirsin.

## main branch'ini korumak

GitHub'da **ruleset** veya **protected branch** (branch koruma kuralları) ile `main`'e doğrudan push'u ve **force push**'u (GitHub'daki geçmişin üzerine zorla yazmayı) engelleyebilirsin. Böylece Claude da sen de kazara ana hattın üzerine yazamazsınız.

GitHub'ın [ruleset sayfasına](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets) göre bu özellik GitHub Free'de public repolarda, Pro ve üzeri planlarda private repolarda da kullanılabilir.

## Commit mesajı ne yazmalı?

Ne yapıldığını anlatan kısa bir cümle yeterli. Birçok proje `feat:` (yeni özellik), `fix:` (hata düzeltme), `docs:` (doküman) gibi önekler kullanır. Bu düzene **Conventional Commits** denir, ama zorunlu değildir. Claude değişikliğe bakıp mesajı kendisi de önerebilir.

## Git'e giren geçmişte kalır

Git'e giren şey geçmişte kalır. Sonraki commit'te bir dosyayı silmek onu geçmişten silmez. Bu yüzden şifreleri hiçbir zaman commit etme ([6. bölüm](06-guvenlik.md)).

Daha fazlası için: [GitHub Docs: Git ile başlangıç](https://docs.github.com/en/get-started/using-git/about-git).

---

[← Önceki: İyi istek yazmak](04-iyi-istek-yazmak.md) · [İçindekiler](../README.md) · [Sonraki: Güvenlik →](06-guvenlik.md)

**Made By FALCREB**
