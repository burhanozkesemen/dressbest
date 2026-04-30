```mermaid
graph TD
    %% Belge Bilgisi ve Başlık
    subgraph Belge_Kutusu [NUMUNE HAZIRLAMA İŞ AKIŞI - IA.03]
        direction TB
        doc_info[Yayın Tarihi: 30.11.2009 -- Revizyon: 0 -- Sayfa: 3]
    end

    %% SAYFA 1: Tasarım ve Hazırlık Süreci
    S1_Basla[TASARIM SORUMLUSU] --> S1_Adim1[Numune hazırlanacak modellere ilişkin ayrıntılar müşteri beklentileri doğrultusunda değerlendirilir. Model, artwork çalışmaları -baskı, nakış, logo- ve dikiş özellikleri belirlenir.]
    S1_Adim1 --- S1_Tasarimci[TASARIMCI]

    S1_Adim1 --> S1_Adim2[Modellere ilişkin formlar hazırlanır, teknik çizimleri yapılır. Modellere ilişkin kumaş, malzeme ve aksesuar varsa depodan, yoksa piyasadan temin edilir.]
    S1_Adim2 --- S1_TeknikCizim[TEKNİK ÇİZİM GÖREVLİSİ]

    %% Sayfa 1 Yan Bağlantılar
    S1_Adim2 -.-> S1_Depo[DEPO ÇIKIŞ]
    S1_Depo --- S1_DepoGor[DEPO GÖREVLİSİ][cite: 1]
    S1_DepoGor -.-> S1_Planlama[PLANLAMA SATINALMA SORUMLUSU][cite: 1]
    
    S1_Adim2 --> S1_MalzemeTedarik[KUMAŞ / MALZEME / AKSESUAR][cite: 1]
    S1_MalzemeTedarik --- S1_MalzemeGor[MALZEME GÖREVLİSİ][cite: 1]
    S1_MalzemeGor --> S1_Tedarikci[TEDARİKÇİLER][cite: 1]
    S1_MalzemeTedarik -.-> S1_Fatura_Ref[FATURA][cite: 1]

    S1_Adim2 --> S1_ModelKarti[Model Kartı][cite: 1]
    S1_ModelKarti --- S1_Modelist[MODELİST][cite: 1]

    %% Sayfalar Arası Bağlantılar (1'den 2'ye)
    S1_Modelist -- "a" --> S2_Adim3[Numune için gerekli kalıplar, ölçü tabloları ve dikiş talimatı hazırlanır.][cite: 1]
    S1_MalzemeTedarik -- "b" --> S2_MalzemeRef[KUMAŞ / AKSESUAR / MALZEME][cite: 1]

    %% SAYFA 2: Kesim ve Üretim Süreci
    S2_Adim3 --> S2_DikimGiris[Dikiş / KALIPLAR][cite: 1]
    S2_DikimGiris --- S2_ModelDikimSor[MODEL DİKİM SORUMLUSU][cite: 1]
    
    S2_DikimGiris --> S2_Adim4[Kumaş kesimi yapılır, baskı ve nakış için gerekli parçalar hazırlanır.][cite: 1]
    S2_Adim4 --- S2_Modelist2[MODELİST][cite: 1]

    %% Baskı ve Nakış Alt Süreci
    S2_Adim4 --> S2_BaskiGidis[BASKI VE NAKIŞA GİDECEK İŞLER][cite: 1]
    S2_BaskiGidis --- S2_MalzemeGor2[MALZEME GÖREVLİSİ][cite: 1]
    S2_BaskiGidis --> S2_BaskiIslem[Baskı ve nakış işlemleri yaptırılır.][cite: 1]
    S2_BaskiIslem --> S2_BaskiDonus[BASKI VE NAKIŞTAN GELEN İŞLER][cite: 1]

    %% Dikim ve Ara Kontrol
    S2_BaskiDonus --> S2_Adim5[Dikiş işlemleri tamamlanır ve Numuneler dikilir.][cite: 1]
    S2_Adim5 -.-> S2_AraKontrol[Dikiş esnasında ara kontroller yapılır.][cite: 1]
    S2_AraKontrol -.-> S2_Modelist_Ref[MODELİST][cite: 1]
    S2_Adim5 --> S2_Numuneler[NUMUNELER][cite: 1]

    %% Sayfalar Arası Bağlantılar (2'den 3'e)
    S2_BaskiIslem -- "c" --> S3_Fatura[Fatura -Baskı-Nakış- İrsaliye][cite: 1]
    S2_Numuneler -- "d" --> S3_NumuneGor[NUMUNE GÖREVLİSİ][cite: 1]

    %% SAYFA 3: Kontrol, Onay ve Arşivleme
    S3_Fatura --- S3_TasarimSor[TASARIM SORUMLUSU][cite: 1]
    S3_Fatura --> S3_Adim6[Harcama belgeleri değerlendirilir ve onaylanır.][cite: 1]
    S3_Adim6 --> S3_Muhasebe[MUHASEBE SORUMLUSU][cite: 1]
    S3_Muhasebe -.-> S3_TasarimSor_Ref[TASARIM SORUMLUSU][cite: 1]

    S3_NumuneGor --> S3_Adim7[Numunelerin son kontrolü yapılır.][cite: 1]
    S3_Adim7 --- S3_Tasarimci2[TASARIMCI][cite: 1]
    
    S3_Adim7 --> S3_Adim8[Son değerlendirmeler yapılır, bilgisayar kayıtlarına geçirilir, modellerin fotoğrafları çekilir ve arşiv dosyaları oluşturulur. Maliyet Formu hazırlanır.][cite: 1]
    S3_Adim8 --- S3_Modelist3[MODELİST][cite: 1]

    %% Final Adımları
    S3_Adim8 --> S3_MaliyetFormu[Maliyet Formu][cite: 1]
    S3_MaliyetFormu --- S3_MusteriTem[MÜŞTERİ TEMSİLCİSİ][cite: 1]
    S3_MusteriTem --> S3_FinalNumune[NUMUNELER][cite: 1]
    S3_FinalNumune --> S3_Maliyet[Maliyet][cite: 1]
    S3_Maliyet --> S3_Arsiv[/KOLLEKSİYON DOSYASI/][cite: 1]

    %% Stil Tanımları
    style S3_Arsiv fill:#f9f,stroke:#333,stroke-width:2px
    style S2_BaskiIslem fill:#fff,stroke:#000
    style S3_Fatura fill:#fff,stroke:#000
    style doc_info fill:#f4f4f4,stroke:#333
