<p class="has-line-data" data-line-start="0" data-line-end="1"><img src="https://nordlo.com/wp-content/uploads/2019/08/nordlologo.svg" alt="Build Status"></p>
<h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="Checklista_fr_skrare_Active_Directory_1"></a>Checklista för säkrare Active Directory</h2>
<h5 class="code-line" data-line-start=2 data-line-end=3 ><a id="Begrnsa_domain_och_Enterprise_admins_2"></a>Begränsa domain och Enterprise admins</h5>
<p class="has-line-data" data-line-start="3" data-line-end="4">Gå igenom AD och begränsa konton med högre rättigheter. Använd dig av least privilege administrative model. Använd <a href="https://gallery.technet.microsoft.com/scriptcenter/AD-account-Audit-find-bfcc60db">PowerShellscriptet</a> för att hitta dessa konton.</p>
<h5 class="code-line" data-line-start=5 data-line-end=6 ><a id="Stda_ADet_5"></a>Städa AD:et</h5>
<p class="has-line-data" data-line-start="6" data-line-end="7">Radera gamla dator och gamla användarkonton, avaktiverade konton, tjänstekonton som inte används m.m.</p>
<h5 class="code-line" data-line-start=8 data-line-end=9 ><a id="Anvnd_minst_2_konton_vanliga_och_admin_kontot_8"></a>Använd minst 2 konton, vanliga och admin kontot</h5>
<p class="has-line-data" data-line-start="9" data-line-end="10">Admin konton ska endast användas för att administrera AD:et eller systemen, om det krävs. Helst ska det finnas 3 olika kontonivåer, vanligt konto för att lösa vardagliga arbetsuppgifter, adminkonto med helpdesk roll för att administrera AD, så som användare, grupper, DHCP, DNS, GPO:er m.m. och ett adminkonto med högre rättigheter för att administrera systemen vid behov, exempelvis AD restore m.m.</p>
<h5 class="code-line" data-line-start=11 data-line-end=12 ><a id="Anvnd_inte_Domain_Administrator_kontot_11"></a>Använd inte Domain Administrator kontot</h5>
<p class="has-line-data" data-line-start="12" data-line-end="14">Domänadministratörs kontot som är Enterprise admin bör endast användas för uppsättning och återställning av AD.<br>
Använd personliga konton med rollanpassade rättigheter för allt annat.</p>
<p class="has-line-data" data-line-start="15" data-line-end="16">Följande GPO-inställningar bör vara applicerade på domänadministratörs kontot:</p>
<ul>
<li class="has-line-data" data-line-start="16" data-line-end="17">Enable the Account is sensitive and cannot be delegated.</li>
<li class="has-line-data" data-line-start="17" data-line-end="18">Enable the smart card is required for interactive logon.</li>
<li class="has-line-data" data-line-start="18" data-line-end="19">Deny access to this computer from the network.</li>
<li class="has-line-data" data-line-start="19" data-line-end="20">Deny logon as batch job.</li>
<li class="has-line-data" data-line-start="20" data-line-end="21">Deny log on as a service.</li>
<li class="has-line-data" data-line-start="21" data-line-end="23">Deny log on through RDP.</li>
</ul>
<h5 class="code-line" data-line-start=23 data-line-end=24 ><a id="Avaktivera_lokala_administratrskontot_och_anvnd_LAPS_23"></a>Avaktivera lokala administratörskontot och använd LAPS</h5>
<p class="has-line-data" data-line-start="24" data-line-end="25">Det lokala administratörskontot bör avaktiveras och LAPS bör implementeras. Problemet med det lokala administratörskontot är att den har samma SID på alla datorer och har oftast samma lösenord.</p>
<h5 class="code-line" data-line-start=26 data-line-end=27 ><a id="Anvndarna_som_lokala_administratrer_26"></a>Användarna som lokala administratörer</h5>
<p class="has-line-data" data-line-start="27" data-line-end="28">Användarna ska inte vara lokala admins på datorerna.</p>
<h5 class="code-line" data-line-start=29 data-line-end=30 ><a id="Anvnd_SAW_Secure_Admin_Workstation_29"></a>Använd SAW (Secure Admin Workstation)</h5>
<p class="has-line-data" data-line-start="30" data-line-end="31">Använd en SAW för att administrera systemen. SAW ska endast användas för att administrera systemen och inte för surf, mail m.m. Minimal programvara. Se exempelvils <a href="https://www.microsoft.com/sv-se/cloud-platform/windows-admin-center">Windows Admin Center</a>.</p>
<h5 class="code-line" data-line-start=32 data-line-end=33 ><a id="Aktivera_Audit_policyn_32"></a>Aktivera Audit policyn</h5>
<p class="has-line-data" data-line-start="33" data-line-end="34">Konfigurera följande GPO:er</p>
<blockquote>
<p class="has-line-data" data-line-start="34" data-line-end="35">Computer Configuration -&gt; Policies -Windows Settings -&gt; Security Settings -&gt; Advanced Audit Policy Configuration</p>
</blockquote>
<p class="has-line-data" data-line-start="36" data-line-end="38"><code>Account Logon</code><br>
Säkerställ att ‘Audit Credential Validation’ är inställt på ‘Success and Failure’</p>
<p class="has-line-data" data-line-start="39" data-line-end="45"><code>Account Management</code><br>
Audit ‘Application Group Management’ är ‘Success and Failure’<br>
Audit ‘Computer Account Management’ är ‘Success and Failure’<br>
Audit ‘Other Account Management Events’ är ‘Success and Failure’<br>
Audit ‘Security Group Management’ är ‘Success and Failure’<br>
Audit ‘User Account Management’ är ‘Success and Failure’</p>
<p class="has-line-data" data-line-start="46" data-line-end="49"><code>Detailed Tracking</code><br>
Audit ‘PNP Activity’ är ‘Success’<br>
Audit ‘Process Creation’ är ‘Success’</p>
<p class="has-line-data" data-line-start="50" data-line-end="57"><code>Logon/Logoff</code><br>
Audit ‘Account Lockout’ är ‘Success and Failure’<br>
Audit ‘Group Membership’ är ‘Success’<br>
Audit ‘Logoff’ är ‘Success’<br>
Audit ‘Logon’ är ‘Success and Failure’<br>
Audit ‘Other Logon/Logoff Events’ är ‘Success and Failure’<br>
Audit ‘Special Logon’ är ‘Success’</p>
<p class="has-line-data" data-line-start="58" data-line-end="60"><code>Object Access</code><br>
Audit ‘Removable Storage’ är ‘Success and Failure’</p>
<p class="has-line-data" data-line-start="61" data-line-end="65"><code>Policy Change</code><br>
Audit ‘Audit Policy Change’ är ‘Success and Failure’<br>
Audit ‘Authentication Policy Change’ är ‘Success’<br>
Audit ‘Authorization Policy Change’ är ‘Success’</p>
<p class="has-line-data" data-line-start="66" data-line-end="68"><code>Privilege Use</code><br>
Audit ‘Sensitive Privilege Use’ är ‘Success and Failure’</p>
<p class="has-line-data" data-line-start="69" data-line-end="75"><code>System</code><br>
Audit ‘IPsec Driver’ är ‘Success and Failure’<br>
Audit’ Other System Events’ är ‘Success and Failure’<br>
Audit ‘Security State Change’ är ‘Success’<br>
Audit ‘Security System Extension’ är ‘Success and Failure’<br>
Audit ‘System Integrity’ är ‘Success and Failure’</p>
<h5 class="code-line" data-line-start=76 data-line-end=77 ><a id="vervaka_AD_hndelser_76"></a>Övervaka AD händelser</h5>
<p class="has-line-data" data-line-start="77" data-line-end="86">Använd gärna något övervakningsverktyg för övervakning och analys av följande händelser:<br>
<code>Changes to privileged groups such as Domain Admins, Enterprise Admins and Schema Admins</code><br>
<code>A spike in bad password attempts</code><br>
<code>A spike in locked out accounts</code><br>
<code>Account lockouts</code><br>
<code>Disabled or removal of antivirus software</code><br>
<code>All actives performed by privileged accounts</code><br>
<code>Logon/Logoff events</code><br>
<code>Use of local administrator accounts</code></p>
<h5 class="code-line" data-line-start=87 data-line-end=88 ><a id="Lsenordspolicy_87"></a>Lösenordspolicy</h5>
<p class="has-line-data" data-line-start="88" data-line-end="89">Sätt upp en lösenordspolicy för alla AD-konton. Använd exempelvis <a href="https://blogs.technet.microsoft.com/canitpro/2013/05/29/step-by-step-enabling-and-using-fine-grained-password-policies-in-ad">Fine Grained Password Policies</a>.</p>
<h5 class="code-line" data-line-start=90 data-line-end=91 ><a id="Hll_domnkontrollanterna_rena_90"></a>Håll domänkontrollanterna rena</h5>
<p class="has-line-data" data-line-start="91" data-line-end="92">Installera inte roller och programvara på domänkontrollanterna. Dessa ska installeras på applikationsservrar.</p>
<h5 class="code-line" data-line-start=93 data-line-end=94 ><a id="Patcha_93"></a>Patcha</h5>
<p class="has-line-data" data-line-start="94" data-line-end="95">Patcha servrar och klienter och migrera bort enheter med gamla operativsystem.</p>
<h5 class="code-line" data-line-start=96 data-line-end=97 ><a id="Blockera_skadlig_trafik_med_hjlp_av_DNS_96"></a>Blockera skadlig trafik med hjälp av DNS</h5>
<p class="has-line-data" data-line-start="97" data-line-end="98">Quad9 är exempelvis gratis att använda och skyddar miljön igenom att blockerar trafik mot skadliga siter.</p>
<h5 class="code-line" data-line-start=99 data-line-end=100 ><a id="Aktivera_skerhetsfunktioner_i_AD_99"></a>Aktivera säkerhetsfunktioner i AD</h5>
<p class="has-line-data" data-line-start="100" data-line-end="101">Använd senaste OS för de kritiska systemen och aktivera funktioner som Crendential Guard som skyddar mot Pass the hash attacker.</p>
<h5 class="code-line" data-line-start=102 data-line-end=103 ><a id="Multifaktorautentisering_102"></a>Multifaktorautentisering</h5>
<p class="has-line-data" data-line-start="103" data-line-end="104">Använd MFA på alla system som stöjder funktionen.</p>
<h5 class="code-line" data-line-start=105 data-line-end=106 ><a id="vervaka_DHCP_och_DNS_105"></a>Övervaka DHCP och DNS</h5>
<p class="has-line-data" data-line-start="106" data-line-end="107">Övervaka DHCP och DNS loggarna för att hitta suspekta enheter och uppslag.</p>
<h5 class="code-line" data-line-start=108 data-line-end=109 ><a id="Kontrollera_backuper_108"></a>Kontrollera backuper</h5>
<p class="has-line-data" data-line-start="109" data-line-end="110">Kontrollera och säkerställ att backuperna fungerar enligt schemaläggningen och provkör återställning av data.</p>
<h5 class="code-line" data-line-start=111 data-line-end=112 ><a id="Skydda_tjnstekonton_111"></a>Skydda tjänstekonton</h5>
<p class="has-line-data" data-line-start="112" data-line-end="113">Skydda tjänstekonton med långa lösenord, begränsat åtkomst, neka as batch m.m.</p>
<h5 class="code-line" data-line-start=114 data-line-end=115 ><a id="Avaktivera_SMB1_114"></a>Avaktivera SMB1</h5>
<p class="has-line-data" data-line-start="115" data-line-end="116">Avaktivera SMB1 eftersom det protokollet är gammalt och osäkert. Många av de senaste årens attacker har använt sig av SMB1-protokollet.</p>
<h5 class="code-line" data-line-start=117 data-line-end=118 ><a id="Anvnd_Microsoft_Security_Baselines_117"></a>Använd Microsoft Security Baselines</h5>
<p class="has-line-data" data-line-start="118" data-line-end="119">Använd Security Compliance Toolkit för att analysera, testa och säkra miljön</p>
