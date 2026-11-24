# İş Gereksinimleri Dokümanı (BRD): Online Alışveriş İade Süreci İyileştirme

Sürüm 0.1 (taslak) · Hazırlaya[Damla Ertürk] · Tarih: [20.11.2026]

> Bu doküman, bir online alışveriş sitesinin iade sürecini baştan sona inceleyerek elde ettiğim üç bulguya dayanır. "Varsayım" etiketli yerler gözlemle doğrulanacaktır.

## 1. Doküman bilgisi

| Alan | Değer |
|---|---|
| Proje adı | İade süreci iyileştirme |
| Sürüm | 0.1 (taslak) |
| Hazırlayan | [Damla Ertürk] |
| İncelenen site | [Trenyol , Amazon , HepsiBurada] |
| İlgili belgeler | [As-Is şeması](../01-surec-analizi/iade_sureci_as_is.png), [As-Is / To-Be tablosu](../01-surec-analizi/iade_sureci_as_is_to_be_tablo.xlsx), [Pano](../03-pano/index.html), [Jira backlog](iade_jira_backlog.csv) |

| Sürüm | Tarih | Değişiklik | Yazan |
|---|---|---|---|
| 0.1 | [20.11.2026] | İlk taslak | [Damla Ertürk] |

## 2. Amaç ve kapsam

**Amaç:** Müşterinin iade talebini daha az çabayla başlatması, iade kargosunu tanıdık bir firmayla sürdürmesi ve iade sebebini doğru anlatabilmesi. Böylece iade kaynaklı müşteri hizmetleri başvurularının azaltılması hedeflenir.

**Kapsam içi:** İade butonunun yerleşimi, iade sebebi seçimi, iade kargosunun atanması, iade kodu ve etiket bildirimi, iade sebebi raporlama.

**Kapsam dışı:** Para iadesinin bankaya yansıması, satıcı onay süresi, fiyat ve kampanya politikaları, yeni ödeme yöntemleri. Gözlemle bunlar da sorun çıkarırsa sonraki sürüme eklenir.

## 3. İş problemi ve hedefler

| # | Bulgu | Etki |
|---|---|---|
| 1 | İade butonu sipariş ekranında diğer işlemlerin arasında kalıyor | Müşteri butonu bulmakta zorlanıyor, iade talebi gecikiyor, destek başvurusu artabilir (varsayım) |
| 2 | İade kargosu, siparişi teslim eden firmayla aynı akışta ilerlemiyor | Etiket ve kod karışıklığı, takip zorluğu |
| 3 | İade sebebi seçenekleri sınırlı | Müşteri "Diğer"i seçiyor, neden verisi analiz edilemiyor |

**İş hedefleri**

- H1: Müşterinin iade butonuna ulaşma çabasını azaltmak (hedef: sipariş ekranından en fazla 2 tık, varsayım).
- H2: İade talebini açma süresini kısaltmak (hedef: yaklaşık %30 azalış, varsayım).
- H3: İade kargosunu siparişi teslim eden firmayla sürdürmek (hedef: uygun siparişlerin tamamı, varsayım).
- H4: "Diğer" sebebi oranını düşürmek ve sebep verisini kullanılabilir hale getirmek.

**Başarı ölçütleri (KPI)**

| Gösterge | As-Is | To-Be hedefi | Ölçüm yöntemi |
|---|---|---|---|
| İade butonuna tıklama sayısı | [4] | ≤ 2 (varsayım) | Elle sayım, ardından ölçüm olayı (US-03) |
| İade talebini açma süresi | [40, saniye] | As-Is değerinin yaklaşık %70'i (varsayım) | Zaman ölçümü, ardından ölçüm olayı |
| "Diğer" sebebi oranı | [%30] | Belirgin şekilde düşük (varsayım) | İade sebebi raporu (FR-08) |
| İade kargosu destek sorusu | [orta, tahmin] | Azalır (varsayım) | Müşteri hizmetleri kayıtları |

## 4. Paydaşlar

