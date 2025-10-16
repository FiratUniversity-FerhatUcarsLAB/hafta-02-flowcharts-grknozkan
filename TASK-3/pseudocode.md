BAŞLA

// Kimlik doğrulama aşaması
GİRİŞ: T.C. Kimlik Numarası, Şifre
EĞER kimlik bilgileri doğrulanırsa
    DEVAM ET
DEĞİLSE
    EKRANA "Kimlik doğrulama başarısız!" yaz
    BİTİR
EĞER-İSE SONU

// Poliklinik seçimi
POLİKLİNİKLERİ GÖSTER
GİRİŞ: Seçilen_Poliklinik

// Doktor listesi görüntüleme
SEÇİLEN_POLİKLİNİĞE_AİT_DOKTORLARI_GÖSTER
GİRİŞ: Seçilen_Doktor

// Uygun saatleri gösterme
SEÇİLEN_DOKTORUN_UYGUN_SAATLERİNİ_GÖSTER
GİRİŞ: Seçilen_Saat

// Randevu onaylama
EĞER Seçilen_Saat MÜSAİT ise
    Randevuyu_Kaydet(Seçilen_Poliklinik, Seçilen_Doktor, Seçilen_Saat)
    EKRANA "Randevunuz başarıyla oluşturuldu." yaz
DEĞİLSE
    EKRANA "Seçilen saat dolu! Lütfen başka bir saat seçin." yaz
EĞER-İSE SONU

// SMS gönderme
EĞER Randevu oluşturulduysa
    SMS_GÖNDER("Randevunuz onaylandı: " + Seçilen_Poliklinik + " - " + Seçilen_Doktor + " - " + Seçilen_Saat)
    EKRANA "Onay SMS’i gönderildi." yaz
EĞER-İSE SONU

BİTİR
