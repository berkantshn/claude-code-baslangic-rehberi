# 7. Onay istemeleri ve riskli komutlar

Claude Code bir işlem yapmadan önce izin isteyebilir. Ne zaman soracağını **izin modu (permission mode)** belirler. Bu bölümün en önemli bilgisi şudur: **yeni sürümlerde Claude her şeyi sana sormayabilir.**

## İzin modları

| Mod | Durum çubuğunda | Sormadan yapabildikleri | Ne zaman |
|---|---|---|---|
| **Manual** (`default`) | `manual mode on` | Sadece okuma | Öğrenirken, hassas işlerde |
| **Accept edits** (`acceptEdits`) | `accept edits on` | Okuma, dosya düzenleme, `mkdir`, `touch`, `rm`, `rmdir`, `mv`, `cp`, `sed` gibi komutlar (çalışma klasöründe) | Değişiklikleri sonradan toplu inceleyeceksen |
| **Plan** (`plan`) | `plan mode on` | Okuma ve keşif. Plan onaylanana kadar kaynak dosya düzenlemez | Değişiklikten önce |
| **Auto** (`auto`) | `auto mode on` | Her şey, arka planda güvenlik kontrolüyle | Yönüne güvendiğin uzun işler |
| **Bypass** (`bypassPermissions`) | `bypass permissions on` | Neredeyse her şey, kontrolsüz | Yalnızca yalıtılmış ortamlar |

Bir de **betikler** (otomatik çalışan küçük programlar) için `dontAsk` modu vardır. Yeni başlayan biri için gerekli değildir. Ayrıntılar: [İzin modları](https://code.claude.com/docs/en/permission-modes).

## Varsayılan mod: Auto

Resmî dokümana göre v2.1.283 ve sonrasında terminal ve VS Code oturumları **auto modda başlar**. Bu modda ayrı bir yapay zekâ modeli (sınıflandırıcı) işlemleri denetler ve güvensiz bulduklarını engeller. Normal onay ekranlarının çoğunu görmezsin.

Anthropic'in kendi uyarısı nettir: auto mod onay ekranlarını azaltır ama **güvenliği garanti etmez** ve hassas işlerde incelemenin yerini tutmaz.

**Önerimiz:** Komutları tanıyana kadar Manual modda çalış.

```bash
claude --permission-mode manual
```

Oturum içinde `Shift + Tab` ile mod değiştirebilirsin. Auto'dan başlayınca sıra şöyledir: Manual → Accept edits → Plan → tekrar Auto. Etkin modu durum çubuğundan kontrol et.

Bu bilgisayardaki terminal oturumlarının hep Manual başlaması için `~/.claude/settings.json` dosyasına şunu ekleyebilirsin:

```json
{
  "permissions": {
    "defaultMode": "default"
  }
}
```

`~`, kullanıcı klasörün demektir. Bu dosyada başka ayarların varsa üzerine yazma. Claude'dan mevcut ayarları koruyarak eklemesini iste.

## Onay ekranını okumak

Sor kendine:

1. **Ne yapacak?** Komutu ve açıklamasını oku.
2. **Nereye dokunuyor?** Proje klasörünün dışı mı?
3. **Geri alınabilir mi?** Silme, gönderme, yayınlama gibi işler dikkat ister.
4. **Ben bunu istedim mi?** İstemediğin bir işse reddet.

Anlamadığında reddet ve açıklama iste. Reddetmek bir şeyi bozmaz.

**"Yes, and don't ask again" dikkat ister.** Dokümana göre bu seçenek bir terminal komutu için o repoda kalıcı olabilir. Bu izinleri `/permissions` ile görüp kaldırabilirsin. "Çok soruyor" diye geniş izin vermek, kontrolü bırakmak demektir.

## Riskli komutlar tablosu

Bunları görünce dur ve neden gerektiğini sor:

| Komut | Ne yapar | Risk |
|---|---|---|
| `rm -rf ...` | Dosya/klasörü sormadan siler | Çöp kutusuna gitmez |
| `Remove-Item -Recurse -Force ...` | PowerShell'de aynı iş | Aynı |
| `git reset --hard` | Commit edilmemiş değişiklikleri atar | Geri getirmek çoğu zaman imkânsız |
| `git clean -fd` | Git'in takip etmediği dosyaları siler | Silinen dosya geri gelmez. `-x` eklenirse `.env` gibi hariç tutulan dosyalar da silinir |
| `git checkout .` veya `git restore .` | Kaydedilmemiş değişiklikleri atar | Emeğin gidebilir |
| `git push --force` | GitHub'daki geçmişin üzerine yazar | Başka commit'ler kaybolabilir |
| `gh repo edit --visibility public ...` | Repoyu herkese açar | Tüm geçmiş görünür olur |
| `gh repo delete` | Repoyu siler | Çok ciddi veri kaybı |
| `curl ... \| bash`, `irm ... \| iex` | İnternetten kod indirip çalıştırır | Kaynağa tam güven gerekir |
| `npm install`, `pnpm add`, `pip install` | Dış paket kurar | Adı doğru mu, gerçekten gerekli mi? |
| `DROP TABLE`, `DELETE FROM` | Veritabanı kaydı siler | Yedek yoksa geri gelmez |
| `--dangerously-skip-permissions` | Tüm onayları kapatır | Sadece yalıtılmış ortamda |

Liste tam değildir. Tanımadığın her komutu sorabilirsin.

## Bypass modu

`--dangerously-skip-permissions` ve `bypassPermissions`, onay ve güvenlik kontrollerini büyük ölçüde kapatır. Resmî doküman bunları yalnızca internet erişimi olmayan **container** veya **sanal makine** gibi yalıtılmış ortamlar için önerir (ikisi de bir programı bilgisayarının geri kalanından ayrı çalıştırır). **Normal bilgisayarında kullanma.**

## Kendi kurallarını yazmak

Proje içindeki `.claude/settings.json` dosyasına izin kuralı ekleyebilirsin. `ask` sormaya, `deny` engellemeye zorlar:

```json
{
  "permissions": {
    "ask": ["Bash(git push *)", "PowerShell(git push *)"],
    "deny": ["Read(./.env)", "Read(./.env.local)"]
  }
}
```

- `deny` kuralları bütün modlarda geçerlidir.
- `ask` kuralları auto ve bypass modlarında da sormaya zorlar.
- Kurallar komutun yazılış biçimine bakar. Aynı işi farklı yazan bir komutu kaçırabilir. Yani bir katmandır, mutlak engel değildir.

Ayrıntı: [İzinleri yapılandırmak](https://code.claude.com/docs/en/permissions).

## Prompt injection

**Prompt injection**, bir web sayfasına veya dosyaya gizlenen metinle yapay zekâyı kandırma girişimidir. Örneğin indirilen belgede "şu şifreyi şuraya gönder" yazabilir. Claude Code'da bu riske karşı önlemler vardır, ama dokümanın dediği gibi hiçbir sistem tamamen güvenli değildir.

- Tanımadığın kaynaklardan gelen içeriklerle çalışırken Manual modda kal.
- İnternetten bulduğun bir projeyi veya metni incelemeden "bunu çalıştır" deme.

## Daha fazla yalıtım

`/sandbox`, komutların erişebileceği dosya ve ağ alanını sınırlar. macOS, Linux ve WSL 2'de vardır, yerel Windows'ta yoktur. Ayrıntı: [Sandboxing](https://code.claude.com/docs/en/sandboxing).

---

[← Önceki: Güvenlik](06-guvenlik.md) · [İçindekiler](../README.md) · [Sonraki: CLAUDE.md →](08-claude-md.md)

**Made By FALCREB**
