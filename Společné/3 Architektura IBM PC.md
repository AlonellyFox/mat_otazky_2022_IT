# 3. Architektura IBM-PC

> Historický přehled počítačů PC, form faktory. Hlavní komponenty, jejich vlastnosti a parametry. Sběrnice a čipové sady, BIOS. Adresy zařízení na sběrnici. Realizace operační paměti. Pevné disky (HDD a SSD).

---

## Historický přehled

### Nultá generace (1930 – 1940)

Elektromechanické počítače s reléovými obvody či manuálními přepínači.

Howard Aiken – Studoval a učil na Harvardu, pomohl sestrojit s IBM Harvard Mark I za pomocí jím vymyšlené harvardské
koncepce

[Wikipedia](https://en.wikipedia.org/wiki/Mechanical_computer#Electro-mechanical_computers)

### První generace (1945 – 1951)

Využívala elektronek, relé už jen zřídka. Počítače byly neefektivní, velmi drahé, vysoký příkon, velká poruchovost a
velmi nízkou výpočetní rychlost. Například jeden počítač z této generace, ENIAC (1946), spotřeboval 150 kW energie a
trpěl poruchou v elektronkách každé 2 dny, oprava trvala 15-20 minut.

V této době se také objevuje použití binární soustavy a von Neumannovy architektury.

[Wikipedia](https://en.wikipedia.org/wiki/Vacuum-tube_computer)

### Druhá generace (1951 – 1965)

*Poznámka: následující generace sdílí stejný odkaz
pro [Wikipedii](https://en.wikipedia.org/wiki/History_of_computing_hardware_(1960s%E2%80%93present))*

Používány tranzistory: zmenšení rozměrů, zvýšení rychlosti a spolehlivosti, snížení energetických nároků. V této
generaci jsou stále zmínky o používání decimální soustavy, ale ta je silně nahrazována binární.

Trhu počítačů v této době dominovalo IBM, za zmínku stojí i Bell labs, kde vznikl tranzistor (Bardeen, Brattain a
Shockley).

### Třetí generace (1965 – 1980)

Integrované obvody, postupem času roste počet tranzistorů v jednom obvodu (zlepšuje se integrace). Multitasking proces (
vykonávané programy se střídají).

Mezi první počítače z této doby patří třeba Apollo Guidance Computer, který řídil první Apollo misi.

### Čtvrtá generace (od 1981)

Charakteristická mikroprocesory a osobními počítači. Mikroprocesory v jednom pouzdře obsahují celé CPU (dřívější
procesory se skládaly z více obvodů) a jsou integrované s vysokou integrací, které umožnily snížit počet obvodů na
základní desce, zvýšila se spolehlivost, zmenšily rozměry, zvýšila se rychlost a kapacita pamětí. Objevuje se také paměť
RAM vytvořena z polovodičů. S rozvojem počítačů sítí vzniká internet. VLSI = miliony tranzistorů

### Přehled technologií použitých v PC

[Timeline](https://en.wikipedia.org/wiki/Timeline_of_computing)

- **1981** – první IBM PC – 8088 @ 4.55Mhz, až 64MB RAM, záznam na 5“ disketu
- **1987** – IBM PS/2 – VGA, 80386, záznam na 3,5“ disketu, PS/2 rozhraní a SIMM (paměť)
- **90‘s** – CD-ROM, Pentium, 1024x768, zvukové karty a modem, inkoustové tiskárny
- **2000‘s** – USB, Ethernet, Wi-Fi, bluetooth, PCIe, DVD, SATA
- **2010‘s** – SSD

## Form faktory

Definice rozměrů a potřeb napájení počítače. Pro PC existují dva základní form faktory: AT a ATX

Zdroje typu ATX – jiný způsob zapínání/vypínání. Zdroj není spojen přímo se zapínacím tlačítkem. To umožňuje zapínání
počítače i jinými způsoby (Wake on LAN, Wake on RING, klávesnicí nebo myší). Přesto má mnoho napájecích zdrojů ATX na
své zadní straně klasický vypínač. Tím se počítač skutečně vypne a softwarové zapnutí pak není možné. Pokud je tento
vypínač zapnutý, PC stále spotřebovává energii, i když vypadá jako vypnutý.

### AT

Nahradil XT. Od 286 do PenII. Napájecí zdroj měl 2x šesti pinové konektory. Zapojovaly se do jednoho 12pin konektoru
ČERNOU k sobě! Počítače se zapínaly přímo na zdroji a fyzické tlačítko určovalo, zda je počítač zapnutý, nebo ne.
Jediným I/O je klávesnice.

### ATX

Od Pentium II až do současné doby, zdroj má 24pin (mívaly jen 20). Počítače se zapínají tak, že se pin PS-ON spojí se
zemí
(tohle většinou dělá základní deska). Díky trvalému příkonu +5V se dají počítače zapnout i jinými způsoby, jako Wake on
LAN, klávesnicí nebo myší. Na rozdíl od AT mají počítače větší I/O.

### Koncepce PC

*Poznámka: dle zadání tato sekce se nezdá být důležitá, nicméně je potřeba ji znát podle učitelů...*

- John von Neumannovo schéma – používá 1 elektronickou paměť pro program i pro data
- Harvardská architektura – používá oddělenou paměť pro data a pro program

Současné PC nejsou konstruovány ani podle jedné architektury. Univerzální PC obsahují jen 1 paměť, do které se umísťují
programy i zpracovávaná data, avšak procesor umožňuje paměť obsahující program označit jen pro čtení, a naopak část
paměti, která obsahuje data označit tak, že nelze vykonávat strojové instrukce, které jsou v ní uloženy.

## Hlavní komponenty PC

### CPU

Central Processing Unit, procesor – vykonává instrukce

Procesor základní součást počítače, která vykonává strojový kód spuštěného počítačového programu. Ten je složen z
jednotlivých strojových instrukcí, které jsou uloženy v operační paměti počítače. Procesor je v současnosti velmi
složitý sekvenční integrovaný obvod umístěný na základní desce počítače.

Frekvence, počet jader a vláken, počet PCIe linek, potřeba

### GPU

Graphics Processing Unit – specializovaný mikroprocesor pro grafické výpočty určený k zobrazování obrazu na displeji.
Zpracovávají instrukce grafické API, jako je třeba Vulkan, OpenGL, OpenCL, DirectX atd.

Frekvence, počet grafických jader, grafická paměť, spotřeba

### RAM

Random Access Memory – rychlá paměť, kterou lze jakkoliv a kdekoliv číst a používá se k ukládání dat a zdrojového kódu,
používá se na dočasné uložení dat a při ztrátě napájení se vymaže.

Frekvence, typ (DDR4, DDR5, SRAM,...), kapacita

#### Realizace RAM

Fyzický paměťový prostor se jeví jako souvislý prostor buněk. Tyto buňky jsou pak lineárně adresovány.

SRAM – Statická RAM

DRAM – Dynamická

DDR – Double data rate

Ecc – error correction code – kontrola bloku dat paritním bitem přímo v RAM modulu

### Zdroj

PSU – Power Supply Unit – mění střídavé napětí na napětí použité počítačem

Slouží ke zpracování střídavého napětí dodávaného ze sítě na nízké napětí potřebné napájení komponent počítače. Některé
zdroje mají přepínač pro změnu vstupního napětí mezi 230 V a 115 V, valná většina v dnešní době se ale automaticky
přizpůsobí jakémukoli napětí v tomto rozsahu. Nejčastěji dodávané počítačové zdroje spadají do standardu ATX. Ve
stejnosměrném napětí vrací +3, +5, +12 a -12 V.

Výkon, form faktor

### Základní deska

Motherboard – deska jenž propojuje všechny periferie mezi sebou

Obsahuje většinu elektronických částí počítače. Hlavním účelem základní desky je propojit jednotlivé součástky počítače
do fungujícího celku a poskytnout jim elektrické napájení. Typická základní deska umožňuje zapojení procesoru, operační
paměti. Další komponenty (například grafické a zvukové karty, pevné disky, mechaniky) se připojují pomocí rozšiřujících
slotů nebo kabelů, které se zastrkávají do příslušných konektorů. Některé komponenty jsou v současné době integrované
přímo v deskách, třeba zvuková karta, Wi-Fi karta atd.

Základní desky obsahují také North Bridge (dnes integrovaný v CPU, propojený přes **F**ront **S**ide **B**us) a South
Bridge. Zde na obrázku je zobrazeno, co který můstek dělá:

![Ukázka propojení NB a SB](https://upload.wikimedia.org/wikipedia/commons/5/51/Chipset_schematic.svg)

#### BIOS

Basic Input/Output System (BIOS) se nachází v ROM paměti na základní desce.

BIOS provádí Power on Self Test (POST):

1. kontrola prvních 64Kib paměti
2. Kontrola řadičů, čipové sady
3. Vyhledávání dalších BIOSů
4. Předá kontrolu jiným BIOSům
5. Zjištění kapacity RAM
6. Vyhledávání úložišť
7. Předání kontroly OS

CMOS paměť – baterka (většinou [CR2032](https://en.wikipedia.org/wiki/Button_cell)) v PC – drží nastavení BIOSu a drží
také čas a datum Funkcí BIOSu je řízení celého systému – zajišťuje komunikaci jednotlivých komponent počítače (hardwaru)
s čipovou sadou základní desky a operačním systémem (OS) –
**propojuje hardware se softwarem**.

BIOS nabízí nejenom změny pro urychlení chodu počítače, tedy zvýšení výkonu PC. Pro nastavování, změnu a ukládaní údajů
systému BIOS slouží program setup. Do setup se dá většinou vstoupit přes zmáčknutí klávesy několik sekund po provedení
POST.

V dnešní době byl BIOS nahrazen UEFI, které hlavně změnilo způsob bootování systému. Funkce UEFI je jinak stejná jako
funkce BIOSu, také provádí POST, zajišťuje komunikaci mezi software a hardware atd. Partition table disků také přešel z
MBR na GPT, čili disky v těchto systémech mohou mít větší kapacitu boot partition a také mohou mít více jak 4 partitions
bez použití extended partition. MBR disky jsou limitované tedy jen na 4 oddíly.

#### Čipové sady (chipset)

Chipset je v dnešní době víceméně jen south bridge. Původně se jednalo o
kombinaci [south a north bridge](#základní-deska).

### Úložiště

Slouží k trvalému ukládání dat.

#### HDD – Hard Disk Drive

Je magnetický disk. Ukládá magneticky na plotny, které adresuje na cylindr, hlavu a sektor. Je velmi náchylný na
vibrace, v případě nutnosti a při vypnutí zaparkuje čtecí hlavu. S příchodem větších kapacit se přešlo na LBA (Logic
Block Addressing), což je spojení do clusterů (několik sektorů dohromady).

#### SSD - Solid State Disk

SSD postupem času nahradily pevné disky a umožnily řadu nových aplikací, jako digitální fotoaparáty a kamery, mobilní
telefony, GPS a podobně, často ve tvaru paměťových karet a flash úložiště. Používají stejné rozhraní SATA, pro vyšší
přenosové rychlosti PCI-Express (M.2).

```diff
Výhody SSD (oproti HDD):
+ SSD nemají mechanické pohyblivé části
+ mají rychlejší přístup k datům
+ dosahují vyšších přenosových rychlostí
+ nevydávají hluk
+ jsou mnohem menší a lehčí
+ spotřebují mnohem méně energie
+ fragmentace dat na disku není zde problémem
+ SSD přežijou více tepla než hard disky, mohou také operovat v teplotách pod nulou
+ SSD mohou fungovat ve výškách nad 3000 m. n. m.

Nevýhody SSD:
- poškozují se zápisem do buněk (controller na SSD se snaží zamezit zápisu do stejných buněk)
- SSD používají DRAM cache a při náhlém výpadku energie může dojít ke ztrátě dat
```

##### Buňky SSD

Víceúrovňová buňka je v elektronice paměťový prvek schopný ukládat více než jeden bit informace, ve srovnání s
jednoúrovňovou buňkou (SLC), která může uložit pouze jeden bit v paměťovém prvku. Trojúrovňové buňky (TLC) a
čtyřúrovňové buňky (QLC) jsou verzí MLC paměti. Jedna buňka se typicky skládá z jednoho MOSFET tranzistoru, čili použití
MLC buněk snižuje jejich počet.

Hierarchie pamětí je setříděna následovně:

* SLC (1 bit v buňce) – nejrychlejší, nejvyšší cena, největší životnost MLC (2 bity v buňce)
* TLC (3 bity v buňce)
* QLC (4 bity v buňce) – nejpomalejší, nejlevnější, největší životnost

### Skříň

Místo pro uložení komponentů. Stará se o airflow, přední I/O a některé mají i filtry proti prachu. Case se vždy vybírá a
dělá tak, aby vyhovovala podmínkám a požadavkům uživatele.

## Sběrnice

Sběrnice slouží ke připojení komponentů a přídavných karet.

### ISA

Používala se během 80. let 20. století. Jedná se o paralelní sběrnici, která byla původně 8 bitová, později 16 bitová.
Byly i pokusy o 32 bitovou verzi (EISA). Původně byla frekvence sběrnice určena podle frekvence procesoru, což
způsobovalo problémy mezi počítači s jinými než podporovanými frekvencemi. Později byla standardní frekvence stanovena
na 4, 6 a 8 MHz.

Rychlost je 16 MB/s pro full-duplex, poloviční pro half-duplex.

### PCI

Paralelní 64 bitová sběrnice s podporou pro 32 bitové karty. Frekvence je mezi 33 až 66 Mhz, rychlost mezi 133 MB/s a
533 MB/s pro half-duplex, obojí závislé na použité frekvenci a počtu bitů. Výchozí stav byl 33 MHz a 133 MB/s na 32 bit.

Karty na sběrnici mohou podporovat Plug&Play, čili počítač je může automaticky detekovat a nainstalovat potřebné
ovladače. Podporuje také bus mastering pro všechny karty, čili karty mají možnost přímého přístupu do paměti.

### PCI-e

Sériová sběrnice, kde komunikace je rozdělena na linky, každé zařízení může mít od jedné do osmi linek. Rychlost linky
se mění verze od verze, zde jsou rychlosti jedné linky obou směrech:

* 1.0 - 250 MB/s
* 3.0 - 985 MB/s, nachází se ve valné většině dnešních domácích počítačů
* 4.0 - 1.97 GB/s, začíná se objevovat v domácích počítačích
* 5.0 - 3.94 GB/s, standardní ve serverech
* 6.0 - 7.56 GB/s, specifikace schválena v lednu 2022

Standardní počet linek je x1, x2, x4, x8 a x16, pro výpočet rychlost x16 linky vynásobíme x1 linku 16. Příklad: rychlost
16 linek PCIe 5.0 je 16 * 3.94 = 63 GB/s.

Vznikla v roce 2003.

```
Editace: Roman Táborský

Autor: Roman Skalík
Merger: Sádlík Kryštof
Datum: 7.5.2020
```
