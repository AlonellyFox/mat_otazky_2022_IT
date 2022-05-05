# 19. Hardware podnikových řešení

>Rozdíl mezi HW PC a HW serveru, procesory pro servery, SMP. UEFI, DRAC/iLO. Rozhraní iSCSI, FC, SAS, disková
pole RAID (0, 1, 4, 5, 6, 10, 50), disky pro RAID, NAS, archivační možnosti, redundance řešení (zvýšení dostupnosti
zařízení – cluster, failover, failsafe, UPS), SW pro zálohování.

---

## Rozdíl mezi HW PC a HW serveru

PC a server se liší poskytováním služeb na síti, které třeba PC nemá. 
Server obsluhuje účastníky na síti tedy pc uživatele. 
Servery se nacházejí v místnosti, která se nazývá serverovna kdežto obyčejný PC se nachází například v kanceláři a pracují s ním obyčejní lidé.
Hardware na serverech bývá většinou výkonnější než běžné pracovní stanice a to znamená, že komponenty jsou dražší a například jako u RAM pamětí jsou certifikována.
Server s nachází ve skříni která se nazývá rack. [](..\AppData\Local\Programs\Microsoft VS Code\editor.action.unicodeHighlight.disableHighlightingOfNonBasicAsciiCharacters)
Většinou by u sebe měli mít UPS napájená, protože výpadek serveru se nesmí stát, aby mohl lidem poskytovat služby 24-7.
Základní deska se liší například tím, že na serverových deskách se nachází více soketů pro cpu oproti základní desce osobního pc.
Dále také může mýt mnoho disků či mnoho slotů pro RAM paměti či přídavné karty jako jsou grafické, síťové karty.

---

## Procesory pro servery - SMP

Symetrický multiprocesing (SMP, anglicky Symmetric multiprocessing) je označení pro druh víceprocesorových systémů, u kterých jsou všechny procesory v počítači rovnocenné.
Zvýšení počtu procesorů, které v počítači sdílí stejnou operační paměť, vede ke zvýšení výkonu počítače, i když ne lineárním způsobem, protože část výkonu je spotřebována na režii.
Je-li procesorů v SMP systému mnoho, označujeme je jako masivně paralelní systémy (MPP, anglicky Massive Parallel Processing), u kterých je využívána NUMA architektura. 
Opakem víceprocesorových systémů jsou jednoprocesorové systémy (anglicky uniprocessor, zkratka UP). 
Výrobci serverových procesorů jsou například Intel (řada Xeon) a AMD (řady EPYC).

---

## UEFI

Unified Extensible Firmware Interface je specifikace, která definuje softwarové rozhraní mezi operačním systémem a firmwarem použitého hardwaru.
UEFI je určeno jako významně vylepšená náhrada zastaralého firmwarového rozhraní BIOS, které se používalo během celé historie IBM PC kompatibilních osobních počítačů.

---

## DRAC/iLO.

Vzdálený přístup IPMI HP, Dell má webové rozhraní, které umožňuje kontrolovat stav a zdraví serveru a vzdáleně jej aktualizovat a konfigurovat.
Je zabudováno v hardwaru. Oba nástroje mají vyhrazený síťový port pro připojení a nástroj je v serveru předinstalován. 
Je integrován do hardwaru. Pokud tedy dojde k poruše operačního systému zařízení, můžete stále přistupovat k serveru (zatímco v případě použití nástroje pro vzdálený přístup k operačnímu systému by to nebylo možné).
Jedná se o systém Out of Band - což znamená, že k serveru může vzdáleně přistupovat uživatel mimo jeho síť.

---

## iSCSI

Internet Small Computer System Interface je v informatice síťový protokol, který umožňuje připojovat úložný prostor pomocí počítačové sítě.
Příkladem jsou naše síťové disky ve škole kde si ukládáme data.

---

## FC (Fiber-cable)

Optical fiber connector
Konektor optického vlákna spojuje optická vlákna a umožňuje rychlejší připojení. 
Konektory se mechanicky spojují a srovnávají jádra vláken, aby mohlo projít světlo. 
Lepší konektory ztrácejí velmi málo světla v důsledku odrazu nebo vychýlení vláken.
Používá se na delší vzdálenosti.

