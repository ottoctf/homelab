# Installation och konfigurering av Windows 11-klient

## Installation

Jag installerade en Windows 11 Pro VM som ska användas som klientdator i mitt Active Directory-labb.

Installationen genomfördes som en vanlig Windows-installation, men VM:n konfigurerades med följande inställningar för att fungera tillsammans med Active Directory:

- Operativsystem: Windows 11 Pro x64
- Virtualiseringsplattform: VirtualBox 7.2.12
- Firmware: UEFI
- TPM: 2.0
- Secure Boot: Aktiverat

Nästa steg var att konfigurera en statisk IP-adress. Det viktiga här är att IP Adressen har samma nät som Domain controllern samt att DNS pekar mot
Domain Controllerns IP Adress och inte exempelvis Google 8.8.8.8.

Jag konfigurerade följande nätverksinställningar:

IP-adress: 192.168.10.20 Subnet mask: 255.255.255.0 Default gateway: Lämnades tom DNS-server: 192.168.10.10

## Troubleshooting

### DNS
`nslookup lab.local` Fungerade men `nslookup dc01.lab.local` gav Request timed out. I Powershell testade jag Get-Service DNS. Fick svaret `Cannot find any service with service name 'DNS'`. Det betyder troligtvis att DNS Server rollen inte är installerad på domain controllern.

På Domain Controllern så körde jag powershell. Jag använde kommandot `Get-WindowsFeature AD-Domain-Services,DNS` för att se ifall DNS var installerat. Vilket det var för mig.

Jag körde sen nltest /dsgetdc:lab.local vilket gav rätt resultat så DNS problemet var inget kritiskt och troligtvis bara DNS Serverns reverse lookup/PTR saknas eller tar lång tid.
