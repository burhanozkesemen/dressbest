```mermaid
graph TD
    %% Belge Bilgileri
    subgraph Belge_Kutusu [SİPARİŞ İŞ AKIŞI | Doküman No: IA.02 | Yayın: 30.11.2008]
        direction TB
        info1[Revizyon No: 0]
        info2[Sayfa Sayısı: 4]
    end

    %% SAYFA 1: Başlangıç ve Teklif
    S1_Musteri([MÜŞTERİ]) --> S1_Siparis[SİPARİŞ / MÜŞTERİ TEMSİLCİSİ]
    S1_Siparis --> S1_Gorusme[Müşteri ile görüşmeler yapılır. Departmanlar bazında personel sayısı ve beden dağılımı alınır. Tasarım ve modeller gözden geçirilerek hiyerarşik yapıya göre adlandırılır.]
    S1_Gorusme --- Tasarim_Sor[TASARIM SORUMLUSU]
    
    S1_Gorusme --> S1_Maliyet[Modeller, önerilen kumaş, aksesuar ve birim metrajlar bazında birim maliyetler çıkartılır. Kar marjları eklenerek satış fiyatı belirlenir ve Bütçe hazırlanır.]
    S1_Maliyet --> S1_Pazarlama[PAZARLAMA VE SATIŞ MÜDÜRÜ]
    S1_Pazarlama --> S1_Onay{Onay Alınır}
    S1_Onay --> S1_Butce[BÜTÇE]
    S1_Butce --> S1_Musteri_Onay[MÜŞTERİ]

    %% SAYFA 2: Müşteri Değerlendirme ve Sözleşme
    S1_Musteri_Onay -- "a" --> S2_Degerlendirme[Müşteri teklifi değerlendirir. Gerekli durumlarda Bütçe revize edilir.]
    S2_Degerlendirme --> S2_Soru{Teklif Hakkında Bilgi}
    
    S2_Soru -- Hayır --> S2_Dosya_Kapat[Müşteri ile görüşülerek teklifin niçin kabul edilmediği öğrenilir ve dosya kapatılır]
    S2_Soru -- Evet --> S2_Sozlesme[Müşteri ile görüşülerek Sözleşme imzalanır ve ön ödeme alınır]

    subgraph S2_Finans [Finansal Kayıt]
        S2_Sozlesme --> S2_Butce_Suret[BÜTÇE Suret]
        S2_Sozlesme --> S2_Soz_Suret[SÖZLEŞME Suret]
        S2_Sozlesme --> S2_On_Odeme[Ön Ödeme Bilgisi]
        S2_Butce_Suret & S2_Soz_Suret & S2_On_Odeme --- Muhasebe[MUHASEBE SORUMLUSU]
    end

    %% El Yazısı Notu
    S2_Finans -.-> Note1[<i>Not: Bütçe Hangisi?</i>]

    %% SAYFA 3: Teknik Hazırlık ve Kitapçık
    S2_Sozlesme --> S3_Kitapcik[Kesinleşmiş modeller, kumaş ve aksesuarlar ile ilgili tüm teknik bilgileri içeren kitapçık hazırlanır ve müşteriye gönderilir]
    S3_Kitapcik --- S3_Tasarim_Kitap[TASARIM KİTAPÇIĞI]
    S3_Tasarim_Kitap --- S3_Tasarim_Sor[TASARIM SORUMLUSU]

    S3_Kitapcik -- "c" --> S3_Maliyet_Form[Modellere İlişkin Maliyet Formları]
    S3_Maliyet_Form --> S3_Planlama_C[BÜTÇE Fiatsız / TASARIM KİTAPÇIĞI]
    S3_Planlama_C --> S3_Planlama_Sor[PLANLAMA SATINALMA SORUMLUSU]
    S3_Planlama_Sor --> S3_Is_Akisi_C[[PLANLAMA SATINALMA İŞ AKIŞI]]

    S3_Kitapcik -- "d" --> S3_Modelist_D[TASARIM MODELHANESİ MODELİSTİ]

    S3_Kitapcik -- "e" --> S3_Butce_E[BÜTÇE Fiatsız]
    S3_Butce_E --> S3_Kalıp_E[Gelen bilgiler doğrultusunda modellerin ana kalıpları çıkartılır]

    %% SAYFA 4: Ölçü Alma ve Üretim Hazırlığı
    S3_Kalıp_E --> S4_Olcu_Basla[Ölçü alma işlemleri başlatılır]
    
    S4_Olcu_Basla --> S4_Olcu1[ITKİB Ölçü Tablosuna göre personelin ölçüleri alınır]
    S4_Olcu_Basla --> S4_Olcu2[Müşteriden alınan veya Model Dikim Sorumlusu tarafından Müşteri işyerinde alınan ölçüler personelin ismine göre Bütçeye işlenir]
    S4_Olcu_Basla --> S4_Olcu3[DRESSBEST Size Setine göre personelin ölçüleri]

    S4_Olcu1 & S4_Olcu2 --> S4_Beden_List[Personel Beden Ölçüleri Listesi]
    S4_Olcu3 --- S4_Model_Dikim_Sor[MODEL DİKİM SORUMLUSU]

    S4_Beden_List -- "f" --> S4_Siparis_Form_F[SİPARİŞ FORMU]
    S4_Siparis_Form_F --> S4_Butce_F[BÜTÇE Beden Dağılımı - Fiatsız]
    S4_Butce_F --> S4_Planlama_Sor_F[PLANLAMA SATINALMA SORUMLUSU]
    S4_Planlama_Sor_F --> S4_Uretim_Akis[[SİPARİŞ ÜRETİM İŞ AKIŞI]]

    S4_Beden_List -- "g" --> S4_Siparis_Form_G[SİPARİŞ FORMU]
    S4_Siparis_Form_G --> S4_Modelist_G[MODELİST]
    S4_Modelist_G --> S4_Final[Siparişe ilişkin modellerin kalıpları çıkartılır ve serilendirmeleri yapılır. Pastal hazırlanır. İşaret ve çizim kalıpları çıkartılır. Dikiş Talimatı Hazırlanır.]

    %% Görseldeki Notlar
    subgraph El_Yazisi_Notlar [Görsel Üzerindeki Notlar]
        direction TB
        N1[Yeni dosya olacak?]
        N2[Fatma uygun]
        N3[Satış emirleri ve Üretim İş emirleri uygun]
    end

    %% Stil
    style S1_Onay fill:#fff,stroke:#000
    style S2_Soru fill:#fff,stroke:#000
    style S3_Is_Akisi_C fill:#fff9c4,stroke:#fbc02d
    style S4_Uretim_Akis fill:#fff9c4,stroke:#fbc02d