---

## SAS

Serial Attached SCSI (SAS) je v informatice sériová sběrnice, která nahrazuje paralelní sběrnici SCSI. 
Slouží k připojení pevných disků a páskových jednotek. Poprvé byla představena v 80. letech 20. století.
Pro komunikaci používá standardní příkazy SCSI. V roce 2008 byla o něco pomalejší než toho času aktuální standard SCSI, avšak v roce 2009 byla její rychlost zdvojnásobena na 6 Gbit/s. 
Je zpětně kompatibilní se SATA 2.0, takže disky se 3.0 Gbit/s SATA lze připojit na rozhraní SAS, avšak disky SAS k rozhraní SATA připojit nelze. 

---

## Disková pole RAID

Zkratka RAID (Redundant Array of Inexpensive/Independent Disks) označuje disková pole, na nichž se ukládají data na dva a více nezávislých disků. 
Z několika fyzických uzlů se tím vytvoří úložiště, které operační systém serveru nebo počítače vnímá jako jednu logickou jednotku.
RAID  (0, 1, 4, 5, 6, 10, 50)

### RAID 0

Pole RAID 0 není vlastně skutečný RAID, protože neobsahuje žádné redundantní informace, a tedy neposkytuje uloženým datům žádnou ochranu. 
Jednotlivá zařízení jsou jen spojena do logického celku a vytváří tak kapacitu součtu všech členů. 
Spojení může být realizováno dvěma způsoby: jako zřetězení (tj. lineárně, anglicky linear), anebo prokládání (anglicky striping).

#### Zřetězení (JBOD)

JBOD - zřetězení
Just a Bunch Of Disks neboli „jen hromada disků“.
Ve zřetězení jsou data postupně ukládána na několik disků.
Jakmile se zaplní první, ukládá se na druhý, poté na třetí atd (za sebou, viz obrázek JBOD).
Výhodou je snadné zvětšení kapacity přidáním dalšího členu a skutečnost, že při výpadku členu mohou být některé soubory nedotčeny.
Pokud jsou v JBODu zapojeny dva a více disků s odlišnou kapacitou, zachová se maximální kapacita úložiště.

#### Prokládání

Při prokládání jsou data ukládána na disky cyklicky (střídavě, viz obrázek RAID 0 - striping).
Prostor je rozdělen na části pevné velikosti a zápis nebo čtení delšího úseku dat tak probíhá z více disků. 
Při poruše disku není pravděpodobné, že by nějaký soubor zůstal nepoškozen. 
Prokládání může zrychlit čtení i zápis větších bloků dat, protože je možné zároveň číst (zapisovat) jeden blok z jednoho disku a následující blok z jiného disku. 
Zrychlení čtení by mělo být teoreticky menší, než v případě RAID 1, avšak při reálném použití je čtení i zápis v režimu RAID 0 výrazně rychlejší než v RAID 1. 
Výkonnostní nárůst při sekvenčním čtení bývá v domácích podmínkách kolem 50 % (tj. při použití dvou disků se sekvenčním čtením 100 MB/s bude mít diskové pole rychlost čtení (obvykle) přibližně 150 MB/s).
Zvýšení o 50 % samozřejmě neznamená o polovinu vyšší výkon, jelikož zapojení do RAID 0 nesnižuje přístupovou dobu. 
Pokud jsou v RAID 0 Striping zapojeny dva a více disků s odlišnou kapacitou, maximální kapacita úložiště bude rovna velikosti nejmenšího disku krát počet zapojených disků.

---

### RAID 1

