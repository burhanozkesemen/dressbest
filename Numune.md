```mermaid
graph TD
    %% Belge Bilgisi
    subgraph Belge_Kutusu [NUMUNE HAZIRLAMA İŞ AKIŞI - IA.03]
        direction TB
        doc_info["Yayın Tarihi: 30.11.2009 -- Revizyon: 0 -- Sayfa: 3"]
    end

    %% SAYFA 1: Tasarım ve Hazırlık
    S1_Basla[TASARIM SORUMLUSU] --> S1_Adim1["Numune hazırlanacak modellere ilişkin ayrıntılar müşteri beklentileri doğrultusunda değerlendirilir. Model, artwork çalışmaları (baskı, nakış, logo) ve dikiş özellikleri belirlenir."]
    S1_Adim1 --- S1_Tasarimci[TASARIMCI]

    S1_Adim1 --> S1_Adim2["Modellere ilişkin formlar hazırlanır, teknik çizimleri yapılır. Modellere ilişkin kumaş, malzeme ve aksesuar varsa depodan, yoksa piyasadan temin edilir."]
    S1_Adim2 --- S1_TeknikCizim[TEKNİK ÇİZİM GÖREVLİSİ]

    %% Sayfa 1 Yan Bağlantılar (Kesikli Çizgiler Dahil)
    S1_Adim2 -.-> S1_DepoCikis[DEPO ÇIKIŞ]
    S1_DepoCikis --- S1_DepoGor[DEPO GÖREVLİSİ]
    S1_DepoGor -.-> S1_Planlama[PLANLAMA SATINALMA SORUMLUSU]
    
    S1_Adim2 --> S1_MalzemeTedarik[KUMAŞ / MALZEME / AKSESUAR]
    S1_MalzemeTedarik --- S1_MalzemeGor[MALZEME GÖREVLİSİ]
    S1_MalzemeGor --> S1_Tedarikci[TEDARİKÇİLER]
    S1_MalzemeTedarik -.-> S1_Fatura_Ref[FATURA]

    S1_Adim2 --> S1_ModelKarti[Model Kartı]
    S1_ModelKarti --- S1_Modelist[MODELİST]

    %% Sayfalar Arası Bağlantılar (1 -> 2)
    S1_Modelist -- "a" --> S2_Adim3["Numune için gerekli kalıplar, ölçü tabloları ve dikiş talimatı hazırlanır."]
    S1_MalzemeTedarik -- "b" --> S2_MalzemeRef[KUMAŞ / AKSESUAR / MALZEME]

    %% SAYFA 2: Kesim ve Dikim
    S2_Adim3 --> S2_DikimGiris["Dikiş / KALIPLAR"]
    S2_DikimGiris --- S2_ModelDikimSor[MODEL DİKİM SORUMLUSU]
    
    S2_DikimGiris --> S2_Adim4["Kumaş kesimi yapılır, baskı ve nakış için gerekli parçalar hazırlanır."]
    S2_Adim4 --- S2_Modelist2[MODELİST]

    %% Baskı/Nakış Akışı
    S2_Adim4 --> S2_BaskiGidis[BASKI VE NAKIŞA GİDECEK İŞLER]
    S2_BaskiGidis --- S2_MalzemeGor2[MALZEME GÖREVLİSİ]
    S2_BaskiGidis --> S2_BaskiIslem["Baskı ve nakış işlemleri yaptırılır."]
    S2_BaskiIslem --> S2_BaskiDonus[BASKI VE NAKIŞTAN GELEN İŞLER]

    %% Dikim ve Kontrol
    S2_BaskiDonus --> S2_Adim5["Dikiş işlemleri tamamlanır ve Numuneler dikilir."]
    S2_Adim5 -.-> S2_AraKontrol["Dikiş esnasında ara kontroller yapılır."]
    S2_AraKontrol -.-> S2_Modelist_Ref[MODELİST]
    S2_Adim5 --> S2_Numuneler[NUMUNELER]

    %% Sayfalar Arası Bağlantılar (2 -> 3)
    S2_BaskiIslem -- "c" --> S3_Fatura["Fatura (Baskı-Nakış) İrsaliye"]
    S2_Numuneler -- "d" --> S3_NumuneGor[NUMUNE GÖREVLİSİ]

    %% SAYFA 3: Kontrol ve Arşiv
    S3_Fatura --- S3_TasarimSor[TASARIM SORUMLUSU]
    S3_Fatura --> S3_Adim6["Harcama belgeleri değerlendirilir ve onaylanır."]
    S3_Adim6 --> S3_Muhasebe[MUHASEBE SORUMLUSU]
    S3_Muhasebe -.-> S3_TasarimSor_Ref[TASARIM SORUMLUSU]

    S3_NumuneGor --> S3_Adim7["Numunelerin son kontrolü yapılır."]
    S3_Adim7 --- S3_Tasarimci2[TASARIMCI]
    
    S3_Adim7 --> S3_Adim8["Son değerlendirmeler yapılır, bilgisayar kayıtlarına geçirilir, modellerin fotoğrafları çekilir ve arşiv dosyaları oluşturulur. Maliyet Formu hazırlanır."]
    S3_Adim8 --- S3_Modelist3[MODELİST]

    %% Kapanış
    S3_Adim8 --> S3_MaliyetFormu[Maliyet Formu]
    S3_MaliyetFormu --- S3_MusteriTem[MÜŞTERİ TEMSİLCİSİ]
    S3_MusteriTem --> S3_FinalNumune[NUMUNELER]
    S3_FinalNumune --> S3_Maliyet[Maliyet]
    S3_Maliyet --> S3_Arsiv[/KOLLEKSİYON DOSYASI/]

    %% Stil Tanımları
    style S3_Arsiv fill:#f9f,stroke:#333
    style S2_BaskiIslem fill:#fff,stroke:#000
    style S3_Fatura fill:#fff,stroke:#000
