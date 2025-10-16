BAŞLA  // Kullanıcı girişi aşaması
    KULLANICI_GİRİŞ_BİLGİLERİNİ_AL()
    EĞER BİLGİLER_DOĞRU_İSE
        OTURUMU_BAŞLAT()
        KULLANICI_ID ← AKTİF_KULLANICI()
    DEĞİLSE
        "Giriş başarısız. Tekrar deneyiniz." YAZ
        SİSTEMİ_SONLANDIR()
    SON
BİTİR


BAŞLA  // Ürün ekleme aşaması
    SEÇİLEN_ÜRÜN ← KULLANICIDAN_AL()
    MİKTAR ← KULLANICIDAN_AL()
    EĞER ÜRÜN_MEVCUT_İSE
        EĞER ÜRÜN_SEPETTE_VARSA
            SEPETTEKİ_MİKTARI_ARTTIR(MİKTAR)
        DEĞİLSE
            ÜRÜNÜ_SEPETE_EKLE(SEÇİLEN_ÜRÜN, MİKTAR)
        SON
    DEĞİLSE
        "Ürün stokta yok." YAZ
    SON
BİTİR


BAŞLA  // Stok kontrolü aşaması
    DÖNGÜ HER_ÜRÜN İÇİN SEPETTE
        STOK ← STOK_DURUMU(ÜRÜN)
        EĞER STOK < MİKTAR
            "Yetersiz stok: " + ÜRÜN_ADI YAZ
            ÜRÜNÜ_SEPETTEN_KALDIR(ÜRÜN)
        SON
    SON
BİTİR


BAŞLA  // İndirim kodu uygulama
    EĞER KULLANICI_INDİRİM_KODU_GİRDİ_Mİ
        KOD ← AL()
        EĞER KOD_GEÇERLİ_Mİ(KOD)
            SEPET_TOPLAMINI_GÜNCELLE(İNDİRİM_UYGULA(KOD))
            "İndirim başarıyla uygulandı." YAZ
        DEĞİLSE
            "Kod geçersiz veya süresi dolmuş." YAZ
        SON
    SON
BİTİR


BAŞLA  // Kargo hesaplama aşaması
    ADRES ← KULLANICIDAN_ADRES_AL()
    KARGO_TÜRÜ ← KULLANICIDAN_KARGO_SEÇ()
    KARGO_ÜCRETİ ← KARGO_HESAPLA(ADRES, KARGO_TÜRÜ)
    SEPET_TOPLAMINA_EKLE(KARGO_ÜCRETİ)
    "Toplam tutar güncellendi." YAZ
BİTİR


BAŞLA  // Ödeme aşaması
    "Ödemeye geçiliyor..." YAZ
    KART_BİLGİLERİ ← KULLANICIDAN_AL()
    EĞER ÖDEME_ONAYLANIRSA(KART_BİLGİLERİ)
        SİPARİŞ_OLUŞTUR()
        STOKTAN_DÜŞ()
        SEPETİ_TEMİZLE()
        "Ödeme başarılı! Siparişiniz oluşturuldu." YAZ
    DEĞİLSE
        "Ödeme başarısız! Lütfen tekrar deneyiniz." YAZ
        TEKRAR_DENEME_SEÇENEĞİ_VER()
    SON
BİTİR


BAŞLA  // Sipariş tamamlama ve bildirim
    EĞER SİPARİŞ_OLUŞTURULDU_MU
        E_POSTA_GÖNDER()
        SMS_GÖNDER()
        KARGO_SÜRECİNİ_BAŞLAT()
        "Sipariş onaylandı, takip numaranız gönderildi." YAZ
    SON
BİTİR


BAŞLA  // Sistem sonu
    "Teşekkür ederiz. E-ticaret sisteminden çıkılıyor..." YAZ
    OTURUMU_KAPAT()
BİTİR