Nejjednodušší, ale poměrně efektivní ochrana dat.
Provádí se zrcadlení (mirroring) obsahu disků.
Obsah se současně zaznamenává na dva disky.
V případě výpadku jednoho disku se pracuje s kopií, která je ihned k dispozici.
Podobná technika může být uplatněna o úroveň výše, kdy jsou použity dva samostatné řadiče.
Tato technika se nazývá duplexing a je odolná i proti výpadku řadiče.
Teoreticky se může výrazně zvýšit rychlost čtení a o něco snížit odezva, avšak záleží na konkrétním řadiči (softwarové řadiče většinou možnost čtení z obou disků nevyužijí vůbec).
Zato zápis může být pomalejší, protože se ukládají stejná data na dva disky.
Technika výrazně zvyšuje bezpečnost dat proti ztrátě způsobené poruchou hardware.
Nevýhodou je potřeba dvojnásobné diskové kapacity.

---

### RAID 4

Disky jsou stripovány po blocích, ne po bitech a parita je na paritním disku opět ukládána po blocích. Výhody a nevýhody jsou stejné jako u RAID 3.

---

### RAID 5 

Vyžaduje alespoň 3 členy, přičemž kapacitu jednoho členu zabírají samoopravné kódy (neboli parity), které jsou uloženy na členech střídavě (a ne pouze na jednom, čímž byla odstraněna nevýhoda RAID 4).
Výhodou je, že lze využít paralelního přístupu k datům, protože delší úsek dat je rozprostřen mezi více disků, takže čtení je rychlejší.
Nevýhodou je pomalejší zápis (nutnost výpočtu samoopravného kódu). Je odolný vůči výpadku jednoho disku.

---

### RAID 6

Obdoba RAID 5, používá dva paritní bloky na každém z použitých disků, přičemž na každém z nich je samoopravný kód vypočten jiným způsobem.
Opět kvůli přetížení paritních disků jsou paritní data uložena střídavě na všech discích. Výhodou je odolnost proti výpadku dvou disků.
Rychlost čtení je srovnatelná s RAID 5, ale zápis je pomalejší než u RAID 5, právě kvůli výpočtu dvou sad paritních informací.
RAID 6 je možno sestavit z minimálně čtyř disků (pokud bychom neuvažovali rozprostření paritních informací na všechny disky, pak by se dalo zjednodušeně říci, že dva jsou datové a dva paritní).
V této minimální konfiguraci se však s ohledem na výslednou kapacitu příliš nepoužívá, neboť kapacita pole je poloviční, tedy stejná jako v konfiguraci zrcadlení (RAID 1) dvou párů disků.
Při zrcadlení navíc není třeba počítat dvě sady paritních informací, je tedy mnohem rychlejší při zápisu a nepotřebuje vysoký výpočetní výkon.
RAID 6 je tedy výhodné při použití pěti a více disků. 

---

### RAID 10 (RAID 1+0)

Pole RAID 1+0 (stripování) je opět kombinací RAID 0 a RAID 1, ale postupujeme obráceně.
Nejdříve uložíme stejná data na disk A, B, poté na disk C, D.
Získáme tak dva logické disky AB, CD, na nichž jsou data uložena stripovaně.
Máme-li soubor, který se při stripování rozdělí na dvě poloviny, první část souboru je na disku A a B, druhá část je na disku C a D, na rozdíl od RAID 0+1) RAID 1+0 je odolný proti výpadku jednoho disku v každém podpoli.
Výhody jsou podobné RAID 0+1, navíc je obnova dat po chybě oproti RAID 0+1 mnohem rychlejší.
Díky stripování dat a faktu, že se nemusí dopočítávat paritní data toto pole, dosahuje velkých přenosových rychlostí, proto se často používá pro hodně vytížené databázové aplikace.
Nevýhodou je opět využití pouze 50 % kapacity, využitelná kapacita se vypočítá následovně (c = kapacita nejmenšího použitého disku; n = celkový počet disků v diskovém poli):

velikost = n ⋅ c 2 {\displaystyle velikost={\frac {n\cdot c}{2}}} {\displaystyle velikost={\frac {n\cdot c}{2}}} 

---

### RAID 50 (RAID 5+0)

