---
title: Exchange Server - Yeni Sertifikanın Uygulanması
author: mkailaydin
date: 2023-09-09 20:55:00 +0800
categories: [Microsoft Windows, Exchange]
tags: [Microsoft Exchange Server]
pin: true
img_path: '/posts/20180809'
---

## Exchange Server - Yeni Sertifikanın Uygulanması

- Alınan SSL Sertifikasının .pfx uzantılı hali bir paylaşım klasöründe erişilebilir bir konuma kopyalanır.
- Exchange Powershell açılır ve aşağıdaki komutta ilgili alanlar değiştirilerek komut çalıştırılır.

```powershell
Import-ExchangeCertificate -Server <Exchange Server Name> -FileData ([System.IO.File]::ReadAllBytes(<SSL Sertificate Path>)) -PrivateKeyExportable:$true -Password (ConvertTo-SecureString -String <pfx file password> -AsPlainText -Force)
```

- Aşağıda alanları değiştirilmiş bir örneği görebilirsiniz.

```powershell
Import-ExchangeCertificate -Server "EXCH" -FileData ([System.IO.File]::ReadAllBytes('\\exch\Share\ExchangeCert.pfx')) -PrivateKeyExportable:$true -Password (ConvertTo-SecureString -String 'Passw0rd01' -AsPlainText -Force)
```

- Sertfika yükleme işlemi başarıyla gerçekleştirildikten sonra ekrana sertifikanın özellikleri yazılacaktır. Burada bizim için önemli olan Thumbprint (parmakizi) alanıdır. Çünkü sertifikayı kullanıma alırken komut içerisinde bu thumbprint alanını kullanacağız.
- Sertifikayı servislerde kullanmak için aşağıdaki komutu kullanabiliriz.

```powershell
Enable-ExchangeCertificate -Server "EXCH" -Thumbprint A09015D0724FB91DB5CA00D46A4324E3C35001F5 -Services SMTP,IMAP,POP,IIS
```

- Aşağıdaki görselden nasıl bir powershell penceresi ile karşılaşmanız gerektiğini görebilirsiniz.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f96f707b-cc92-4630-bfa1-4ebd421af780/Untitled.png)