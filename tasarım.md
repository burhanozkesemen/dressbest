```mermaid
flowchart TD
  %% Roles (visual grouping)
  subgraph R1[PAZARLAMA & SATIŞ / MÜŞTERİ TEMSİLCİSİ]
    A1[Başlat: Müşteri İletişimi]
    A2[Bilgi Toplama<br/>Yatak & personel sayısı, zincir profili]
    A3[Fiyat Politikası ile Değerlendirme]
    A4[Teklif Hazırlama (Tasarım Fiyat Teklifi)]
  end

  subgraph R2[TASARIM SORUMLUSU]
    B1[Konsept Tasarım Çalışması]
    B2[Sunum Dosyası Hazırlama]
    B3[Çizimler ve Renklendirme]
    B4[Tasarım Revizyonları]
    B5[Tasarım Dosyası Teslimi]
  end

  subgraph R3[MÜŞTERİ]
    C1[Müşteri Teklifi Değerlendirir]
    C2[Olumlu]
    C3[Olumsuz]
    C4[Geri Bildirim / Kabul Nedenleri]
  end

  subgraph R4[MUHASEBE]
    D1[Sözleşme ve Ön Ödeme Alımı]
    D2[Fatura Kesimi]
    D3[SAP Bilgilendirmesi (Ödeme alındığında)]
  end

  %% Documents / Ekler
  Offer[Doküman: Tasarım Fiyat Teklifi]
  Contract[Doküman: Tasarım ve Danışmanlık Sözleşmesi]
  DesignFile[Doküman: Tasarım Dosyası]
  Invoice[Doküman: Fatura]
  Samples[Numune: Kumaş / Aksesuar Numuneleri ve Fiyatlar]
  SalesBrief[Satis Brief]
  DesignSample[Tasarım Numunesi (Gerekirse)]

  %% Akış
  A1 --> A2
  A2 --> A3
  A3 --> A4
  A4 --> Offer
  A4 --> C1

  C1 -->|Olumlu| C2
  C1 -->|Olumsuz| C3

  %% Olumlu akış
  C2 --> D1
  D1 --> Contract
  D1 -->|Ön ödeme alındı mı?| PayCheck{Ön ödeme alındı mı?}
  PayCheck -->|Evet| B1
  PayCheck -->|Hayır| WaitPay[Ön ödeme beklenir]

  WaitPay -->|Ön ödeme alındığında| B1

  B1 --> B2
  B2 --> B3
  B3 --> DesignSample
  B3 --> B2
  B3 --> Presentation[Sunum Müşteriye Yapılır]
  Presentation --> C4
  C4 --> B4
  B4 --> B5
  B5 --> DesignFile
  B5 --> D2
  D2 --> Invoice
  D2 --> D3
  D3 --> End[Proje Kapanışı]

  %% Olumsuz akış
  C3 --> Samples
  Samples --> OfferReview[Teklifin neden kabul edilmediği görüşülür]
  OfferReview --> FileClose[Dosya kapatılır veya revize edilir]
  FileClose --> End

  %% İlgili doküman bağlantıları
  Offer --> SalesBrief
  DesignFile --> Invoice
  Contract --> D1

  %% İyileştirme / Yapılacaklar (Süreç dışı ama bağlı)
  subgraph Improvements[Yapılacaklar / Süreç İyileştirme]
    I1[Tasarım PDF'lerinin sadeleştirilmesi ve merkezi depolama]
    I2[Müşteri brieflerinin yeni formata geçirilmesi]
    I3[Müşteri kontratlarının merkezi toplanacağı yer (ör. Dubai benzeri)]
    I4[Satış ve Tasarım için aynı kod/etiketleme sistemi]
  end

  %% Bağlantılar: iyileştirmeler sürece etki eder
  I1 -.-> B2
  I2 -.-> A4
  I3 -.-> D1
  I4 -.-> A3

  %% Görüşme / geri bildirim döngüsü
  Presentation -->|Geri bildirim| C4
  C4 -->|Kritikler alındı| B4
  B4 -->|Değişiklik yapıldı| B3

  %% Notlar
  classDef doc fill:#f9f,stroke:#333,stroke-width:1px;
  class Offer,Contract,DesignFile,Invoice,Samples,SalesBrief,DesignSample doc;
