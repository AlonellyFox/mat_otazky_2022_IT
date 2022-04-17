# MOTD
- Po připojení k routeru se ukáže tzv. **MOTD – Message Of The Day** s libovolným textem
- Nastaví se v konfiguračním módu následujícím příkazem:

*Router(config)#banner motd #Nějaký vlastní text#*
## Protokoly vzdálené správy
- Slouží ke vzdálenému ovládání zařízení odkudkoliv
- Nejvíce využívané ke vzdálené konfiguraci a ovládání je SSH a dříve předchůdce Telnet
- Telnet je oproti SSH nijak nezabezpečený, nešifruje data, jsou přenášena v plaintextu, tedy v současné době je jej nevhodno využívat
- Konfigurace telnetu z routeru:

*Router(config)#int (název interface)*

*Router(config-if)#ip address (nějaká adresa a maska)*

*Router(config-if)#no shut*

*Router(config-if)#exit*

*Router(config)#int vlan 1*

*Router(config-if)#no shut*

*Router(config-line)#line vty 0 15*

*Router(config-line)#password (heslo)*

*Router(config-line)#login*

- Připojení k telnetu pomocí *telnet (ip gateway)*
- Konfigurace SSH z routeru je :

*Router(config)#username (nazev) secret (heslo)*

*Router(config)#hostname (název routeru)*

*nazev\_routeru(config)#enable secret (heslo)*

*nazev\_routeru(config)#ip domain -name (název sítě)*

*nazev\_routeru(config)#crypto key generate rsa*

*(zadáme velikost alespoň 768 a vyšší)*

*nazev\_routeru(config)#line vty 0 15*

*nazev\_routeru(config-line)#transport input ssh*

*nazev\_routeru(config-line)#login local*

- Připojení k SSH pomocí *SSH -l (username a ip gatewaye)*
## Nakládání s přístupovými hesly
- Tzv. nebuď kokot a nedávej si heslo do peněženky.
- Nedávej si stejné heslo pro všechny účty, každé heslo by mělo být unikátní
- Hesla by měly obsahovat speciální znaky, čísla atd.
- Lze využít keypass a alternativy, ty však nejsou 100% bezpečné, je možnost, že budou prolomeny
- Vedle hesla je vhodné využívat ještě druhou možnost ověřování
- Přihlašuj se na stránky s HTTPS protokolem, přes HTTP lze heslo snadno získat.
## Zabezpečení přístupu na úrovni konzoly a virtuálního připojení (Cisco)
- ` `User EXEC:

*Router(config)#line console 0*

- Privileged EXEC

*Router(config)#enable secret (heslo)* 

- VTY

*Router(config)#line vty 0 15*

