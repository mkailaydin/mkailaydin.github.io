---
title: Exchange Server - Delete Mailbox Content
author: mkailaydin
date: 2023-09-09 20:55:00 +0800
categories: [Microsoft Windows, Exchange]
tags: [Microsoft Exchange Server]
pin: true
img_path: '/posts/20180809'
---

## Delete Mailbox Content

Mailbox’ın içeriğinin tamamen temizlenmesi için öncelikle işlemi yapacak kullanıcının aşağıdaki rollere sahip olması gerekir.  Roller istenirse Powershell scripti istenirse arayüz üzerinden kullanıcıya tanımlanabilir. Bkz..

```powershell
New-ManagementRoleAssignment -Role "Mailbox Search" -User "mikail.aydin"
New-ManagementRoleAssignment -Role "Mailbox Import Export" -User "mikail.aydin"
```

Ardından ilgili mailbox için bir arama sorgusu oluşturulur ve hedef kullanıcı ve kullanıcının klasörü belirtilir, son olarak -DeleteContent parametresi verilir ve ilgili mailboxın içindeki bütün maillerin temizlenmesi sağlanır. Bkz..

***Dikkat : Mailbox’ın içeriği temizlenmeden önce ilgili yedeklerin alındığından emin olun. Yedekler herhangi bir felaket yaşamamak için hem kullanıcı hem de sunucunun tamamı için alınmalıdır.*** 

```powershell
Search-Mailbox Administrator -SearchQuery '(received<01/01/2022)' -TargetMailbox Administrator -TargetFolder Administrator -DeleteContent
```