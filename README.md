# 🤖AI DESTEKLİ TELEGRAM ASİSTANI 
(n8n + OpenAI + Gmail + Takvim)

Bu proje, no-code otomasyon aracı **n8n** kullanılarak geliştirilmiş bir **Telegram bot sistemidir**. Kullanıcıdan gelen **yazılı** veya **sesli** mesajları işleyerek **OpenAI ile analiz** eder, cevap verir. Ek olarak **Gmail ile e-posta gönderebilir/alabilir**, ve **Google Calendar** entegrasyonuyla takvime etkinlik ekleyebilir.

---

## ✨ PROJE YETKİNLİKLERİ

* 📢 Telegram botu ile mesaj alma (yazı ve ses)
* 🧠 OpenAI GPT-4o ile akıllı mesaj analiz ve yanıtlama
* 🎤 Sesli mesajları yazıya çevirme (OpenAI Whisper API)
* 📧 Gmail ile e-posta gönderme / alma
* 🗓️ Google Calendar ile etkinlik yaratma ve listeleme
* ⏰ Gerçek zamanlı İstanbul saat diliminde çalışma
* 🧳 Hafıza modülü ile sohbet geçmişi takibi

---

## ⚙️ NASIL ÇALIŞI? 

### 1. ⚡️ Telegram Trigger

Telegram botuna bir mesaj geldiğinde workflow başlar. Mesaj JSON formatında alınır.

### 2. 🌐 Switch Node

Mesaj türüne bakar:

* `text` varsa: yazılı mesaj akışı gerçekleşir.
* `voice.file_id` varsa: sesli mesaj akışı gerçekleşir.

### 3A. 🖊️ Yazılı Mesaj Akışı

* `Set` node ile mesaj "metin" değişkenine atanır
* `AI Agent` node GPT-4o ile mesajı analiz eder
* `Send Message` node, cevabı tekrar Telegram'a yollar

### 3B. 🎤 Sesli Mesaj Akışı

* `Telegram: Get a file` node ile ses dosyası indirilir
* `Transcribe Recording` node OpenAI Whisper ile sesi yazıya çevirir
* `AI Agent` node analiz eder ve cevap üretir
* `Send Message` node cevabı Telegram'a yollar

### 4. 📧 Gmail Bağlantıları

* `Send a message in Gmail`: OpenAI'den alınan bilgilerle mail atabilir
* `Get many messages`: Gelen kutusundaki mailleri listeleyebilir

### 5. 🗓️ Google Calendar Entegrasyonu

* `Create Event`: AI tarafından belirlenen tarih/saat ile etkinlik yaratılır
* `Get Events`: Belirli tarih aralığındaki etkinlikleri listeler

### 6. 🧣 Simple Memory

* Sohbetlerin 10 mesaj gerisine kadar geçmişi tutarak AI agent'lara daha bağlamı anlamaları için kullanılır

---

## 📅 Zaman Dilimi Ayarı

Bu workflow **Europe/Istanbul** saat diliminde çalışacak şekilde ayarlanmıştır.

AI Agent içindeki `systemMessage` şu şekilde zaman bilgisi verir:

```txt
Şu anki saat: {{ $now.setZone("Europe/Istanbul").toFormat("yyyy-MM-dd HH:mm:ss") }}
```

---

## 📚 Kullanılan Araçlar & Teknolojiler

| Teknoloji           | Amaç                               |
| ------------------- | ---------------------------------- |
| n8n                 | Otomasyon workflow tasarımı        |
| Telegram API        | Bot tetikleme, mesaj alma/gönderme |
| OpenAI GPT-4o       | Akıllı mesaj yanıtlama             |
| OpenAI Whisper      | Sesli mesajı yazıya dökme          |
| Gmail API           | E-posta işlemleri                  |
| Google Calendar API | Takvim etkinlikleri                |

---

## 📖 Projeyi Kullananlar için Notlar

* Telegram botun `/start` komutu ile aktif olabilir
* Credential hataları çok yaygın, dikkatle OAuth kurulumları yapılmalı
* AI yanıtlarının çoğu `systemMessage` ayarına bağlı olarak değişir
* Saat bilgisi varsayılan olarak UTC'dir; `Europe/Istanbul` olarak ayarlandı

---
