---
title: Veeam Backup 12 Upgrade and Configure to Hardened Repository
author: mkailaydin
date: 2023-03-15 14:50:00 +0800
categories: [Veeam Backup]
tags: [Veeam Backup 12, Immutable Repository,]
pin: true


---
Merhaba, Veeam Backup & Replication 11 ‘den 12’ye geçerken 'Hardened Repository' kullanıyorsanız ve 'Single use credential' ile yapılandırmadıysanız upgrade ederken hata alacaksınız ve bu hatayı gidermek için backup dosyalarındaki 'Immutable' flagını kaldırıp owner’ını değiştirmeniz ve ardından ilgili dosyalara yeniden 'Immutable' flagını koymanız gerekecektir ya da Bütün Job’lar için Full Backup çalıştırmanız gerekecektir. Bu durumun önüne geçebilmemiz için Veeam bir script yayınlamış. Bu scripti kullanarak geçişi daha kolay hale getirebiliriz.

Aslında bu script 'Single use credential' ile yapılandırılmamış bir 'Linux Hardened Repository' i 'Single use credential' ile yeniden yapılandırırken kullanılan bir script ancak Veeam Backup & Replication 12’de 'Linux Hardened Repository' için 'Sigle use credential' zorunlu hale geldi, o sebeple bu makaleden yararlanarak işleri kolay hale getirmek en mantıklı seçenek oluyor.

```bash
#!/bin/bash
 
auxiliaryfile="/tmp/veeamstoragefilenames_"$(date '+%Y-%m-%d-%H-%M')
 
find $1 -name "*.vbk" -o -name "*.vib" -type f > $auxiliaryfile
while read -r line;
do  
    is_immutable=false
    STR=$(eval lsattr -Rl ${line// /\\ })
    SUB=' Immutable'
    SUB2=',Immutable'
    if [[ "$STR" == *"$SUB"* ]]; then
        is_immutable=true
    elif [[ "$STR" == *"$SUB2"* ]]; then
        is_immutable=true
    fi
    if [[ $is_immutable == 'true' ]]; then
        eval chattr -i "${line// /\\ }" ;
    fi    
    eval chown $2:$3 "${line// /\\ }" ;
    if [[ $is_immutable == 'true' ]]; then
        eval chattr +i "${line// /\\ }" ;
    fi
done < $auxiliaryfile
 
find $1 -name "*.vbm" -type f > $auxiliaryfile
while read -r line;
do  
    eval chown $2:$3 "${line// /\\ }" ;
done < $auxiliaryfile
 
chown -R $2:$3 $1 2>/dev/null
 
rm -rf $auxiliaryfile
```

Peki tamam scripti gördük ama nasıl çalıştıracağız derseniz aşağıdaki adımları takip edebilirsiniz;

**NOT: Aşağıdaki işlemlerin bazıları için root yetkisine sahip olunması gerekebilir. Aşağıdaki komutlar doğrudan root user ile çalıştırıldığı için ‘sudo’ komutu kullanılmadan yazılmıştır.**

```bash
# vi Editörü parametre olarak isim vererek açıyoruz ve içine scriptimizi yapıştırıyoruz. Siz nano ya da farklı editörleri de kullanabilirsiniz.
vi change_backup_owner.sh

# Aşağıdaki komutla ilgili dosyamızı 'Executable' hale getiriyoruz. Yani çalıştırılabilir bir komut dosyası olduğunu belirtmiş oluyoruz.
chmod +x change_backup_owner.sh

# Ardından .sh dosyamızı çağırıyoruz ve gerekli parametereleri veriyoruz. 
# Örnekteki parametreleri kendi parametreleriniz ile değiştirmelisiniz. Sytax'i ayrıca belirtiyorum.
# ./change_backup_owner.sh /immrepo/backups/ vuser vuser
./change_backup_owner.sh <RepositoryPath> <User> <Group>
```
