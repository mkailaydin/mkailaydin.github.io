---
title: Create Windows Firewall Rule with Powershell for Fortigate FSSO Collector Agent
author: mkailaydin
date: 2023-10-27 11:50:00 +0800
categories: [Microsoft Windows, Firewall]
tags: [Microsoft Windows, Windows Firewall, Fortigate]
pin: true



---
 Aşağıdaki Script ile ilgili kurallar oluşturulabilir.

>Script'i daha rahat kopyala yapıştır yapabilmek adına Powershell ISE kullanabilirsiniz

>Aynı Zamanda Powershell Prompt/Powershell ISE Yönetici olarak çalıştırmayı unutmayınız.
>

```powershell
# Inbound Port
$inboundPorts = @(
    "8002 - UDP - Fortigate DC Agent keepalive and push logon info to Collector Agent",
    "8001 - TCP - Fortigate FortiGate to FSSO Collector Agent connection (SSL)",
    "8000 - TCP - Fortigate FortiGate to FSSO Collector Agent connection",
    "8000 - TCP - Fortigate NTLM"
)

# Outbound Port
$outboundPorts = @(
    "135 - TCP - Fortigate Workstation check, polling mode (fallback method)",
    "139 - TCP - Fortigate Required Port",
    "137 - UDP - Fortigate Required Port",
    "445 - TCP - Fortigate Remote access to logon events, Workstation check (remote registry)",
    "389 - TCP - Fortigate Group lookup using LDAP",
    "636 - TCP - Fortigate Group lookup using LDAPS",
    "3268 - TCP - Fortigate Group lookup using LDAP with global catalog",
    "3269 - TCP - Fortigate Group lookup using LDAPS with global catalog",
    "53 - UDP - Fortigate DNS for resolving hostnames of the logon events"
)

# Open Inbound Ports
Write-Host "Opened Inbound Ports:"
foreach ($portDesc in $inboundPorts) {
    $portInfo = $portDesc -split " - "
    $port = $portInfo[0]
    $protocol = $portInfo[1]
    $description = $portInfo[2]
    Write-Host "Opening: $port $protocol - $description"

    New-NetFirewallRule -DisplayName "$description (Inbound)" -Direction Inbound -LocalPort $port -Protocol $protocol -Action Allow -Enabled True
}

# Open Outbound Ports
Write-Host "Opened Outbound Ports:"
foreach ($portDesc in $outboundPorts) {
    $portInfo = $portDesc -split " - "
    $port = $portInfo[0]
    $protocol = $portInfo[1]
    $description = $portInfo[2]
    Write-Host "Opening: $port $protocol - $description"

    New-NetFirewallRule -DisplayName "$description (Outbound)" -Direction Outbound -LocalPort $port -Protocol $protocol -Action Allow -Enabled True
    
}

```