RAID 50 je dvouúrovňové pole, vytvořené prokládáním několika RAID 5 polí.
Prokládání zvyšuje rychlost oproti jednoúrovňovému RAID 5, ovšem v každém podpoli je potřeba jeden disk navíc na paritní data, to znamená, že pole je odolné proti selhání jednoho disku každého podpole (oproti RAID 60, které je odolné proti selhání dvou disků v každém podpoli).
Celková velikost se vypočítá podle následujícího vzorce, kde n = počet disků v podřazeném poli RAID 5; c = kapacita disku; p = počet podřazených polí.

velikost = ( n − 1 ) ⋅ c ⋅ p {\displaystyle velikost=(n-1)\cdot c\cdot p} {\displaystyle velikost=(n-1)\cdot c\cdot p}

---

## NAS

Network Attached Storage (zkratka NAS, česky „datové úložiště na síti“) je označení pro datové úložiště připojené k místní síti LAN.
Data toho úložiště mohou být poskytována různým uživatelům. NAS nemusí mít pouze funkci souborového serveru, ale může mít i jiné specializované funkce.
Například klient P2P sítě, webový server a další. Většinou obsahuje nějaký vestavěný počítač, který má za úkol sdílení dat a podporu různých protokolů.
Tato zařízení si získala popularitu od roku 2010, když začala být používána pro sdílení dat mezi několika počítači.
V porovnání mezi jinými síťovými úložišti jsou NASy rychlejší, mají lehčí administraci a snadnější nastavení.
NAS obsahuje jeden nebo více pevných disků, které se mohou slučovat do větších datových struktur nebo mohou vytvořit RAID pole.
Levnější zařízení podporují hlavně RAID 0 a 1.

---

## Archivační možnosti

Archivační technologie řeší něco jiného. 
Jsou určeny primárně k uchovávání starších či neaktuálních dat po určitou dobu, většinou z na základě regulačních požadavků či potřeby dohledávání starších informací obsažených například v podnikových e-mailech. Specializovaná archivační řešení typicky přemisťují informace určené k archivaci do úložišť, která jsou cenově výhodnější než v případě zálohování.
Na rozdíl od zálohování existují archivovaná data jenom v jedné kopii, takže v případě havárie systému může firma o tato data přijít úplně, i když to nemusí pro firmu znamenat bezprostřední katastrofu.
Přístup k archivovaným informacím je zajištěn tak, aby poskytl okamžitý granulární přístup k uloženým informacím s možností vyhledávání a přístupu k jednotlivým souborům či e-mailům. 
Na rozdíl od backup systémů nemůže archivační řešení zajistit kompletní obnovu systémů, protože obsahuje pouze podmnožinu podnikových dat.
Archivace umožňuje držet v archivu veškerá data z historie firmy. 
V SMB firmách zpravidla stačí archivovat elektronickou poštu ve stavu, v jakém přišla a odešla.
Archivace elektronické pošty je ze zákona stejně důležitá jako archivace obchodní korespondence a v důsledku toho, že dnes je většina faktur posílána elektronicky ve formátu PDF, je dokonce archiv elektronické pošty vyžadován zákonem o účetnictví.
Archivační řešení umožňuje rychlé vyhledávání informací, což je velkým přínosem pro uživatele – podle průzkumu společnosti GFI Software se s problémem, že zaměstnanci ztratili či nemohli nalézt důležité e-maily, se často setkává přes 90 % českých firem.
V segmentu SMB firem je populární řešení GFI Archiver, které umožňuje uživatelům komfortně vyhledávat starší e-maily přímo z nejrozšířenějšího poštovního klienta Microsoft Outlook.
Zálohování není archivace a ani archivace není zálohování: zatímco zálohování vás kompletně vrátí tam, kde jste byli v okamžiku zálohy, archivace vám vrátí jen soubory a e-maily, které vznikly do okamžiku archivace, tj. teoreticky až do současnosti. Proto se doporučuje kombinovat oba přístupy.

---

## Cluster