| Paydaş | Rol | Beklentisi | Etki / İlgi |
|---|---|---|---|
| Müşteri (alıcı) | Ana kullanıcı | Kolay, hızlı, anlaşılır iade | Yüksek / Yüksek |
| Müşteri hizmetleri | İade kaynaklı başvuruları yönetir | Daha az tekrarlayan başvuru | Orta / Yüksek |
| Ürün ve UX ekibi | Ekran ve akış tasarımı | Net gereksinim, ölçülebilir hedef | Yüksek / Yüksek |
| Yazılım ekibi | Geliştirme ve entegrasyon | Uygulanabilir, net kapsam | Yüksek / Orta |
| Kargo firmaları | İade taşıma | Standart entegrasyon, doğru etiket | Orta / Orta |
| Satıcılar | İade edilen ürünü teslim alır | Doğru iade sebebi ve hasar bilgisi | Orta / Orta |
| Hukuk ve uyum | Mevzuat ve KVKK | Cayma hakkı ve veri uyumu | Orta / Orta |

Paydaş tablosu genel varsayımdır.

## 5. Mevcut ve hedef durum (özet)

| # | Süreç adımı | As-Is | To-Be |
|---|---|---|---|
| 1 | İade talebini başlatma | İade butonu diğer işlemlerin arasında kalıyor | Sipariş kartında ve detayında ayrı, belirgin "İade Et" butonu |
| 2 | İade kargosu | İade, siparişi teslim eden firmayla aynı akışta ilerlemiyor | İade, aynı kargo firmasıyla devam eder, etiket ve kod otomatik oluşur |
| 3 | İade sebebi seçme | Sınırlı sebep, çoğu zaman "Diğer" | Kategoriye göre ayrıntılı sebep ve alt sebep listesi |

## 6. Gereksinimler

### 6.1 İş gereksinimleri

| ID | Gereksinim | Kaynak |
|---|---|---|
| BR-01 | Müşteri, iade talebini diğer işlemlerden ayrı ve belirgin bir giriş noktasından, en az çabayla başlatabilmelidir. | Bulgu 1 |
| BR-02 | İade gönderisi, siparişi teslim eden kargo firmasıyla devam etmelidir. | Bulgu 2 |
| BR-03 | Müşteri, ürününe uygun ayrıntılı bir sebeple iade başvurusu yapabilmeli, sebep verisi raporlanabilmelidir. | Bulgu 3 |

### 6.2 İşlevsel gereksinimler

| ID | Gereksinim | İlgili BR | Öncelik (MoSCoW) |
|---|---|---|---|
| FR-01 | Sistem, iade hakkı süren siparişlerde sipariş kartında ve detayında diğer işlemlerden ayrı bir "İade Et" butonu göstermelidir. | BR-01 | Must |
| FR-02 | İade süresi dolmuş veya iadeye uygun olmayan ürünlerde buton pasif olmalı ve nedeni kısa bir açıklamayla gösterilmelidir. | BR-01 | Should |
| FR-03 | İade formu, ürün kategorisine göre sebep listesi sunmalı, seçilen sebebe bağlı alt sebep seçimi zorunlu olmalıdır. | BR-03 | Must |
| FR-04 | "Diğer" seçildiğinde serbest açıklama alanı zorunlu olmalıdır. | BR-03 | Should |
| FR-05 | Sistem, onaylanan iade talebinde kargoyu siparişin teslim edildiği firmaya otomatik atamalıdır. Firma iadeyi desteklemiyorsa nedenini belirterek uygun alternatifi önermelidir. | BR-02 | Must |
| FR-06 | Sistem iade kodunu ve etiketini otomatik oluşturmalı, müşteriye e-posta ve uygulama bildirimiyle iletmelidir. | BR-02 | Must |
| FR-07 | Müşteri, iade kargosunun durumunu tek ekrandan takip edebilmelidir. | BR-02 | Should |
| FR-08 | Sistem, iade sebeplerini kategori ve satıcı bazında raporlayabilmelidir. | BR-03 | Could |

### 6.3 İşlevsel olmayan gereksinimler

