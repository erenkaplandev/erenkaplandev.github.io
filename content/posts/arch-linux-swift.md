+++
author = "Eren Kaplan"
title = "Arch Linux’ta Swift ve Vapor"
date = "2022-09-22"
description = "Swift’in gücünü sunucu tarafında da görelim."
tags = [
    "swift",
    "linux",
    "server side",
]
categories = [
    "programming",
    "linux",
]
+++

![](https://cdn-images-1.medium.com/max/2400/1*1uTQIR_1grk5niRdg5jQ-w.jpeg)

Swift, Apple’ın geliştirdiği open-source, güçlü ve tasarımı güzel bir dil. Her iOS geliştiricinin Swift’i güzel özelliklerinden yararlanarak güzel uygulamalar ortaya çıkartıyor. Ama bugünkü blogumda iOS ile ilgili değil Swift'in Server-Side nimetlerinden konuşacağız.

## Peki nedir bu Vapor?

Swift ile yazılan en popüler (bu yazıyı yazdığım itibari ile Github’da 22.1k star almış) HTTP web framework’üdür. Vapor ile web sitelerinizi, API’larınızı ve bulut projeleri yazmayı sağlar. Hali hazırda Swift biliyorsanız başka bir dil öğrenmeden backend projeler geliştirebilirsiniz. Swift ile yazıldığı için performansı yüksektir, macOS ve Linux dağıtımları üzerinde çalışabilir.

## Kurulum

## macOS için kurulum

Bu blogu yazarken Linux için kurulumu hedefledim ancak asıl platformunu da es geçmemek gerekiyor. Bilgisayarınızda Xcode ve Brew kurulu olduğunu varsayarak anlatacağım.

Tek yapmamız gereken brew ile Vapor’u yüklemek.

    brew install vapor

Sorunsuz şekilde kurulup kurulmadığını kontrol etmek için de — help parametresi ile çalışıp çalışmadığını kontrol edebilirsiniz.

    vapor --help

## Arch Linux için kurulum

Linux üstünde geliştirmek için adımlar şöyle;

* Swift kodu yazmak için metin editörü. Ben Visual Studio Code kullanmayı tercih ediyorum.

* Linux dağıtımınıza uygun Swift paketi ve

* Swift kurulduktan sonra Vapor’un derlenmesi

ilk başta sevdiğiniz metin editörünü hazır tutalım. Ben bilgisayarımda Arch Linux kullandığım için AUR’dan Visual Studio Code’u derledim

    yay -S visual-studio-code-bin #Stabil olan
    yay -S visual-studio-code-insider-bin #Bu da Insider sürümü(kararsız)

Metin editörümüzü kurduktan sonra şimdi sıra Swift’i yüklemeye geldi. Swift’in sitesinde Ubuntu, CentOS 7 ve Amazon Linux 2 için kurulumlar mevcut. Kullanmış olduğunuz dağıtımın deposunda arama yaparak bulabilirsiniz. Arch Linux kurulumu için isterseniz AUR’dan Fedora için paketlenmiş binary olarak kurabilirsiniz([swift-bin](https://aur.archlinux.org/packages/swift-bin/)), isterseniz de kendiniz baştan derleyebilirsiniz([swift-language](https://aur.archlinux.org/packages/swift-language/)). Ben uzun sürmesin diye binary dosyasını yükledim. Şu şekilde yükleyebilirsiniz;

[Arch Linux Swift Lang](https://asciinema.org/a/WYONSKo0P1nSVqUpURYkzG1ka)

Yükleme işlemi bittikten sonra çalışıp çalışmadığını — version parametresi ile kontrol edebilirsiniz.

    swift --version

Swift kurulumunu da başarıyla tamamladıysak şimdi Vapor Toolbox kurmaya geçelim. Vapor Toolbox kurmak için git sayfasından indirip bilgisayarımızda derlememiz gerekiyor.

    git clone <https://github.com/vapor/toolbox.git>
    cd toolbox
    make install

Mac kurulumunda yaptığımız gibi sorunsuz şekilde kurulup kurulmadığını teyit etmek için — help parametresi çalıştıralım.

    vapor --help

Komutu çalıştırdıktan sonra mevcut komutların listesini görmeniz gerekiyor. Eğer gördüyseniz tebrikler, adımları uygulayarak başarılı bir şekilde Vapor Framework’ü kurdunuz 🥳

## Kurulum sonrası

Kurulumumuzu tamamladığımıza göre yeni bir proje oluşturalım. Projeyi oluşturmak için

    vapor new <proje ismi>

    #Örnek
    vapor new merhaba
> *-n parametresi eklerseniz size soru sormadan bütün sorulara hayır cevabı vererek saf bir şablon ile başlarsınız. Ben de öyle yaptım.*

![](https://cdn-images-1.medium.com/max/2096/1*mDXvZTqC8xCtLLypJe2ptw.png)

Şimdi de projemizin içine gidelim ve projemizi metin editörümüz ile açalım.

    cd merhaba
    code . #vscode kullandığım için bu komutu yazdım

    #Eğer Mac ortamındaysanız 
    open Package.swift #Komutuyla xcode ile açabilirsiniz projenizi

![](https://cdn-images-1.medium.com/max/3840/1*SRjGxMQeuipUE3Y-oyY0LA.png)

Eğer Visual Studio Code kullanacaksanız [Swift](https://marketplace.visualstudio.com/items?itemName=sswg.swift-lang) eklentisini kurmanızı şiddetle öneririm. Kod tamamlama, hata açıklamaları, hata ayıklama özelliklerini destekliyor. Visual Studio Code kullanmayacaksanız da diğer IDE/Editörler için [kurulum rehberi](https://github.com/swift-server/guides/blob/main/docs/setup-and-ide-alternatives.md) bulunmakta. Şu anlık rehberde Atom, CLion, Emacs ve Vim kurulumları için rehberler var.

Projeyi oluşturup metin editörümüzle açtığımıza göre şimdi de projemizi çalıştıralım.

    swift run

Bu komut projemizin derlenmesi ve çalışması için. İlk çalışmada birazcık uzun sürebilir.

    [...]
    Creating working copy for <https://github.com/swift-server/swift-backtrace.git>
    Working copy of <https://github.com/swift-server/swift-backtrace.git> resolved at 1.3.3
    Building for debugging...
    [1852/1852] Linking Run
    Build complete! (61.74s)
    [ NOTICE ] Server starting on <http://127.0.0.1:8080>

Derleme bittikten sonra tarayıcınızdan [http://127.0.0.1:8080/hello](http://127.0.0.1:8080/hello) adresine gidip yine çalışıp çalışmadığını teyit edebilirsiniz.

Bugünkü yazımda Arch Linux’ta Swift ve Vapor kurulumunu anlattım. Swift aşırı sempati duyduğum, yazarken eğlendiğim bir dil. Kurulumda sıkıntı yaşarsanız ~~Discord sunucuma~~ gelip takıldığınız yerler hakkında tartışabiliriz. Ayrıca yeni yazdığım yazılardan haberdar olmak için de [Twitter’dan](https://twitter.com/hellstabber) takip edebilirsiniz. またね!

<img src="insan-yazimi.png" alt="https://notbyai.fyi/" width="300" height="200">