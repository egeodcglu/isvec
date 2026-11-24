# İsveç Makale Sitesi (GEO ve Web Performansı Odaklı Statik Proje)

Bu depo, İsveç'in coğrafi, tarihi, ekonomik, kültürel ve idari yapısını ele alan; klasik ansiklopedi mizanpajı ile modern web standartlarını (Generative Engine Optimization - GEO, anlamsal HTML ve Core Web Vitals) bir araya getiren statik bir web sitesidir.

- **Canlı Site:** https://egeodcglu.github.io/isvec/
- **Kaynak Depo:** https://github.com/egeodcglu/isvec
- **Yayın Dalı:** main

---

## Projenin Amacı ve Kapsamı

Projenin temel amacı, hem geleneksel arama motorları hem de yeni nesil üretken yapay zekâ sistemleri (ChatGPT, Google Gemini, Perplexity, Claude, Copilot vb.) tarafından doğrudan taranabilir, anlaşılabilir ve alıntılanabilir (citable) bir referans bilgi kaynağı oluşturmaktır.

Görsel tasarımda İsveç'in ulusal renkleri (koyu mavi `#004B76`, lacivert `#003D60` ve İsveç sarısı `#FECC02`) temel alınmış; SaaS şablonlarından, gereksiz animasyonlardan ve geçiş efektlerinden arındırılmış yalın bir araştırma sitesi kurgulanmıştır.

---

## Kullanılan Teknolojiler

- **HTML5:** Semantik etiketler (`article`, `aside`, `section`, `figure`, `figcaption`, `time`, `sup`), mikrodata ve Schema.org yapılandırmaları.
- **CSS3:** Merkezi CSS değişkenleri (`:root`), Flexbox tabanlı 3 sütunlu ızgara, responsive medya sorguları (`@media`) ve CSS reset kuralları.
- **JavaScript Durumu:** Projede harici veya dahili herhangi bir JavaScript kütüphanesi (jQuery, React, Vue, Bootstrap, Tailwind vb.) kullanılmamıştır. Statik bir makale sitesinde dinamik script ihtiyacı bulunmadığından, ana iş parçacığı (main thread) yükünü sıfıra indirmek ve render blocking gecikmelerini önlemek amacıyla tamamen saf HTML ve CSS mimarisi tercih edilmiştir.

---

## Dosya ve Dizin Yapısı

```text
.
├── README.md           # Proje dokümantasyonu
├── index.html          # Ana makale, semantik yapı ve JSON-LD şemaları
├── style.css           # Merkezi renkler, tipografi ve duyarlı yerleşim kuralları
├── robots.txt          # Arama ve yapay zekâ botlarına yönelik dizinleme direktifleri
├── sitemap.xml         # Standart arama motoru site haritası
├── llms.txt            # LLM tarayıcıları için doğrudan özet ve kaynak rehberi
└── img/                # Sayfada kullanılan optimize edilmiş görseller
    ├── isvec-kapak.png # İsveç bayrağı (header)
    ├── stockholm.jpg   # LCP odaklı Gamla Stan başlık görseli
    ├── nl1.jpg         # Kuzey Işıkları (galeri)
    ├── vasa.jpg        # Vasa Müzesi (galeri)
    └── midnightsun.jpg # Gece Yarısı Güneşi (galeri)
```

---

## Web Performansı ve Core Web Vitals İyileştirmeleri

Sitede yüksek sayfa yükleme hızı ve kararlılığı sağlamak üzere uygulanan teknik optimizasyonlar şunlardır:

1. **Largest Contentful Paint (LCP):**
   - İlk ekranda yer alan ana başlık görseline (`img/stockholm.jpg`) `fetchpriority="high"` niteliği verilmiş, `loading="lazy"` niteliği ise kaldırılarak tarayıcının görseli en yüksek öncelikle indirmesi sağlanmıştır.
   - Harici font sunucuları (Google Fonts vb.) elenerek yerel sistem fontları (`Arial, Helvetica, sans-serif`) kullanılmış; harici DNS çözümleme, TLS el sıkışma ve render-blocking font gecikmeleri sıfırlanmıştır.

2. **Cumulative Layout Shift (CLS):**
   - Sayfa kaymalarını tamamen engellemek amacıyla tüm `<img>` ve `<iframe>` etiketlerine piksel bazında kesin `width` ve `height` öznitelikleri tanımlanmıştır (`stockholm.jpg`: 2081x1080, `nl1.jpg`: 900x600 vb.).
   - CSS tarafında `aspect-ratio` oranları tanımlanarak görsel yüklenmeden önce alan rezerve edilmiştir (Laboratuvar CLS hedefi: `0.00`).

3. **First Input Delay (FID) / Interaction to Next Paint (INP) ve Total Blocking Time (TBT):**
   - Sayfada hiçbir JavaScript kodu çalışmadığından tarayıcının ana iş parçacığı (main thread) tamamen boşta kalmakta, kullanıcı etkileşimlerine anında yanıt verilmektedir.

