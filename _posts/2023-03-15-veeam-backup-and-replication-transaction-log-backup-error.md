---
title: Veeam Backup Sql Transaction Log Backup - Failed to prepare guest for SQL transation log backup
author: mkailaydin
date: 2023-11-13 15:15:00 +0800
categories: [Veeam Backup & Replication]
tags: [Veeam Backup 12, Veeam Backup SQL Transaction Log, Guest Processing,]
pin: true


---
Veeam Backup ile SQL Transaction Log Backup aldığınız bir job vardı, ve bir şekilde o job artık kullanmıyorsunuz ancak yeni oluşturduğunuz job ile transaction log backup almak istiyorsunuz ve fakat şöyle bir hatayla karşılaşıyorsunuz;

> Failed to prepare guest for SQL transaction log backup Details: <"Old Job"> is responsible for SQL transaction logs backup

Bu hatanın sebebi Veeam Backup & Replication'ın tasarımından gelen bir durum, yani hata değil, tercih. Varsayılan olarak gelen 7 günlük bir döngüyü beklemeniz gerekiyor. Bu durumdan aslında 7 gün sonra kurtulacaksınız ancak iş backup olunca 1 saatin bile önemi olabiliyor. O sebeple regedit üzerinde bir değeri değiştirmemiz gerekiyor, aşağıdaki şekilde çözüme ulaşabilirsiniz.

> - Key Location          : HKLM\SOFTWARE\Veeam\Veeam Backup and Replication\
> - Value Name            : SqlBackupLogsAgeDaysToSkipLogBackup
> - Value Type            : DWORD (32-bit) Value
> - Value Data Default    : 7

SqlBackupLogsAgeDaysToSkipLogBackup DWORD girdisinin varsayılan 7 değerini 0 yapıyoruz.

Hadi elinize sağlık. Backup Job artık çalışıyor.

Original Makaleye aşağıdaki linkten ulaşabilirsiniz.

<https://www.veeam.com/kb2029>
