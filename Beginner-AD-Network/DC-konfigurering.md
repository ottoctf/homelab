## Installation och konfigurering av Domain Controller

Startade upp min Windows Server 2022 VM och ändrade servernamnet till DC01. Detta är inte ett krav för att Active Directory ska fungera, men det är en bra standard eftersom namnet tydligt visar vilken roll servern har i miljön och gör administrationen enklare.

Efter namnbytet startade jag om servern för att ändringen skulle börja gälla.

Nästa steg var att konfigurera en statisk IP-adress. En Domain Controller bör ha en fast IP-adress eftersom Active Directory är beroende av DNS. Om IP-adressen skulle ändras kan klienter få problem med att hitta Domain Controllern och kommunicera med domänen.

Jag konfigurerade följande nätverksinställningar:

IP-adress: 192.168.10.10
Subnet mask: 255.255.255.0
Default gateway: Lämnades tom
DNS-server: 192.168.10.10

Jag valde 192.168.10.10 eftersom det är en privat IP-adress och passar bra i en separat labbmiljö. Det viktiga är inte exakt vilken privat IP-adress som används, utan att nätverket är korrekt planerat och att adressen inte krockar med andra enheter.

DNS pekades mot serverns egen IP-adress eftersom Domain Controllern även kommer att fungera som DNS-server. Active Directory använder DNS för att hitta tjänster och Domain Controllers i domänen. 

Jag lämnade default gateway tom eftersom detta är en isolerad labbmiljö. En gateway används när en dator behöver kommunicera med andra nätverk, exempelvis internet. Eftersom min server och användare kommer ligga i samma interna nätverk behöver de ingen gateway för att kommunicera med varandra.

Efter detta skapade jag ett separat internt virtuellt nätverk för labbmiljön. Syftet var att hålla miljön isolerad från mitt vanliga hemnätverk och skapa en mer kontrollerad testmiljö där jag själv kan styra IP-adresser och nätverkskommunikation.

Därefter installerade jag rollen Active Directory Domain Services (AD DS) och gjorde om servern till en Domain Controller.

När servern befordrades till Domain Controller skapades grunden för Active Directory-miljön. Servern fick en Active Directory-databas och rollen att hantera användare, datorer och autentisering i domänen.

Jag skapade sedan en ny forest med domännamnet:

lab.local

En forest är den högsta nivån i Active Directory-strukturen och innehåller domäner, användare, datorer och andra objekt. I denna labbmiljö består foresten av en enda domän, men i större miljöer kan en forest innehålla flera domäner.

Efter genomförd konfiguration var DC01 klar som Domain Controller.
