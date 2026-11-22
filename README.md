# ByteAI

**ByteAI'ye her cihazdan bağlanma sayfası** · https://egegurkan.github.io/ByteAI/

ByteAI kendi bilgisayarında çalışan özel bir yapay zekâ çalışma alanıdır (Ollama + Open WebUI).
Bu depo yalnızca küçük bir **yönlendirme sayfası** içerir: Tailscale adresini bir kez yazarsın,
sayfa seni doğrudan kendi bilgisayarındaki Open WebUI'ye götürür.

*English summary: a tiny GitHub Pages launcher. Enter your Tailscale machine address once and it
redirects you to the Open WebUI running on your own ByteAI computer. The address stays in your
browser only.*

---

## Nasıl kullanılır

1. Telefonda veya diğer bilgisayarda **Tailscale** uygulamasını aç, ByteAI bilgisayarıyla aynı hesapla giriş yap.
2. https://egegurkan.github.io/ByteAI/ adresine gir.
3. ByteAI bilgisayarının tam Tailscale adresini (`.ts.net` ile biten) yaz ve **Bağlan**'a bas.
   **Port** kutusunu boş bırakabilirsin; boşsa ByteAI'nin varsayılan `8443` portu kullanılır.
4. **Hatırla** seçiliyse sonraki girişlerde sayfa 3 saniye içinde otomatik bağlanır.
   **İptal**, **Değiştir** ve **Unut** düğmeleriyle bu davranışı her zaman kontrol edebilirsin.

Kabul edilen biçimler:

| Yazdığın | Açılan adres |
|---|---|
| `bilgisayar.tailxxxx.ts.net` | `https://bilgisayar.tailxxxx.ts.net:8443/` |
| `bilgisayar.tailxxxx.ts.net:9443` | `https://bilgisayar.tailxxxx.ts.net:9443/` |
| `https://bilgisayar.tailxxxx.ts.net:8443/` | aynen |

Yer imi olarak kaydetmek için adresi sayfa adresinin sonuna `#` ile ekleyebilirsin (alanlar dolu açılır):
`https://egegurkan.github.io/ByteAI/#bilgisayar.tailxxxx.ts.net`
— `#` sonrası tarayıcıdan dışarı gönderilmez.

> Kısa makine adı (`bilgisayar`) veya `100.x.y.z` IP adresi çalışmaz: Tailscale'in HTTPS sertifikası
> yalnızca tam `.ts.net` adı için geçerlidir.

## ByteAI bilgisayarında bir kez yapılacaklar

ByteAI kurulum klasöründe (`UI\Setup`):

```powershell
Script-START.cmd
```

```powershell
.\15-Tailscale-Serve.ps1 -Enable
```

`15-Tailscale-Serve.ps1` sonunda yazan **"Diger cihazlarda: https://…ts.net:8443"** satırı,
bu sayfaya yazacağın adrestir.

| Ne | Nerede |
|---|---|
| Open WebUI (bu bilgisayar) | `http://localhost:3000` |
| Open WebUI (Tailscale) | `https://<bilgisayar>.ts.net:8443` |
| Paylaşımı kapatmak | `.\15-Tailscale-Serve.ps1 -Disable` |

Paylaşım yalnızca **senin tailnet'indeki** cihazlara açıktır. `tailscale funnel` kullanma ve modemde
port yönlendirmesi açma; bu sayfa internete hiçbir port açmaz.

## Gizlilik

- Sayfa tek bir statik `index.html` dosyasıdır; sunucu tarafı, analiz, çerez veya dış kaynak yoktur.
- Tailscale adresi yalnızca tarayıcının `localStorage` alanında tutulur, GitHub'a veya başka bir yere gönderilmez.
- Sohbetler, modeller ve dosyalar kendi bilgisayarında kalır; bu sayfa sadece oraya yönlendirir.
- Tailscale adresini bu depoya **yazma**: depo herkese açıktır.

## GitHub Pages'te yayınlama

1. GitHub'da `ByteAI` adlı yeni bir depo oluştur.
2. Bu klasördeki `index.html`, `README.md` ve `LICENSE` dosyalarını deponun köküne yükle.
3. **Settings → Pages → Build and deployment**: *Deploy from a branch*, branch `main`, klasör `/ (root)`.
4. Birkaç dakika sonra sayfa https://egegurkan.github.io/ByteAI/ adresinde açılır.

> Bu klasör ByteAI kurulumunun içinde durur, ama **ByteAI klasörünün tamamını** depoya yükleme:
> içinde `Secrets` (API anahtarları), modeller ve sohbet verileri vardır.

## Lisans

[MIT](LICENSE) © 2026 the ByteAI contributors
