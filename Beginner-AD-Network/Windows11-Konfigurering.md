# Installation och konfigurering av Windows 11-klient

## Installation

Jag installerade en Windows 11 Pro VM som ska användas som klientdator i mitt Active Directory-labb.

Installationen genomfördes som en vanlig Windows-installation, men VM:n konfigurerades med följande inställningar för att fungera tillsammans med Active Directory:

- Operativsystem: Windows 11 Pro x64
- Virtualiseringsplattform: VirtualBox 7.2.12
- Firmware: UEFI
- TPM: 2.0
- Secure Boot: Aktiverat

Jag satte en statisk IP Adress på denna maskin till `192.168.10.20`. Domain controllern har IP Adressen `192.168.10.10`.