Počítačový cluster (anglicky computer cluster) je seskupení volně vázaných počítačů, které spolu úzce spolupracují, takže se navenek mohou tvářit jako jeden počítač.
Obvykle jsou propojeny počítačovou sítí.
Clustery jsou obvykle nasazovány pro zvýšení výpočetní rychlosti nebo spolehlivosti s větší efektivitou než by mohl poskytnout jediný počítač, přičemž jsou levnější než jediný počítač srovnatelné rychlosti nebo spolehlivosti.
Clustery slouží k paralelním výpočtům složitých početních úloh (např. faktorizace na prvočísla, simulace vývoje počasí, analýza velkého množství statistických dat, atp.), nebo se používají pro zajištění vysoké dostupnosti určité služby (např. databáze, SMS centra, apod.).
Používají se buď specializované víceprocesorové stroje propojené sítí, nebo obyčejné počítače třídy PC.

---

### Serverový cluster

Serverový cluster je vytvářen několika servery, které mezi sebou úzce spolupracují (jsou seskupeny).
Lze vytvořit i serverový cluster, který je kombinací výše uvedených typů.
Toto seskupení má přínos především v oblasti virtualizací.
Například u virtualizační platformy VMware lze za předpokladu spolupráce několika hypervizorů (ESXi) dosáhnout současně High availability i Load ballancing clusteru.
V případě, je-li nějaký z hypervizorů (serverů) vytížen, jsou některé z virtuálních strojů přesunuty (přemigrovány) na hypervizor (server), který má nejmenší vytížení (utilizaci).
Pakliže jeden z hypervizorů (serverů) selže, jednotlivé virtuální stroje jsou spouštěny na dalších funkčních hypervizorech (serverech) v daném clusteru.

---

## Failover

Failover je výraz pro automatické spuštění aplikace či služby na záložním serveru poté, co primární server neočekávaně selže.
Obdobně se tento výraz používá pro automatické přesměrování datového toku na záložní síť, směrovač, atp. po selhání stávající sítě.

---

## Fail-safe

Failover je výraz pro automatické spuštění aplikace či služby na záložním serveru poté, co primární server neočekávaně selže.
Obdobně se tento výraz používá pro automatické přesměrování datového toku na záložní síť, směrovač, atp. po selhání stávající sítě.
Obdobnou operací je přepnutí, s tím rozdílem, že failover proběhne zcela automaticky. 
Návrháři systémů obvykle poskytují schopnost převzetí služeb při selhání v serverech, systémech nebo sítích vyžadujících téměř nepřetržitou dostupnost a vysoký stupeň spolehlivosti .
Na úrovni serveru používá automatizace failover obvykle systém „heartbeat“, který spojuje dva servery, buď pomocí samostatného kabelu (například sériové porty RS-232/kabel), nebo síťového připojení.
Dokud bude mezi hlavním serverem a druhým serverem pokračovat pravidelný „puls“ nebo „srdeční tep“, druhý server nebude své systémy uvádět do provozu.
Může existovat i třetí server „náhradních dílů“, na kterém jsou spuštěny náhradní komponenty pro „horké“ přepínání, aby se zabránilo prostojům.
Druhý server převezme práci prvního, jakmile zjistí změnu „tepu srdce“ prvního stroje.
Některé systémy mají možnost odeslat oznámení o výpadku.
Některé systémy záměrně selhávají ne zcela automaticky, ale vyžadují lidský zásah. Tato konfigurace „automatizovaná s manuálním schválením“ se spustí automaticky, jakmile člověk schválí funkci failover.
Failback je proces obnovení systému, součásti nebo služby dříve ve stavu selhání zpět do původního, funkčního stavu a uvedení záložního systému zpět do pohotovostního stavu.
Použití virtualizačního softwaru umožnilo, aby se postupy převzetí služeb při selhání staly méně závislými na fyzickém hardwaru prostřednictvím procesu označovaného jako migrace, ve kterém je běžící virtuální počítač přesunut z jednoho fyzického hostitele na druhého, s malým nebo žádným narušením služeb.

---

## UPS

Zdroj nepřerušovaného napájení, často označovaný zkratkou UPS je zařízení, které zajišťuje souvislou dodávku elektrické energie pro spotřebiče, které nesmějí být neočekávaně vypnuty.
Příkladem je server, který nesmí vypadnout při výpadku elektrické energie.

---

```
Autor: Zdražil Patrik
Datum: 5.5.2022
```
