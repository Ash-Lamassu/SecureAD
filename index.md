![Build Status](https://nordlo.com/wp-content/uploads/2019/08/nordlologo.svg)
# Checklista för säkrare Active Directory
### Begränsa domain och Enterprise admins
Gå igenom AD och begränsa konton med högre rättigheter. Använd dig av least privilege administrative model. Använd [PowerShellscriptet](https://gallery.technet.microsoft.com/scriptcenter/AD-account-Audit-find-bfcc60db) för att hitta dessa konton.

### Städa AD:et
Radera gamla dator och gamla användarkonton, avaktiverade konton, tjänstekonton som inte används m.m.

### Använd minst 2 konton, vanliga och admin kontot
Admin konton ska endast användas för att administrera AD:et eller systemen, om det krävs. Helst ska det finnas 3 olika kontonivåer, vanligt konto för att lösa vardagliga arbetsuppgifter, adminkonto med helpdesk roll för att administrera AD, så som användare, grupper, DHCP, DNS, GPO:er m.m. och ett adminkonto med högre rättigheter för att administrera systemen vid behov, exempelvis AD restore m.m.

### Använd inte Domain Administrator kontot
Domänadministratörs kontot som är Enterprise admin bör endast användas för uppsättning och återställning av AD.
Använd personliga konton med rollanpassade rättigheter för allt annat.

Följande GPO-inställningar bör vara applicerade på domänadministratörs kontot:
* Enable the Account is sensitive and cannot be delegated.
* Enable the smart card is required for interactive logon.
* Deny access to this computer from the network.
* Deny logon as batch job.
* Deny log on as a service.
* Deny log on through RDP.

### Avaktivera lokala administratörskontot och använd LAPS
Det lokala administratörskontot bör avaktiveras och LAPS bör implementeras. Problemet med det lokala administratörskontot är att den har samma SID på alla datorer och har oftast samma lösenord. 

### Användarna som lokala administratörer
Användarna ska inte vara lokala admins på datorerna.

### Använd SAW (Secure Admin Workstation)
Använd en SAW för att administrera systemen. SAW ska endast användas för att administrera systemen och inte för surf, mail m.m. Minimal programvara. Se exempelvils [Windows Admin Center](https://www.microsoft.com/sv-se/cloud-platform/windows-admin-center).

### Aktivera Audit policyn
Konfigurera följande GPO:er
> Computer Configuration -> Policies -Windows Settings -> Security Settings -> Advanced Audit Policy Configuration

> Account Logon`

Säkerställ att `Audit Credential Validation` är inställt på `Success and Failure`

> Account Management

`Audit Application Group Management` är `Success and Failure`

`Audit Computer Account Management är `Success and Failure`

`Audit Other Account Management Events` är `Success and Failure`

`Audit Security Group Management` är `Success and Failure`

`Audit User Account Management` är `Success and Failure`

> Detailed Tracking

`Audit PNP Activity` är `Success`
`Audit Process Creation` är `Success`

> Logon/Logoff

`Audit Account Lockout` är `Success and Failure`

`Audit Group Membership` är `Success`

`Audit Logoff` är `Success`

`Audit Logon` är `Success and Failure`

`Audit Other Logon/Logoff Events` är `Success and Failure`

`Audit Special Logon` är `Success`

> Object Access

`Audit Removable Storage` är `Success and Failure`

> Policy Change

`Audit Audit Policy Change` är `Success and Failure`

`Audit Authentication Policy Change` är `Success`

`Audit ‘Authorization Policy Change` är `Success`

> Privilege Use

`Audit Sensitive Privilege Use` är `Success and Failure`

`System`

Audit ‘IPsec Driver’ är ‘Success and Failure’

`Audit Other System Events` är `Success and Failure`

`Audit Security State Change` är `Success`

`Audit Security System Extension` är `Success and Failure`

`Audit System Integrity` är `Success and Failure`


### Övervaka AD händelser
Använd gärna något övervakningsverktyg för övervakning och analys av följande händelser:
`Changes to privileged groups such as Domain Admins, Enterprise Admins and Schema Admins`
`A spike in bad password attempts`
`A spike in locked out accounts`
`Account lockouts`
`Disabled or removal of antivirus software`
`All actives performed by privileged accounts`
`Logon/Logoff events`
`Use of local administrator accounts`

### Lösenordspolicy
Sätt upp en lösenordspolicy för alla AD-konton. Använd exempelvis [Fine Grained Password Policies](https://blogs.technet.microsoft.com/canitpro/2013/05/29/step-by-step-enabling-and-using-fine-grained-password-policies-in-ad).

### Håll domänkontrollanterna rena
Installera inte roller och programvara på domänkontrollanterna. Dessa ska installeras på applikationsservrar.

### Patcha
Patcha servrar och klienter och migrera bort enheter med gamla operativsystem.

### Blockera skadlig trafik med hjälp av DNS
Quad9 är exempelvis gratis att använda och skyddar miljön igenom att blockerar trafik mot skadliga siter.

### Aktivera säkerhetsfunktioner i AD
Använd senaste OS för de kritiska systemen och aktivera funktioner som Crendential Guard som skyddar mot Pass the hash attacker.

### Multifaktorautentisering
Använd MFA på alla system som stöjder funktionen.

### Övervaka DHCP och DNS
Övervaka DHCP och DNS loggarna för att hitta suspekta enheter och uppslag.

### Kontrollera backuper
Kontrollera och säkerställ att backuperna fungerar enligt schemaläggningen och provkör återställning av data.

### Skydda tjänstekonton
Skydda tjänstekonton med långa lösenord, begränsat åtkomst, neka as batch m.m.

### Avaktivera SMB1
Avaktivera SMB1 eftersom det protokollet är gammalt och osäkert. Många av de senaste årens attacker har använt sig av SMB1-protokollet.

### Använd Microsoft Security Baselines
Använd Security Compliance Toolkit för att analysera, testa och säkra miljön
