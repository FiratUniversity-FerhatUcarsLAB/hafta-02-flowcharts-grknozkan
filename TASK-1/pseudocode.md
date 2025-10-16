BAŞLA

    PIN ← 1234
    bakiye ← 5000
    günlük_limit ← 2000
    kalan_hak ← 3

    DÖNGÜ (kalan_hak > 0)
        YAZ "Lütfen PIN'inizi giriniz: "
        OKU girilen_PIN

        EĞER girilen_PIN = PIN İSE
            YAZ "PIN doğrulandı."
            ÇIKIŞ DÖNGÜDEN
        DEĞİLSE
            kalan_hak ← kalan_hak - 1
            YAZ "Hatalı PIN! Kalan deneme hakkınız: ", kalan_hak
        BİTİR EĞER
    BİTİR DÖNGÜ

    EĞER kalan_hak = 0 İSE
        YAZ "3 kez hatalı giriş yaptınız. Kart bloke oldu."
        BİTİR
    BİTİR EĞER

    TEKRAR ← "E"

    DÖNGÜ (TEKRAR = "E")
        YAZ "Çekmek istediğiniz tutarı giriniz (20 TL katı olmalıdır): "
        OKU tutar

        EĞER tutar > bakiye İSE
            YAZ "Yetersiz bakiye!"
        DEĞİLSE EĞER tutar > günlük_limit İSE
            YAZ "Günlük limit aşıldı! Maksimum ", günlük_limit, " TL çekebilirsiniz."
        DEĞİLSE EĞER tutar MOD 20 ≠ 0 İSE
            YAZ "Lütfen 20 TL'nin katı bir tutar giriniz!"
        DEĞİLSE
            bakiye ← bakiye - tutar
            günlük_limit ← günlük_limit - tutar
            YAZ "İşlem başarılı. Çekilen tutar: ", tutar, " TL"
            YAZ "Kalan bakiye: ", bakiye, " TL"
            YAZ "Kalan günlük limit: ", günlük_limit, " TL"
        BİTİR EĞER

        YAZ "Başka işlem yapmak ister misiniz? (E/H)"
        OKU TEKRAR
    BİTİR DÖNGÜ

    YAZ "İyi günler dileriz!"
BİTİR
