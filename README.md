# n8n Chatbot Projesi

İşletmelere özel uyarlanabilir, **n8n** workflow tabanlı AI chatbot platformu. Webhook entegrasyonları ve LLM bağlantıları ile özelleştirilebilir konuşma akışları oluşturmaya yarar.

## 📌 Proje Hakkında

Bu proje, küçük ve orta ölçekli işletmelerin müşteri etkileşimini otomatikleştirmek için tasarlandı. **n8n**'in görsel workflow editörü kullanılarak, kod yazmadan veya çok az kodla özelleştirilebilir bir AI destekli chatbot kurmayı amaçlıyor.

Repodaki `n8n_ai_chatbot.json` dosyası, doğrudan n8n'e içe aktarılarak çalıştırılabilen, tam fonksiyonel bir workflow şablonudur. Web sitesi sohbet butonu, WhatsApp Business veya Telegram gibi kanallardan gelen mesajları AI ile cevaplayan bir botun arka planını oluşturur.

## ✨ Özellikler

- 🔌 **Webhook tabanlı giriş** — Web sitesi, WhatsApp, Telegram, Instagram DM gibi kaynaklardan mesaj alır
- 🤖 **AI bağlantısı** — OpenAI, Onysoft AI Gateway, Anthropic Claude veya yerel LLM modellerine yönlendirilebilir
- 💾 **Konuşma geçmişi** — Session bazlı bağlam korunur, kullanıcı önceki mesajlarını "unutmaz"
- 🎯 **İşletmeye özel uyarlama** — System prompt ve workflow node'ları ile her sektöre uygun hale getirilebilir (e-ticaret, randevu, müşteri desteği)
- 📊 **Görsel akış** — n8n'in sürükle-bırak editörü ile teknik olmayan ekipler de bakım yapabilir
- 🔁 **Hata yönetimi** — AI hataları, rate limit ve timeout durumlarında otomatik yedekleme

## 🛠️ Kullanılan Teknolojiler

| Katman | Teknoloji |
|---|---|
| Workflow motoru | **n8n** (self-hosted veya n8n Cloud) |
| Programlama | **JavaScript** (Function ve Code node'larında) |
| Entegrasyon | **REST API / Webhook** (giriş ve çıkış) |
| AI sağlayıcı | OpenAI uyumlu API (GPT, Claude, Gemini, Llama vb.) |

## 🚀 Kurulum

### Gereksinimler

- Çalışan bir n8n instance'ı (self-hosted Docker, n8n Cloud veya VPS üzerinde)
- Bir LLM sağlayıcısı API anahtarı:
  - [Onysoft AI Gateway](https://api.onysoft.com) (TL faturalı, 400+ model)
  - veya OpenAI / Anthropic / Google AI

### Adım Adım

**1. Repoyu klonlayın**

```bash
git clone https://github.com/alierenonyil/n8n-chatbot-projesi.git
cd n8n-chatbot-projesi
```

**2. Workflow'u n8n'e içe aktarın**

- n8n arayüzünde sağ üstteki menüden **Workflows → Import from File** seçin
- Repodaki `n8n_ai_chatbot.json` dosyasını yükleyin
- Workflow editörüne dosya otomatik açılır

**3. Credential'ları ayarlayın**

- Workflow'daki **AI node'una** (örn. "OpenAI" veya "HTTP Request") tıklayın
- **Credentials** kısmından API anahtarınızı tanımlayın
- Onysoft AI Gateway kullanıyorsanız `base_url` olarak `https://api.onysoft.com/v1` yazın

**4. Webhook URL'ini kopyalayın**

- Workflow'un başındaki **Webhook** node'una tıklayın
- "Production URL"i kopyalayın — bu, chatbot frontendinizin bağlanacağı URL

**5. Workflow'u aktifleştirin**

- Sağ üstteki **Active** toggle'ını açın
- Workflow artık webhook'a gelen istekleri otomatik cevaplıyor

### Hızlı Test

```bash
curl -X POST https://your-n8n-instance.com/webhook/chatbot \
  -H "Content-Type: application/json" \
  -d '{
    "message": "Merhaba, ürünleriniz hakkında bilgi alabilir miyim?",
    "sessionId": "test-user-001"
  }'
```

Başarılı yanıt:

```json
{
  "reply": "Merhaba! Tabii ki, hangi konuda bilgi almak istersiniz?",
  "sessionId": "test-user-001"
}
```

## 📁 Proje Yapısı

```
n8n-chatbot-projesi/
├── n8n_ai_chatbot.json    # Tam fonksiyonel n8n workflow şablonu
└── README.md               # Bu dosya
```

## 🔧 Özelleştirme İpuçları

Workflow'u kendi işletmen için uyarlamak için:

- **System prompt** — AI node ayarlarında "system" mesajını işletmenin tonuna göre düzenle ("Sen WawaHouse bebek mağazasının asistanısın..." gibi)
- **Yeni node ekle** — Veritabanı sorgusu (sipariş takibi), e-posta bildirimi, CRM entegrasyonu (HubSpot, Salesforce)
- **Çoklu kanal** — Aynı workflow'a farklı webhook'lar ekleyerek WhatsApp ve site sohbetini birleştir
- **Maliyet kontrolü** — `temperature` ve `max_tokens` değerlerini iş ihtiyacına göre kıs

## 📸 Ekran Görüntüsü

> Workflow görseli ileride eklenecek. Şu anda repodaki JSON dosyasını n8n'e içe aktararak görsel akışı n8n editöründe inceleyebilirsiniz.

## 👥 Katkıda Bulunanlar (Contributors)

- **Ali Eren Onyıl** — [@alierenonyil](https://github.com/alierenonyil) — Workflow tasarımı, JavaScript Function node'ları, AI entegrasyonu

## 🌐 Geliştirici

**Ali Eren Onyıl**
Onysoft Veri Merkezi A.Ş. — Kurucu & Full-Stack Developer

- 🌍 Portfolyo: [ali.onysoft.com](https://ali.onysoft.com)
- 💼 LinkedIn: [linkedin.com/in/alierenonyil](https://linkedin.com/in/alierenonyil)
- 🐙 GitHub: [github.com/alierenonyil](https://github.com/alierenonyil)
- 📧 E-posta: alieren@onysoft.com

## 📄 Lisans

Bu proje kişisel portfolyo ve eğitim amaçlı paylaşılmıştır. Ticari kullanım için iletişime geçiniz.
