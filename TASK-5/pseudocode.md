BASLA

// Sistem Başlatma
Başlat_Sensörler()
Başlat_Alarm_Sistemi()
Başlat_Bildirim_Sistemi()

// Sonsuz ana döngü
DÖNGÜ
    // 1. Sensörleri oku
    hareket_var_mı = Hareket_Sensörü_Oku()
    kapı_pencere_var_mı = Kapı_Pencere_Sensörü_Oku()
    duman_var_mı = Duman_Sensörü_Oku()
    
    // 2. Tehdit algılama
    EĞER (hareket_var_mı VEYA kapı_pencere_var_mı) VE duman_var_mı = HAYIR
        tehdit = "Hırsızlık"
    İŞE_YARARLI_DEĞİLSE EĞER duman_var_mı
        tehdit = "Yangın"
    DEĞİLSE
        tehdit = "Yok"
    
    // 3. Alarm ve bildirim
    EĞER tehdit ≠ "Yok"
        Alarmı_Aç(tehdit)
        Bildirim_Gönder(tehdit)
    
    // 4. Döngü kısa gecikme ile devam eder
    Bekle(1 saniye)

DÖNGÜ_BİTİR

BİTİR
