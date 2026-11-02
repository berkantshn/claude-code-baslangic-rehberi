# 10. Bir şey bozulunca

Bozulması normaldir. Arıza ararken önce şalteri indirirsin, sonra ölçersin, en son tamir edersin. Burada da aynı sıra geçerlidir: **durdur, anla, sonra geri al.**

## 1. Durdur

Claude yanlış yöne gidiyorsa `Esc` tuşuna bas. O ana kadar yapılanlar korunur, sen de yön verirsin.

## 2. Anla

Paniklemeden önce neyin değiştiğini gör:

```bash
git status
git diff
git log --oneline -5
```

Oturum içinde `/diff` de değişiklikleri gösterir. Claude'a şunu sorabilirsin:

```text
Son yaptığın değişiklikleri ve ne bozulmuş olabileceğini anlat. Henüz hiçbir şeyi değiştirme.
```

Hata mesajı varsa **tam metnini** yapıştır. İçinde secret olup olmadığına bak.

## 3. Duruma göre geri al

### Claude az önce yaptı

`/rewind` yaz veya istek satırı boşken iki kez `Esc` bas. Menüden önceki bir isteği seçersin:

- **Restore code and conversation:** Kod ve konuşma geri döner.
- **Restore conversation:** Yalnızca konuşma geri döner.
- **Restore code:** Yalnızca kod geri döner.

**Sınırları var:** `/rewind` esas olarak Claude'un dosya düzenleme araçlarıyla yaptığı değişiklikleri izler. Yalnızca bir komutun değiştirdiği dosyalar, senin elle yaptığın değişiklikler ve bazı **subagent** (Claude'un iş devrettiği yardımcı ajan) düzenlemeleri geri gelmeyebilir. Resmî doküman da bunun Git'in yerini tutmadığını belirtir. Ayrıntı: [Checkpointing](https://code.claude.com/docs/en/checkpointing).

### Henüz commit etmedin

Tek dosyayı son commit'teki haline döndürmek için:

```bash
git restore index.html
```

**Dikkat:** O dosyadaki kaydedilmemiş değişiklikler kaybolur. Emin değilsen önce kopyasını al.

### Commit ettin

**Revert**, bir commit'i tersine çeviren yeni bir commit oluşturur. Geçmiş silinmez, güvenlidir:

```bash
git log --oneline -5
git revert abc1234
```

`abc1234` yerine geri almak istediğin commit'in kimliğini yaz. Bu bir merge commit'iyse komut `git revert -m 1 abc1234` olur.

### PR'ı merge ettin

GitHub'daki PR sayfasında **Revert** düğmesi vardır. Bu, değişikliği geri alan yeni bir PR açar. Ayrıntı: [PR geri alma](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/reverting-a-pull-request).

### Kayıp commit arıyorsun

```bash
git reflog
```

Git'in yakın zamanda geçtiği noktaları gösterir. Kayıp görünen commit'ler çoğu zaman buradadır. Bir şey denemeden önce mevcut hali güvenceye almak için bir branch aç:

```bash
git switch -c kurtarma/deneme
```

## Sık görülen durumlar

| Durum | Anlamı | Ne yapmalı |
|---|---|---|
| Push reddedildi, `Updates were rejected` | GitHub'da sende olmayan commit var | `git fetch` yap, durumu Claude'a anlattır. **Force push yapma** |
| `CONFLICT`, `Automatic merge failed` | **Merge çakışması**: aynı yeri iki farklı değişiklik düzeltmiş | Claude'a "çakışmayı çözmeme yardım et, seçenekleri anlat" de. Vazgeçmek için `git merge --abort` |
| `GH013: Repository rule violations` | Korunan branch'e doğrudan push denedin | Koruma çalışıyor. Branch ve PR ile ilerle |
| `Not possible to fast-forward` | Yerel kopyan ile GitHub'daki farklılaşmış | Dur ve durumu incele, otomatik birleştirme yaptırma |
| `LF will be replaced by CRLF` uyarısı | Windows ve diğer sistemlerin satır sonu farkı. Genelde bir hata değildir | Aşağıya bak |
| `claude` çalışmıyor | Kurulum veya PATH sorunu | `claude doctor`, sonra [kurulum sorun giderme](https://code.claude.com/docs/en/troubleshoot-install) |
| Ayarların veya CLAUDE.md okunmuyor | Yapılandırma sorunu | `/doctor`, `/context`, [yapılandırma hatalarını ayıklama](https://code.claude.com/docs/en/debug-your-config) |
| Kullanım sınırına geldin | Planının sınırı doldu | `/usage` ile kontrol et, [maliyet sayfası](https://code.claude.com/docs/en/costs) |
| Bilinmeyen Claude Code hatası | Rehberde yok | [Hata referansı](https://code.claude.com/docs/en/errors) |

Farklı işletim sistemleri arasında çalışıyorsan, satır sonu farkının dosyaları değişmiş göstermesini önlemek için proje köküne `.gitattributes` dosyası ekle:

```gitattributes
* text=auto eol=lf
```

## Claude döngüye girdiyse

Aynı hatayı düzeltmeye çalışıp başka şeyleri bozuyorsa:

1. `Esc` ile durdur.
2. `/rewind` ile veya Git ile çalışan son hale dön.
3. `/clear` ile temiz başla.
4. Şunları içeren yeni bir istek yaz: Ne çalışıyordu, ne bozuldu, neler denendi ve işe yaramadı.

## Riskli denemeden önce

Büyük bir değişiklikten önce çalışan hali commit et ve yeni branch'te dene. Bozulursa `main` zaten sağlamdır.

## Ne zaman yardım almalısın?

- Secret sızmış olabilir: [6. bölüm](06-guvenlik.md#secret-sızarsa-ne-yapmalı)
- Canlı sistem gerçek kullanıcılar için durmuşsa
- Veri kaybolduysa ve yedeğin belirsizse
- Ödeme, kişisel veri veya güvenlik söz konusuysa
- Claude'un önerdiği çözümü anlamıyor ama geri dönüşü olmayan bir adım atman gerekiyorsa

Bu durumlarda deneme yanılmayı bırakıp deneyimli birine danış. Değişiklik yapmadan önce sorunun kaydını al.

Claude Code'un kendisinde hata bulursan oturum içinde `/feedback` kullanabilirsin. Güvenlik açıkları için [resmî bildirim yolu](https://code.claude.com/docs/en/security#reporting-security-issues) farklıdır.

---

[← Önceki: Oturum devamlılığı](09-oturum-devamliligi.md) · [İçindekiler](../README.md) · [Sonraki: Sık yapılan hatalar →](11-sik-yapilan-hatalar.md)

**Made By FALCREB**
