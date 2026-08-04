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

## Anslutning till domänen

För att ansluta klientdatorn till domänen öppnade jag System Properties med Win + R och kommandot sysdm.cpl. Under fliken Datornamn valde jag Ändra, markerade Domän och angav domännamnet lab.local.

När Windows begärde autentisering använde jag ett administratörskonto från Domain Controllern. Detta krävs eftersom endast användare med rätt behörighet får ansluta datorer till domänen. Efter en omstart var klienten medlem i domänen.

För att verifiera att anslutningen fungerade loggade jag in på klienten med domänens Administrator-konto. Eftersom kontot finns i Active Directory kunde det användas på klientdatorn efter att den anslutits till domänen.


Detta nedanför till ovanför troubleshoot ska vara på en egen .md fil sedan som ska heta AD Konfigurering.

Därefter skapade jag två egna Organizational Units (OU):

OU-Computers – där jag flyttade datorobjektet AD-User från den inbyggda Computers-containern.
OU-Users – där jag skapade två användarkonton:
bob – ett vanligt användarkonto.
bob.admin – ett administratörskonto.

För administratörskontot bob.admin lade jag till gruppen Domain Admins under Member Of. Detta gav kontot administrativa rättigheter i domänen, medan Bob behöll vanliga användarbehörigheter enligt principen om least privilege. Jag verifierade sedan att båda kontona kunde logga in på klientdatorn.

## Troubleshooting

### DNS

Vid felsökning började jag med att kontrollera namnuppslagning.

nslookup lab.local

Detta fungerade och visade att klienten kunde hitta domänen via DNS.

När jag däremot körde:

nslookup dc01.lab.local

fick jag svaret:

Request timed out.

Eftersom Active Directory är beroende av DNS ville jag säkerställa att DNS-tjänsten faktiskt var installerad på Domain Controllern.

Jag testade först på klienten med:

Get-Service DNS

vilket gav:

Cannot find any service with service name 'DNS'

Detta är dock förväntat på en vanlig klient eftersom DNS Server-tjänsten endast finns installerad på servrar med DNS Server-rollen.

På Domain Controllern verifierade jag därför installationen med:

Get-WindowsFeature AD-Domain-Services,DNS

Resultatet visade att både Active Directory Domain Services och DNS Server var installerade.

Som ett sista test körde jag:

nltest /dsgetdc:lab.local

Kommandot lyckades hitta Domain Controllern, vilket bekräftade att klienten kunde kommunicera med domänen och att DNS fungerade tillräckligt bra för Active Directory. Eftersom både domänanslutningen och autentiseringen fungerade bedömde jag att timeouten från nslookup dc01.lab.local inte var ett kritiskt fel, utan sannolikt ett mer specifikt problem med namnuppslagningen snarare än ett generellt DNS-fel.

