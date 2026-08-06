# Konfigurering av Active Directory miljön.(Work in progress)

Jag började med att skapa två egna Organizational Units (OU):

* OU-Computers – där jag flyttade datorobjektet `AD-User` från den inbyggda Computers-containern.
* OU-Users – där jag skapade ett användarkonton:
    - bob
* OU-Admins - där jag skapade ett administratör konto
    - bob.admin

 Sedan skapade jag en GPO för OU-Users där jag:
* Blockerade kontrollpanelen
  - <img width="555" height="123" alt="bild" src="https://github.com/user-attachments/assets/ed6674e9-13e0-470d-8a9e-2f0292548dbf" />

* Stängde av Command-Prompt
  - <img width="542" height="131" alt="bild" src="https://github.com/user-attachments/assets/dea854ac-b85b-44cb-a7fb-dc0366beb22b" />

* Blockerade åtkomst till Registry-editor
  - <img width="387" height="124" alt="bild" src="https://github.com/user-attachments/assets/d9e0862a-c6f2-47ba-b0f9-ac7a543eac44" />

* Aktiverade skärmlås som startar efter 15 min inaktivitet.

Sedan loggade jag in på `Bobs` konto för att testa att allt fungerade.

För administratörskontot bob.admin lade jag till gruppen Domain Admins under Member Of. Detta gav kontot administrativa rättigheter i domänen, medan Bob behöll vanliga användarbehörigheter enligt principen om least privilege. 
Jag verifierade sedan att båda kontona kunde logga in på klientdatorn.
