---
title: VMware Esxi Root Password Reset
author: mkailaydin
date: 2023-09-21 23:25:00 +0800
categories: [Vmware, Esxi]
tags: [Vmware,ESXi,Virtualization]
pin: true
---

## ESXi Root Password Reset

- vCenter WebClient'e giriş yapın.
- Envanteri açın ve şifresini sıfırlamak istediğiniz host üzerinde Sağ tıklayın, ardından ‘Host Profiles’ altından ‘Extract Host Profile…’ seçeneğini seçin.
    
    ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/esx-extract-host-profile.png)
    
- Açılan pencerede yeni Host Profile için isim girin.
    
    ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/esx-extract-host-profile-page.png)
    
- ‘Policies and Profiles’ altınadaki ‘Host Profiles’ sekmesine gelin, ardından Extract işlemi ile oluşturduğunuz profil üzerinde sağ tıklayın ve ‘Edit Host Profile’ seçeneğini seçin.
    
    ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/esx-policy-page.png)
    
- Açılan pencerede arama filtresini kullanarak ‘root’ kelimesini aratın, ‘root’u’ işaretleyin, ardından ‘Password’ alanındaki ‘Fixed password configuration’ seçeneğini seçin.
    - Yeni parolanızı girin,
    - Ayarlamak/değiştirmek **istemediğiniz** diğer ayaların işaretlenmediğinden emin olun. Save butonunu seçerek pencereden çıkın.
        
        ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/esx-edit-host-profile.png)
        
    - Arama filtresini sildikten sonra bütün kırılımları kapatırsanız böyle bir pencere göreceksiniz.
        
        ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/esx-edit-host-profile-1.png)
        
- Envanter sekmesini açın ve yeni oluşturduğunu host profili atayın.
    
    ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/attach-esx-host-profile.png)
    
- ‘Attach Host Profile…’ seçeneğini seçtikten sonra aşağıdaki pencere ile karşılaşacaksınız. Burada oluşturduğunuz profili seçip ‘OK’ demeniz yeterli olacaktır.
    
    ![Desktop View](/assets/img/2023-09-18-esxi-root-password-reset/select-esx-attach-host-profilepng.png)
    
- Bu aşamadan sonra, makine şifresi başarıyla güncellenmiş olmalıdır.

Herkese musmutlu günler dilerim.
