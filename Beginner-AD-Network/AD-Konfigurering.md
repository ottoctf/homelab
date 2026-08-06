# Konfigurering av Active Directory miljön.(Work in progress)

Jag började med att skapa två egna Organizational Units (OU):

* OU-Computers – där jag flyttade datorobjektet `AD-User` från den inbyggda Computers-containern.
* OU-Users – där jag skapade ett användarkonton:
    - bob
* OU-Admins - där jag skapade ett administratör konto
    - bob.admin

För administratörskontot bob.admin lade jag till gruppen Domain Admins under Member Of. Detta gav kontot administrativa rättigheter i domänen, medan Bob behöll vanliga användarbehörigheter enligt principen om least privilege. 
Jag verifierade sedan att båda kontona kunde logga in på klientdatorn.
