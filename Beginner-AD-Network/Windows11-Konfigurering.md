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
