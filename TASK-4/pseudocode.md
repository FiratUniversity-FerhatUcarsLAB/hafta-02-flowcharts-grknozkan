BASLA

  // Giriş
  YAZ "Kullanıcı adı giriniz:"
  OKU kullaniciAdi
  YAZ "Şifre giriniz:"
  OKU sifre

  EĞER (girisDogruMu(kullaniciAdi, sifre)) İSE
      YAZ "Giriş başarılı. Ders listesi görüntüleniyor..."
      
      // Ders listesi
      dersListesi = tumDersleriGetir()
      YAZ dersListesi

      secilenDersler = BOS_LİSTE
      toplamKredi = 0

      // Ders seçimi
      DÖNGÜ (her ders için dersListesi)
          YAZ "Bu dersi almak ister misiniz? (EVET/HAYIR)"
          OKU secim
          EĞER (secim == "EVET") İSE
              secilenDersler.EKLE(ders)
      DÖNGÜ BİTİR

      // Kontroller
      her ders için ders in secilenDersler DÖNGÜ
          EĞER (kontenjanDolduMu(ders)) İSE
              YAZ ders.ad + " dersinin kontenjanı dolu!"
              secilenDersler.SIL(ders)
          İSE
              EĞER (onKosulTamamlandiMi(ders, kullaniciAdi)) İSE
                  EĞER (zamanCakisiyorMu(ders, secilenDersler)) İSE
                      YAZ ders.ad + " dersinde zaman çakışması var!"
                      secilenDersler.SIL(ders)
                  İSE
                      EĞER ((toplamKredi + ders.kredi) > krediLimiti) İSE
                          YAZ "Kredi limiti aşılıyor!"
                          secilenDersler.SIL(ders)
                      İSE
                          EĞER (danismanOnayiVarMi(ders, kullaniciAdi)) İSE
                              toplamKredi = toplamKredi + ders.kredi
                              YAZ ders.ad + " dersi başarıyla eklendi."
                          İSE
                              YAZ "Danışman onayı gereklidir!"
                              secilenDersler.SIL(ders)
  DÖNGÜ BİTİR

      // Onay
      EĞER (secilenDersler.BOS_MU()) İSE
          YAZ "Hiç ders seçilmedi veya tüm dersler reddedildi."
      İSE
          YAZ "Ders kaydınız onaylandı:"
          YAZ secilenDersler

  İSE
      YAZ "Giriş hatalı!"

BİTİR
