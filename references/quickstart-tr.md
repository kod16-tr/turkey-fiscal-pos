# Hızlı Başlangıç (Türkçe)

> Hukuki veya vergi danışmanlığı değildir. Kurallar değişir; GİB ve mali müşavirinizle doğrulayın.

**Temel kural:** Her satış mali iz bırakmalı. Ya ÖKC (yazarkasa) mali fiş basar ya da fatura (e-Arşiv / e-Fatura) kesilir ve ÖKC bilgi fişi basar. Aynı satışa hem fiş hem fatura olmaz.

| Durum | Belge |
|---|---|
| Tezgâh / restoran, tüketici | ÖKC fişi |
| Tutar fatura sınırını aşıyor (2026: 12.000 TL) ya da müşteri istiyor | e-Arşiv Fatura + bilgi fişi |
| Alıcı e-Fatura kullanıcısı | e-Fatura |
| İnternet satışı, adrese teslim | e-Arşiv Fatura |
| Masaya servis, GİB tarafından belirlenmişseniz | e-Adisyon |

**Akış:** sepet → ödeme (nakit / kart / yemek kartı / parçalı) → ÖKC mali belgeyi kapatır → fiş no ve Z no uygulamaya döner → kayıt.

**KDV:** %20 genel, %10 ve %1 indirimli (10.07.2023'ten beri). Her ürün bir kısma/KDV grubuna bağlı olmalı. Yuvarlamayı cihaz gibi KDV grubu bazında yapın.

**Yemek kartı:** Multinet, Pluxee (Sodexo), Edenred, Setcard, Metropol ayrı ödeme tipi olarak tutulmalı; işlem no ile fiş no birlikte saklanmalı.

**Gün sonu:** Açık satış bırakmayın, her satış gününde Z raporu alın, Z toplamlarını KDV ve ödeme tipine göre mutabık edin.

**Sık hata:** Zaman aşımında körlemesine tekrar göndermek (çift fiş). Idempotency anahtarı kullanın, önce cihaz durumunu sorgulayın.

Ayrıntılar: `01`–`06` dosyaları, kaynaklar: `sources.md`.

Yardım: KOD16 Digital Solutions, info@kod16.com.tr
