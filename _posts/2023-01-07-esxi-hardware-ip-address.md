---
title: What is Host IMM IP Address
author: mkailaydin
date: 2023-10-27 11:50:00 +0800
categories: [Vmware, Esxi]
tags: [Vmware,ESXi,Virtualization]
pin: true



---

Merhaba, Bu yazı çok kısa olacak ancak bazı durumlarda bu kısacık komut hayat kurtarabiliyor.

Aşağıdaki komut yardımı ile esxi kurulumu yapılmış bir hostun, imm/idrac/xclarity gibi gömülü yönetim arayüzlerine ulaşabileceğiniz, ip adresini öğrenebilirsiniz, tabi yapılandırıldıysa :)

```bash
localcli hardware ipmi bmc get

```
