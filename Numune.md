```mermaid

graph TD
    %% Belge Başlığı ve Bilgileri
    subgraph Belge_Bilgisi [NUMUNE HAZIRLAMA İŞ AKIŞI - IA.03]
        direction TB
        info[Yayın Tarihi: 30.11.2009 | Revizyon: 0 | Sayfa: 3/3]
    end

    %% SAYFA 1: Tasarım ve Hazırlık
    S1_Basla[TASARIM SORUMLUSU] --> S1_Box1[Numune hazırlanacak modellere ilişkin ayrıntılar müşteri beklentileri doğrultusunda değerlendirilir. Model, artwork çalışmaları -baskı, nakış, logo- ve dikiş özellikleri belirlenir.]
    S1_Box1 --- S1_Tasarimci[TASARIMCI]

    S1_Box1 --> S1_Box2[Modellere ilişkin formlar hazırlanır, teknik çizimleri yapılır. Modellere ilişkin kumaş, malzeme ve aksesuar varsa depodan, yoksa piyasadan temin edilir.]
    S1_Box2 --- S1_TeknikCizim[TEKNİK ÇİZİM GÖREVLİSİ]

    %% Sayfa 1 - Yan Süreçler
    S1_Box2 -.-> S1_DepoCikis[DEPO ÇIKIŞ]
    S1_DepoCikis --- S1_DepoGor[DEPO GÖREVLİSİ]
    S1_DepoGor -.-> S1_Planlama[PLANLAMA SATINALMA SORUMLUSU]
    
    S1_Box2 --> S1_Malzeme_Tedarik[KUMAŞ / MALZEME / AKSESUAR]
    S1_Malzeme_Tedarik --- S1_MalzemeGor[MALZEME GÖREVLİSİ]
    S1_MalzemeGor --> S1_Tedarikci[TEDARİKÇİLER]

    S1_Box2 --> S1_ModelKarti[Model Kartı]
    S1_ModelKarti --- S1_Modelist[MODELİST]

    %% Bağlantı Noktaları (Sayfa 1'den 2'ye geçiş)
    S1_Modelist -- "a" --> S2_Box3[Numune için gerekli kalıplar, ölçü tabloları ve dikiş talimatı hazırlanır.]
    S1_Malzeme_Tedarik -- "b" --> S2_MalzemeTransfer[KUMAŞ / AKSESUAR / MALZEME]

    %% SAYFA 2: Kesim ve Dikim
    S2_Box3 --> S2_DikimGiris[Dikiş / KALIPLAR]
    S2_DikimGiris --- S2_ModelDikimSor[MODEL DİKİM SORUMLUSU]
    
    S2_DikimGiris --> S2_Box4[Kumaş kesimi yapılır, baskı ve nakış için gerekli parçalar hazırlanır.]
    S2_Box4 --- S2_Modelist2[MODELİST]

    %% Baskı/Nakış Yan Akışı
    S2_Box4 --> S2_BaskiNakisGidis[BASKİ VE NAKIŞA GİDECEK İŞLER]
    S2_BaskiNakisGidis --- S2_MalzemeGor2[MALZEME GÖREVLİSİ]
    S2_BaskiNakisGidis --> S2_Box5[Baskı ve nakış işlemleri yaptırılır.]
    S2_Box5 --> S2_BaskiNakisDonus[BASKI VE NAKIŞTAN GELEN İŞLER]

    %% Dikim ve Kontrol
    S2_BaskiNakisDonus --> S2_Box6[Dikiş işlemleri tamamlanır ve Numuneler dikilir.]
    S2_Box6 --- S2_AraKontrol[Dikiş esnasında ara kontroller yapılır.]
    S2_Box6 --> S2_Numuneler[NUMUNELER]

    %% Bağlantı Noktaları (Sayfa 2'den 3'e geçiş)
    S2_Box5 -- "c" --> S3_Fatura[Fatura -Baskı-Nakış- İrsaliye]
    S2_Numuneler -- "d" --> S3_NumuneGor[NUMUNE GÖREVLİSİ]

    %% SAYFA 3: Kontrol, Maliyet ve Arşiv
    S3_Fatura --- S3_TasarimSor[TASARIM SORUMLUSU]
    S3_Fatura --> S3_Box9[Harcama belgeleri değerlendirilir ve onaylanır.]
    S3_Box9 --> S3_Muhasebe[MUHASEBE SORUMLUSU]
    S3_Muhasebe --- S3_TasarimSor2[TASARIM SORUMLUSU]

    S3_NumuneGor --> S3_Box11[Numunelerin son kontrolü yapılır.]
    S3_Box11 --- S3_Tasarimci2[TASARIMCI]
    
    S3_Box11 --> S3_Box12[Son değerlendirmeler yapılır, bilgisayar kayıtlarına geçirilir, modellerin fotoğrafları çekilir ve arşiv dosyaları oluşturulur. Maliyet Formu hazırlanır.]
    S3_Box12 --- S3_Modelist3[MODELİST]

    %% Final Adımları
    S3_Box12 --> S3_MaliyetFormu[Maliyet Formu]
    S3_MaliyetFormu --- S3_MusteriTem[MÜŞTERİ TEMSİLCİSİ]
    S3_MusteriTem --> S3_FinalNumune[NUMUNELER]
    S3_FinalNumune --> S3_Maliyet[Maliyet]
    S3_Maliyet --> S3_Arsiv[/KOLLEKSİYON DOSYASI/]

    %% Stil Tanımlamaları
    style S3_Arsiv fill:#f9f,stroke:#333,stroke-width:2px
    style S1_Basla fill:#fff,stroke:#000
    style S3_Fatura fill:#fff,stroke:#000
    style S1_DepoGor fill:#f0f0f0,stroke:#333
    style S3_Muhasebe fill:#f0f0f0,stroke:#333