4. **Bant Genişliği ve Sayfa Altı Kaynaklar:**
   - Ekranın alt kısmında kalan galeri görsellerine (`nl1.jpg`, `vasa.jpg`, `midnightsun.jpg`) `loading="lazy"` ve `decoding="async"` öznitelikleri tanımlanmıştır.
   - Tarayıcı önbelleğinin gecikmesini önlemek amacıyla stil bağlantısında sürüm takibi uygulanmıştır (`style.css?v=2`).

*Not: Sitede henüz CrUX (Chrome User Experience Report) için yeterli kullanıcı hacmi oluşmadığından gerçek kullanıcı saha verileri (Field Data) bulunmamaktadır; değerler statik mimari ve laboratuvar parametreleriyle güvence altına alınmıştır.*

---

## SEO ve Generative Engine Optimization (GEO)

Yapay zekâ modellerinin ve arama botlarının içeriği kolayca parse edebilmesi için uygulanan standartlar:

- **Yapılandırılmış Veriler (Schema.org JSON-LD):**
  - `WebSite`: Site kimliği ve dil tanımlaması (`tr`).
  - `Country`: İsveç Krallığı varlık kaydı, Wikidata ID (`Q34`), başkent, para birimi ve resmî adlar.
  - `Article`: Makale başlığı, yazar, son güncelleme tarihi ve alıntı kaynakları listesi.
  - `FAQPage`: Sayfada yer alan 16 soru-cevabın arama motorlarıyla birebir eşleşen yapısal soru şeması.
- **Başlık Hiyerarşisi:** Sayfada yalnızca tek bir `<h1>` başlığı (`article > h1`) kullanılmış; tüm alt bölümler hiyerarşik olarak `h2` ve `h3` etiketleriyle yapılandırılmıştır.
- **Bağımsız Bölüm Yapısı:** Her bölüm kendi içinde doğrudan cevabı veren ilk 1-2 cümleyle başlamaktadır.
- **Karşılaştırmalı Veri Tabloları:** Tarihçe, ekonomi, iklim ve mutfak verileri anlamsal `<table>`, `caption`, `thead` ve `th scope="col"` etiketleriyle tablolaştırılmıştır.
- **llms.txt Standardı:** LLM botlarının site içeriğini özet olarak okuyabilmesi için kök dizinde standartlara uygun `llms.txt` dosyası sunulmuştur.
- **robots.txt Yapılandırması:** Geleneksel arama botları (Googlebot, Bingbot), gerçek zamanlı AI arama botları (OAI-SearchBot, PerplexityBot, Claude-SearchBot) ve model eğitim botları (GPTBot, CCBot) izinli olarak tanımlanmıştır.
- **Doğrulanmış Kaynakça:** 15 maddelik kaynakçada genel ana sayfalar yerine doğrudan ilgili veriyi kanıtlayan resmî alt sayfa bağlantıları (`scb.se`, `riksbank.se`, `visitsweden.com`, `nato.int` vb.) kullanılmıştır.

---

## Responsive Tasarım ve Mobil Uyumluluk

Sitenin 360px ile 1920px arasındaki ekran genişliklerinde test edilen duyarlı tasarım özellikleri:

- **Masaüstü (1100px - 1920px):** 3 sütunlu editoryal düzen. Solda sabit (sticky) İçindekiler menüsü (`#003D60`), ortada ana makale, sağda ülke bilgi paneli ve fotoğraf galerisi (`#003D60`).
- **Tablet (601px - 1100px):** Sütunlar dikey akışa geçer; İçindekiler menüsü ve yan panel dikey olarak akıcı biçimde sıralanır.
- **Mobil (360px - 600px):** Tek sütunlu okuma akışı; tablolar için yatay taşmasız kaydırma (`.table-container`), dokunmatik dostu bağlantı alanları.

**Erişilebilirlik (WCAG 2.2 AA):**
- Beyaz metin / Koyu mavi zemin: `9.26:1` kontrast (AAA seviyesi).
- Sarı başlık / Koyu mavi zemin: `6.11:1` kontrast (AA seviyesi).
- Klavye navigasyonu için `:focus-visible` sarı dış hat göstergesi (`outline: 2px solid #FECC02`).

---

## Yerel Ortamda Çalıştırma

Proje herhangi bir derleme aracı (Node build, Webpack, Vite vb.) gerektirmez. Doğrudan bir web sunucusu ile çalıştırılabilir:

Python ile:
```bash
python -m http.server 8000
```

Node.js (npx) ile:
```bash
npx serve .
```

Ardından tarayıcınızdan `http://localhost:8000` adresine gidebilirsiniz.

---

## GitHub Pages ile Yayınlama

Proje GitHub Pages üzerinden doğrudan `main` dalından kök dizin (`/root`) kaynak gösterilerek sunulmaktadır. Yapılan her `git push origin main` işlemi sonrasında GitHub Actions derlemeyi otomatik olarak tetikler ve sayfayı yayına alır.
