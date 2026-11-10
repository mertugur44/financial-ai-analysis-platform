# Finansal Analiz Platformu – Yapay Zekâ Destekli Bitirme Projesi

Finansal Analiz Platformu; **finansal veri görselleştirme, teknik analiz, yapay zekâ destekli doğal dil etkileşimi, portföy yönetimi, trade günlüğü ve sosyal paylaşım** özelliklerini tek bir platform altında birleştiren Yazılım Mühendisliği bitirme projesidir.

Platform, finansal analiz sürecini özellikle yeni başlayan kullanıcılar için daha **erişilebilir, öğretici ve kullanıcı odaklı** hale getirmeyi amaçlamaktadır.

🌐 **Canlı Demo:** [kriptotufan.com](https://kriptotufan.com/)

## Temel Modüller

Platform altı temel modülden oluşmaktadır:

- **Ana Sayfa** — Platform özelliklerine ve ana modüllere hızlı erişim
- **Piyasa** — Finansal varlıkların görüntülenmesi, grafik ve teknik analiz araçları
- **FinansAI** — Türkçe finans ve kripto odaklı yapay zekâ destekli soru-cevap sistemi
- **Forum** — Kullanıcıların analizlerini paylaşabildiği sosyal etkileşim alanı
- **Portföy** — Finansal varlıkların ve kullanıcı takip listelerinin yönetimi
- **Trade Günlüğü** — Gerçekleştirilen işlemlerin ve analiz geçmişinin kaydedilmesi

## Yapay Zekâ Modülü

Projenin yapay zekâ tarafında **Qwen2.5-0.5B-Instruct** taban modeli kullanılmıştır.

Model, Türkçe kripto ve finans alanına uyarlanmak amacıyla **LoRA / QLoRA** yöntemiyle fine-tuning işleminden geçirilmiş ve **FastAPI** servisi üzerinden platforma entegre edilmiştir.

Yapay zekâ sistemi iki farklı kullanım biçimine sahiptir:

- **FinansAI Sohbet Modu:** Finans ve kripto kavramları hakkında Türkçe soru-cevap desteği
- **Doğal Dil Komut Modu:** `"BTC grafiğine RSI ekle"` gibi komutların analiz edilerek grafik ve teknik analiz işlemlerine dönüştürülmesi

Doğal dil komut tarafı kural tabanlı bir parser ile çalışmaktadır.

## Model Eğitimi

Özel LLM adaptörünün eğitim sürecinde:

- Qwen2.5-0.5B-Instruct taban modeli
- LoRA / 4-bit QLoRA
- Google Colab T4 GPU
- 1.106 eğitim örneği
- 96 doğrulama örneği
- ChatML veri formatı
- 4 epoch
- Learning rate: `2e-4`
- LoRA rank: `16`
- LoRA alpha: `32`
- LoRA dropout: `0.05`

kullanılmıştır.

Modelin yalnızca yaklaşık **%1,75'lik parametre alt kümesi** eğitilmiş ve eğitim çıktısı LoRA adaptörü olarak kaydedilmiştir.

## FinansAI Fine-Tuning Eğitim Verisi

FinansAI modelinin Türkçe finans ve kripto alanına uyarlanması amacıyla hazırlanan **1.106 örnekten oluşan fine-tuning eğitim verisi** repository içerisinde paylaşılmıştır.

Veri seti; finans ve kripto kavramlarına yönelik soru-cevap örneklerinin yanı sıra modelin:

- Finans ve kripto alanında kalması
- Riskleri vurgulaması
- Kesin yatırım tavsiyesi vermemesi
- Kullanıcı sorularına Türkçe ve açıklayıcı yanıtlar üretmesi

gibi davranışlarını şekillendirmek amacıyla hazırlanmış instruction örneklerini içermektedir.

📄 [FinansAI Fine-Tuning Eğitim Verisini Görüntüle](./train.jsonl)

## Sistem Mimarisi

Platform modüler ve katmanlı bir mimari anlayışıyla geliştirilmiştir.

Temel yapı:

`Kullanıcı Arayüzü → REST API → Uygulama Servisleri → Veri Katmanı / Harici Servisler`

Sistem içerisinde finansal veri, kullanıcı yönetimi, yapay zekâ, teknik analiz, forum, portföy ve trade günlüğü işlevleri ayrı modüller halinde ele alınmıştır.

## Kullanılan Teknolojiler

### Frontend

`React.js` `HTML` `CSS` `JavaScript`

### Backend ve API

`Spring Boot` `PHP` `REST API`

### Yapay Zekâ

`Python` `FastAPI` `Qwen2.5-0.5B-Instruct` `LoRA` `QLoRA` `NLP`

### Veritabanı

`Microsoft SQL Server`

### Harici Servis ve Araçlar

`Binance API` `Postman` `Swagger` `Google Colab`

## Teknik Analiz

Platform üzerinde finansal varlıkların gerçek zamana yakın verileri görüntülenebilmekte ve çeşitli teknik analiz işlemleri gerçekleştirilebilmektedir.

Proje kapsamında kullanılan başlıca teknik göstergeler arasında:

`RSI` `EMA` `MACD` `Bollinger Bands`

gibi indikatörler bulunmaktadır.

## Kullanıcı Araştırması

Platformun kullanıcı deneyimini değerlendirmek amacıyla **150 katılımcıyla persona çalışması** gerçekleştirilmiştir.

Katılımcılar dört temel profile ayrılmıştır:

- Yapay zekâ odaklı kullanıcı: **51**
- Sade / teknik kullanıcı: **42**
- Pro / analitik kullanıcı: **33**
- Sosyal / topluluk odaklı kullanıcı: **24**

Elde edilen sonuçlar platformun arayüz, FinansAI erişimi ve sosyal özelliklerine ilişkin tasarım kararlarında kullanılmıştır.

## Test Süreci

Platformun temel kullanıcı akışları ve modülleri **17 test senaryosu** üzerinden değerlendirilmiştir.

Testlerde:

- Kullanıcı kayıt ve giriş işlemleri
- FinansAI mesaj ve yanıt akışı
- Doğal dil komut işleme
- Binance piyasa verisi
- Grafik zaman aralıkları
- Teknik indikatörler
- Forum paylaşımı
- API endpoint doğrulaması
- Hata yönetimi
- Modüller arası uçtan uca akış

kontrol edilmiştir.

Test sürecinde **Postman, Swagger ve manuel test senaryoları** kullanılmıştır.

## Proje Raporu

Projenin mimarisi, geliştirme süreci, veritabanı yapısı, yapay zekâ modeli, kullanıcı araştırması, testleri ve sonuçları ayrıntılı olarak final raporunda yer almaktadır.

📄 [Bitirme Projesi Final Raporunu Görüntüle](./FINANCIAL_AI_PLATFORM_FINAL_REPORT.pdf)

## Proje Posterleri

Bitirme projesi kapsamında hazırlanan yatay ve dikey posterler:

📑 [Dikey Proje Posterini Görüntüle](./FINANCIAL_AI_PLATFORM_POSTER_VERTICAL.pdf)

📑 [Yatay Proje Posterini Görüntüle](./FINANCIAL_AI_PLATFORM_POSTER_HORIZONTAL.pdf)

> **Not:** Posterler proje sunumu amacıyla hazırlanmış özet materyallerdir. Güncel ve ayrıntılı teknik bilgiler için final proje raporu esas alınmalıdır.

## Repository Hakkında

Bu repository, projenin **canlı demosunu ve akademik/teknik dokümantasyonunu** bir arada sunmak amacıyla hazırlanmıştır.

Kaynak kodlar bu repository içerisinde yayımlanmamıştır. Projenin çalışan sürümüne canlı demo bağlantısı üzerinden erişilebilir.

🌐 [Canlı Platformu Görüntüle](https://kriptotufan.com/)

## Proje Ekibi

- Mert Uğur
- Furkan Tufan
- Sudenaz Özel
