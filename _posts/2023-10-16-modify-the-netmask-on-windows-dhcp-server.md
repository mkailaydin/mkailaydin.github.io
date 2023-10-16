---
title: VMware Esxi Root Password Reset
author: mkailaydin
date: 2023-10-16 13:30:00 +0800
categories: [Microsoft Windows, DHCP]
tags: [Microsoft Windows, DHCP Server]
pin: true



---

## Modify The Netmask on windows DHCP Server

- İlgili Scope Powershell ile dışarı export edilir.

```powershell
Export-DhcpServer -ComputerName <FQDN> -Leases -File C:\dhcp.xml -ScopeId x.x.x.x -Verbose
```

- Export edilen XML Dosyası notepad ya da diğer herhangi bir araç ile açılarak düzenlenmek istenilen alanlar düzenlenir ve dosya kaydedilir.

 ![Desktop View](/assets/img/2023-10-16-modify-the-netmask-on-windows-dhcp-server/export-file-review.png)

```xml
.....
<Scopes>
      <Scope>
        <ScopeId>10.0.9.0</ScopeId>
        <Name>Management</Name>
        <SubnetMask>255.255.255.0</SubnetMask>
        <StartRange>10.0.9.1</StartRange>
        <EndRange>10.0.9.254</EndRange>
        <LeaseDuration>8.00:00:00</LeaseDuration>
        <State>Active</State>
        <Type>Dhcp</Type>
.....
```

- Ardından Export edilen scope silinir ve scope yeniden import edilir.

 ![Desktop View](/assets/img/2023-10-16-modify-the-netmask-on-windows-dhcp-server/delete-scope.png)

```powershell
Import-DhcpServer -ComputerName <FQDN> -File C:\dhcp.xml -ScopeId x.x.x.x -Leases -Verbose -BackupPath C:\dhcp_backup
```

- Herhangi bir hata mesajı almadıysanız eğer DHCP Yönetim Konsolundan Scope’u kontrol edebilirsiniz.