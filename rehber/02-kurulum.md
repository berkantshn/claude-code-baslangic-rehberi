# 2. Kurulum

Komutlar değişebilir. Kurmadan önce buradaki komutu resmî sayfayla karşılaştır: [Quickstart](https://code.claude.com/docs/en/quickstart) ve [Advanced setup](https://code.claude.com/docs/en/setup).

## Gerekenler

- **İşletim sistemi:** macOS 13+, Windows 10 1809+ veya Windows Server 2019+, Ubuntu 20.04+, Debian 10+, Alpine 3.19+
- **Donanım:** En az 4 GB RAM, x64 veya ARM64 işlemci
- **İnternet bağlantısı**
- **Uygun hesap** (bkz. [1. bölüm](01-claude-code-nedir.md#ücretli-mi))

## Terminal istemiyorsan

[Masaüstü uygulamasını](https://code.claude.com/docs/en/desktop-quickstart) kurup **Code** sekmesini kullanabilirsin. Terminal gerekmez. Bu rehberdeki terminal komutları yerine ilgili arayüz düğmelerini kullanman gerekebilir.

## Terminali açmak

**Terminal**, bilgisayara yazıyla komut verdiğin penceredir.

| Sistem | Nasıl açılır |
|---|---|
| Windows | `Win + X`, sonra **Terminal** veya **Windows PowerShell** |
| macOS | `Cmd + Boşluk`, `Terminal` yaz, `Enter` |
| Linux | Çoğu dağıtımda `Ctrl + Alt + T` |

Windows'ta satır başı `PS C:\...` ise **PowerShell**'desin. Başında `PS` yoksa **CMD**'desin. Kurulum komutları ikisinde farklıdır.

## Kurulum komutu

Yalnızca kendi sistemine uyanı çalıştır.

**Windows PowerShell:**

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Windows CMD:**

```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

**macOS, Linux veya WSL:**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Birkaç not:

- Komut indirme sırasında ilerleme göstermez. Pencereyi kapatmadan bekle.
- Windows'ta yönetici olarak çalıştırman gerekmez.
- **WSL**, Windows içinde Linux çalıştırma özelliğidir. Bilmiyorsan büyük ihtimalle gerekmiyordur.
- Bu komutlar internetten bir kurulum dosyası indirip çalıştırır. Bu yüzden böyle bir komutu yalnızca güvendiğin resmî kaynaktan kopyala.

Paket yöneticisi seviyorsan **Homebrew** (`brew install --cask claude-code`) veya **WinGet** (`winget install Anthropic.ClaudeCode`) da kullanılabilir. Paket yöneticisi, programları komutla kurup güncelleyen araçtır. Bu ikisi kendiliğinden güncellenmez, zaman zaman `brew upgrade claude-code` veya `winget upgrade Anthropic.ClaudeCode` çalıştırman gerekir. Normal kurulum ise arka planda kendini günceller.

## Kurulumu doğrula

**Yeni bir terminal penceresi aç** ve şunu yaz:

```bash
claude --version
```

Bir sürüm numarası görmelisin. Daha ayrıntılı kontrol için:

```bash
claude doctor
```

## Sık görülen kurulum hataları

| Gördüğün | Anlamı | Ne yapmalı |
|---|---|---|
| `claude` bulunamadı, tanınmıyor | Kurulum klasörü **PATH**'e eklenmemiş (PATH: bilgisayarın komutları aradığı klasör listesi) | [Resmî PATH çözümü](https://code.claude.com/docs/en/troubleshoot-install#command-not-found-claude-after-installation) |
| `The token '&&' is not a valid statement separator` | CMD komutunu PowerShell'de çalıştırdın | PowerShell komutunu kullan |
| `'irm' is not recognized` | PowerShell komutunu CMD'de çalıştırdın | CMD komutunu kullan veya PowerShell'e geç |
| `syntax error near unexpected token '<'`, `403` | İndirme başarısız oldu | [Kurulum sorun giderme](https://code.claude.com/docs/en/troubleshoot-install#find-your-error) |

## Git'i de kur

**Git**, projenin değişiklik geçmişini tutan programdır ([5. bölümde](05-git-ve-github.md) anlatılıyor). Claude Code Git olmadan da açılır, ama bu rehberdeki güvenli çalışma düzeni için Git gerekir.

- **Windows:** [Git for Windows](https://git-scm.com/downloads/win). Kurulum ekranlarında varsayılanlarla ilerleyebilirsin. Kurulu olduğunda Claude Code komutları Git Bash ile de çalıştırabilir. Kurulu değilse PowerShell kullanır.
- **macOS ve Linux:** [git-scm.com/downloads](https://git-scm.com/downloads)

Kontrol etmek için:

```bash
git --version
```

## İlk giriş

Bir proje klasörüne geçip `claude` yaz. İlk açılışta tarayıcı açılır ve hesabınla giriş yaparsın.

- Tarayıcı açılmazsa terminalde `c` tuşuna basıp giriş adresini kopyalayabilirsin.
- Tarayıcı kod gösterirse terminale yapıştır.
- Hesap değiştirmek için oturum içinde `/login` veya `/logout` yaz.

Claude Code, daha önce güvenmediğin bir klasörde açıldığında sana bu klasöre güvenip güvenmediğini sorar. **Yalnızca tanıdığın klasörlerde kabul et.** Ana kullanıcı klasöründe değil, her proje için ayrı bir klasörde başlat.

## Oturum içinde ilk bilmen gerekenler

| Komut veya tuş | Ne yapar |
|---|---|
| `/help` | Kullanılabilir komutları gösterir |
| `/` | Komut listesini açar |
| `Esc` | Çalışan Claude'u durdurur |
| `Shift + Tab` | İzin modunu değiştirir ([7. bölüm](07-onaylar-ve-riskli-komutlar.md)) |
| `/exit` veya boş satırda iki kez `Ctrl + D` | Çıkar |

Tam liste: [Komutlar](https://code.claude.com/docs/en/commands).

Kaldırma ve sürüm yönetimi için: [Advanced setup](https://code.claude.com/docs/en/setup).

---

[← Önceki: Claude Code nedir?](01-claude-code-nedir.md) · [İçindekiler](../README.md) · [Sonraki: İlk proje →](03-ilk-proje.md)

**Made By FALCREB**
