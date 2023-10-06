---
title: Evolution Version Upgrade to Standart Or Datacenter
author: mkailaydin
date: 2023-07-21 23:25:00 +0800
categories: [Microsoft Windows, OS]
tags: [Evolution version, Upgrade windows version]
pin: true
---

Aşağıdaki komut ile sistemin versiyon bilgisi görüntülenebilir.

```bash
Dism /online /Get-CurrentEdition
```

Versiyon Evalution olsa bile lisans anahtarına sahiptir ve temizleme işlemini gerçekleştirmek gerekir. Temizleme işlemini gerçekleştirebilmek için aşağıdaki komutlar kullanılabilir.

```bash
slmgr.vbs /upk #Lisans anahtarını silmek için kullanılır.**
```

```bash
slmgr.vbs /cpky #Lisans ile alakalı kayıt defteri kayıtlarını silmek için kullanılır**
```

Sonrasında ise artık Standart versiyona geçişi sağlayabiliriz. Geçiş işlemi için aşağıdaki komutlar bize yardımcı olacaktır.

```bash
DISM /Online /Set-Edition:ServerStandard /ProductKey:N69G4-B89J2-4G8F4-WWYCC-J464C /AcceptEula
```

Yukarıdaki komuttan sonra bize ait lisans anahtarı ile etkinleştirmemiz gerekecektir bu etkinleştirme işleminden önce yine önceki lisansı silmemiz gerektiğinden baştaki adımı tekrarlayacağız.

```bash
slmgr.vbs /upk
```

```bash
slmgr.vbs /cpky
```

Sonrasında ise orijinal lisans anahtarımızın girişini sağlıyoruz ve artık sistemimiz sorunsuz çalışmaya devam ediyor. Bu işlemleri yine aşağıdaki komutlar ile gerçekleştirebiliriz.