*Router(config-line)#login*
## Pilíře informační bezpečnosti 
### Confidentiality – Důvěrnost
- Důvěrnost brání prozrazení informací neoprávněným osobám, zdrojům a procesům. Dalším termínem důvěrnosti je soukromí. Organizace omezují přístup, aby zajistily, že data nebo jiné síťové zdroje mohou používat pouze oprávnění operátoři. Například programátor by neměl mít přístup k osobním informacím všech zaměstnanců.
- Organizace musí školit zaměstnance o osvědčených postupech při ochraně citlivých informací, aby se chránily samy a organizace před útoky. Metody používané k zajištění důvěrnosti zahrnují šifrování dat, ověřování a řízení přístupu.
### Integrity – Integrita
- Integrita je přesnost, konzistence a důvěryhodnost dat během celého jejich životního cyklu. - Dalším pojmem integrity je kvalita. Data procházejí řadou operací, jako je zachycení, uložení, načtení, aktualizace a přenos. Data musí během všech těchto operací neoprávněných subjektů zůstat nezměněna.
- Metody používané k zajištění integrity dat zahrnují hašování, kontroly validace dat, kontroly konzistence dat a kontroly přístupu. Systémy integrity dat mohou zahrnovat jednu nebo více výše uvedených metod.
### Availability – Dostupnost
- Dostupnost údajů je princip, který se používá k popisu potřeby udržovat dostupnost informačních systémů a služeb za všech okolností. Kybernetické útoky a selhání systému mohou zabránit přístupu k informačním systémům a službám. 
- Například přerušení dostupnosti webové stránky konkurenta jeho snížením může poskytnout výhodu jeho soupeři. Tyto útoky odmítnutí služby ohrožují dostupnost systému a v případě potřeby brání legitimním uživatelům v přístupu k informačním systémům a jejich používání.
- Metody používané k zajištění dostupnosti zahrnují redundanci systému, zálohování systému, zvýšenou odolnost systému, údržbu zařízení, aktuální operační systémy a software a zavedené plány na rychlé zotavení z nepředvídaných katastrof.
## Principy šifrování (protokoly) a jejich využití
### Symetrické
- Např. AES, RC5
- Mají jeden a ten samý klíč k šifrování i dešifrování
- Funguje na principu předem domluveného klíče mezi odesílatelem a příjemcem, odesílatel zprávu zašifruje, příjemce dešifruje
- Výhodou je snadná realizace a malá výpočetní náročnost
- Slabinou je nutnost zabezpečení přenosu šifrovacího klíče
### Asymetrické
- Např. RSA
- Využívá dva klíče – jeden k šifrování, druhý k dešifrování
- Šifrovací klíč, neboli veřejný je komukoliv přístupný a kdokoliv jím může zašifrovat soubory určené jemu, dešifrovací klíč je soukromý, jeho majitel ho musí ponechat v bezpečí a pomocí něho si pro něj určené zprávy dešifruje.
- Výhodou je ještě vyšší bezpečnost, než u symetrického šifrování, jelikož pomocí veřejného klíče lze ověřit autora zprávy
- Nevýhodou je vyšší výpočetní náročnost
## Význam FW – Firewall
- Firewall je síťové zařízení, které slouží k řízení a zabezpečování síťového provozu mezi sítěmi s různou úrovní důvěryhodnosti a zabezpečení. 
- Zjednodušeně se dá říct, že slouží jako kontrolní bod, který definuje pravidla pro komunikaci mezi sítěmi, které od sebe odděluje. Tato pravidla historicky vždy zahrnovala identifikaci zdroje a cíle dat (zdrojovou a cílovou IP adresu) a zdrojový a cílový port, což je však pro dnešní firewally už poměrně nedostatečné – modernější firewally se opírají přinejmenším o informace o stavu spojení, znalost kontrolovaných protokolů a případně prvky IDS. 
- Firewally se během svého vývoje řadily zhruba do následujících kategorií:
- Paketové filtry
- Aplikační brány
- Stavové paketové filtry
- Stavové paketové filtry s kontrolou známých protokolů a popř. kombinované s IDS
## IPS/IDS
IDS – Intrusion Detection Systems

- Má na starost monitoring provozu v síti a porovnává jej se škodlivými kódy ve své databázi, pracuje podobně jako antivirus
- Průběžně podává zprávy o provozu, nevykonává však žádné kroky, je zcela pasivní, nemůže tedy nijak zabránit útoku, pouze na něj upozorní
- Díky pouhé detekci však nijak nenarušuje rychlost přenosu dat
### IPS – Intrusion Prevention Systems
- Funguje na bázi IDS, avšak může zablokovat podezřelé data, respektive neumožnit jejich vstup do sítě, vzhledem k tomu, že veškerý příchozí i odchozí přenos dat teče přes něj.
- Umožňuje tedy blokování, analyzování, monitorování a detekování hrozeb na síti, data, které přes něj nejdou se nedostanou ze sítě/do sítě.
- Může však negativně ovlivňovat rychlost přenosu kvůli analyzování
## Antivir/antimalware
- Slouží k zachycení škodlivého softwaru a počítačových virů, k tomuto využívá několik metod
  - Kontrola aktivity programu v reálném čase
  - Pravidelná kontrola zejména nově stažených souborů 
- Soubory se porovnávají s neustále se aktualizující databází, má-li tedy antivir zastaralou databázi, nemusí odhalit všechny viry, je nutné pravidelně nechat databázi aktualizovat se.
- Zároveň funguje tzv. heuristická analýza – pomocí AI zkouší detekovat, jestli není nějaká část kódu škodlivá, využívá se k detekci nových a ještě neznámých počítačových virů.
## Opatření in use, at rest, in transit
### In use 
- Ověření uživatele, ideálně dvoufázovým ověřením
- Také je vhodné nastavit soubor tak, aby jej mohl spustit jen uživatel, pro kterého je určen a nikdo jiný, zabrání se tak ztrátě citlivých informací
- Také by mělo být zajištěno šifrování dat
### At rest
- Šifrování disku a zařízení
- Šifrování konkrétních souborů a složek, zamezení přístupu nepovolaným osobám
- Vytváření otisků pro porovnávání změn a detekce změn souborů
- Fyzické zabezpečení proti krádeži disků
- Zálohy dat na bezpečné vzdálené uložiště
### In transit
- Porovnání otisku souborů
- Šifrovaný přenos dat přes zabezpečený protokol
- Kontrola provozu na síti a ověření, že nikdo jiný nenaslouchá

```
Editace: David Kabeláč
Autor: Sádlík Kryštof
Datum: 17.04.2022
```