| ID | Alan | Gereksinim |
|---|---|---|
| NFR-01 | Kullanılabilirlik | İade akışı mobil ve masaüstünde sorunsuz çalışmalı, iade formu en fazla 3 adımda tamamlanabilmelidir (varsayım). |
| NFR-02 | Performans | İade formu ve sebep listesi 3 saniyeden kısa sürede yüklenmelidir (varsayım). |
| NFR-03 | Güvenlik ve KVKK | İade sırasında alınan adres, telefon ve fotoğraf gibi kişisel veriler KVKK'ya uygun işlenmeli ve saklanmalıdır. |
| NFR-04 | Ölçülebilirlik | İade akışı, tıklama ve tamamlama süresini ölçebilecek olay kaydı üretmelidir (US-03). |
| NFR-05 | Erişilebilirlik | Buton ve form alanları klavye ve ekran okuyucuyla kullanılabilmelidir. |

## 7. İş kuralları

| ID | Kural |
|---|---|
| BK-01 | İade hakkı süresi mevzuattaki cayma süresine ve ürün istisnalarına göre belirlenir (genellikle 14 gün). Kesin süre ve istisnalar hukuk ekibiyle doğrulanır (varsayım). |
| BK-02 | Hasarlı veya hatalı ürün sebebinde fotoğraf yüklemesi istenir (varsayım). |
| BK-03 | İade kargo ücretini kimin ödediği site ve satıcı politikasına göre belirlenir [evet]. |
| BK-04 | Siparişi teslim eden firma iadeyi desteklemiyorsa iade, alternatif bir firmaya yönlendirilir. |

## 8. Varsayımlar, kısıtlar ve riskler

**Varsayımlar:** Bu çalışma bir öğrenci projesidir, gerçek bir şirketin sistemine erişimim olmadı. As-Is bilgisi dışarıdan yaptığım gözleme dayanıyor. Hedef değerler (2 tık, %30 azalış) gerçek veriyle değil, makul tahminle belirlendi.

**Bağımlılıklar:** Kargo firmalarının iade etiketi ve kodu entegrasyonu, bildirim servisi, satıcı sistemleri.

| ID | Risk | Etki | Önlem |
|---|---|---|---|
| R-01 | Kargo firması iade entegrasyonunu desteklemiyor | Yüksek | Spike (US-04) ile erken doğrula, alternatif firma kuralını (BK-04) uygula |
| R-02 | Çok uzun sebep listesi formu zorlaştırır | Orta | Kategori bazlı kısa liste ve alt sebep kullan, kullanıcıyla dene |
| R-03 | İade edilemeyen ürün istisnaları kafa karıştırır | Orta | Hukukla doğrula, FR-02 ile müşteriyi bilgilendir |
| R-04 | Gözlem örneklemi küçük kalır | Orta | Daha fazla kişiyle mülakat yap, kısa anket ekle |

## 9. İzlenebilirlik matrisi

| Bulgu | İş gereksinimi | İşlevsel gereksinim | Jira epic | Jira hikayeleri |
|---|---|---|---|---|
| 1 | BR-01 | FR-01, FR-02 | EPIC-1 İade başlatma | US-01, US-02, US-03 |
| 2 | BR-02 | FR-05, FR-06, FR-07 | EPIC-2 İade kargosu | US-04, US-05, US-06, US-07 |
| 3 | BR-03 | FR-03, FR-04, FR-08 | EPIC-3 İade sebebi | US-08, US-09, US-10, US-11 |

## 10. Açık sorular

- İncelenen sitede iade süresi ve iade edilemeyen ürün istisnaları nelerdir?
- İade kargo ücretini kim ödüyor?
- Hangi kargo firmaları iade etiketi ve kodu destekliyor?
- Gözlemlediğin başka sorunlar (satıcı onayı, para iadesi takibi) bu BRD'ye eklensin mi?

## 11. Onay

| Ad | Rol | Tarih | Onay |
|---|---|---|---|
| [Damla Ertürk] | Ürün sahibi | | |
| [Damla Ertürk] | Paydaş temsilcisi | | |
