# 2. Procesory pro PC

## Charakteristika a parametry procesorů IBM-PC kompatibilní
|  | **Rok Výroby** | **Typ procesoru (v bitech)** |**Datová Sběrnice (v bitech)** | **Adresní Sběrnice (v bitech)** | **Počet Tranzistorů** |
| - | :-: | :-: | :-: | :-: | :-: |
| **i8086** | 1980 | 16 | 16 | 20 | 29 tisíc |
| **i80286** | 1981 | 16 | 16 | 24 | 130 tisíc |
| **i80386** | 1983 | 32 | 32 | 32 | 275 tisíc |
| **i80486** | 1989 | 32 | 32 | 32 | 1.2 milionů |
| **Pentium 1** | 1993 | 32 | 64 | 36 | 3.1 milionů |
| **Pentium Pro** | 1995 | 32 | 64 | 36 | 5.5 milionů |
| **Pentium 2** | 1997 | 32 | 64 | 36 | 7.2 milionů |
| **Pentium 3** | 1999 | 32 | 64 | 36 | 9.5 milionů |
| **Pentium 4** | 2000 | 32 | 64 | 36 | 125 milionů |


### i8086
- Zpětně kompatibilní s i8080
- První procesor s architekturou x86
- Umí adresovat až 2^20 (Toto se určuje podle adresní sběrnice) (1MiB) operační paměti

#### Adresovaní v reálném režimu
- Skladá se ze dvou 16b složek - segment, offset (zapisuje se jako segment : offset)
- Výsledná adresa vzejde tak, že se segment vynásobí 10 (16 decimálně) a přičte offset
```
Například A859 : 145C

1. Segment se vynásobí 10 hex (16 dec)
A859 * 10 = A8590

2. Výsledek se sečte s offsetem
A8590 + 145C = A99EC

3. Výsledek součtu je výsledná fyzická adresa
A99EC

```
### i286
- První setup BIOS
- Přišel s novým režimem (Chráněný režim)
- Realný režim
  - Plně kompatibilní s procesorem 8086
  - 20b adresa (může adresovat 1MiB operační paměti (2^20))
  - Tvoří se stejně jako u 8086

- Chraněný režim
  - Nový režim, nekompatibilní s 8086
  - Adresa se tvoří ze dvou 16b složek (selektor a offset) za pomoci tabulek 
  - Vysledná adresa je 24b (16MiB ram (2^24))

### i386
- ***První Multitasking***
- První Použítí cahce na základní desce
- Nový režim (Virtuální)
- Reálný - stejný jako 8086
- Chraněný režim
  - Výsledná adresa je 32b (4GiB RAM (2^32))
  - Je rozšířeny o strankovaní - Převádí to lineární adresu ve vzdálené paměti na fyzickou adresu. Všechny adresy nemusí ukazovat na fyzickou paměť, některé mohou být odswapovány na pevný disk (virtuální paměť)
- Virtuální režim
  - Funguje podobně jako 8086
  - Možnost virtualizovat 1Mib, může uložit kdekoli do 4GiB adresního prostoru a spustit v něm reálný mód


### i486
**Prakticky i80386, která má navíc interní cache a numerický koprocesor (FPU)**
- Později vznikly procesory i80486dx2 a i80486dx4 kdy číslo 2 a 4 udává tzv. násobič (kolikrát běží jádro procesoru rychleji, než sběrinice FSB (Front Side Bus))
- Existoval i procesor i80486sx oficiálně bez FPU, reálně byl FPU pouze spálený.


### Intel Pentium 1
- První superskalární procesor (2 Instrukční fronty (během jednoho taktu může dokončit až 2 instrukce))
- Zaveden Branch Target Buffer (Dynamické předvídání skoků) 
- 16KiB Cache paměť
  - 8 KiB na data
  - 8 KiB na insturkce
- U pozdějších verzí se snižuje napájecí napětí na 3,3V

### Pentium Pro
- Pro servery, výkonné pracovní stanice

##### Pentium MMX (Multi Media Extension) (1997)
- Rozšířeni instrukcní sady
- Pro multimediální výpočty
- Technologie SIMD (Simple Instruction Data), která umožňuje práci s více čísly najednou

### Pentium 2
- L2 Cache 256KB
- Levnější varianta - Intel Celeron původně bez L2, později se 128KB L2 Cache

### Pentium 3 
- Nové instrukční sady SSE

### Pentium 4 
- Dvaceti stupňový pipelining
- HyperThreading (Logicky se jádro tváří jako 2 jádra)

```
### Intel CORE

2006+, D-bus i A - bus 64b, frekvence až 4-5 GHz

- Core 2
  - duo - 2 jádra
  - quad - 4 jádra
  - menší taktovací frekvence

Core i
  - 64bit, více jádrové
  - i3 - 2 jádra, hyperthreading
  - i5 - 4 jádra
  - i7 - 4 jádra, hyperthreading
  - variabilní taktovaní jader
 
### AMD
- 386 - napájení 3,6V, pro notebooky
- 486
- K5 - proti Pentiu, vydaný se zpožděním, pomalý v FPU operacích, neuspěšný
- K6 - AMD koupilo firmu Next Gen která ho vyvinula, vykonný procesor
- K6-2 - rozšíření 3D Now!
- K7 - nová architektura, 3 FPU, prodávaný jako Athlon
- K8 - AMD Hammer / Athlon 64 / Opheron - pro servery
```

## Paměťový prostor, cache, módy činnosti

### Paměťový prostor
Dělí se na paměť uživatelskou, paměť systémovou, a paměť dat. Do uživatelské paměti se ukládá
uživatelský program. Tato paměť bývá typu EPROM (Eraseable Programmable Read-Only Memory) nebo EEPROM (Electrically Erasable Read-Only Memory) a mívá kapacitu řádově od
desítek kB až po jednotky MB. V systémové paměti je umístěn systémový
program. Tato paměť bývá rovněž typu EPROM. V paměti dat, která musí být typu RAM (RWM), jsou
umístěny uživateli dostupné uživatelské registry, zápisníkové registry (merkery, flagy), čítače, časovače
a většinou i vyrovnávací registry pro obrazy vstupů a výstupů. Počet těchto registrů výrazně ovlivňuje
možnosti programovatelného automatu. Adresovatelný prostor vymezený pro vstupy/výstupy omezuje
počet připojitelných periferních jednotek. Důležitým parametrem jsou i rozsahy čítačů a časovačů.

### Cache
Cache (též mezipaměť) je v informatice označení pro hardwarovou nebo softwarovou součást počítače,
která uchovává data a tím následující přístup k těmto datům může být rychlejší. Od vyrovnávací paměti
(bufferu) se cache liší tím, že může poskytovat data v ní uložená opakovaně (zatímco vyrovnávací
pamětí data pouze procházejí). Použití termínu cache a vyrovnávací paměť může být zaměňováno,
protože obě funkce mohou splývat.

Cache je tvořena (relativně) rychlou pamětí, která je však dražší. Proto má cache menší velikost, než
úložný prostor, ke kterému zrychluje přístup. Optimalizací úspěšného využití cache lze dosáhnout
vyššího výkonu zařízení. Hardwarovou cache najdeme v mikroprocesorech nebo pevných
discích. Cache může být softwarově vytvořena v operační paměti.


### Módy činnosti

#### Chráněný

##### Ochrana paměti

Chráněný režim přináší podporu ochrany paměti, která umožňuje přidělit běžícímu procesu určitý úsek
operační paměti a znemožnit, aby mohl zasahovat mimo tento vymezený prostor. Umožňuje tím zavést
multitasking (v paměti může být najednou více procesů).

##### Privilegovaný režim

Privilegovaný režim umožňuje zajistit, aby neprivilegované procesy nemohly měnit nastavení, která
byla provedena v privilegovaném režimu. Jádro operačního systému běží v privilegovaném režimu a
všechny ostatní procesy v neprivilegovaném. Tak jádro neztratí nad počítačem kontrolu a jen jádro
může procesům přidělovat a odebírat systémové prostředky, ukončovat je, vynucovat změnu kontextu,
rozhodovat o dostatečném oprávnění k provedení určité činnosti atd.

##### Virtualizace paměti

Dále chráněný režim přináší pokročilou správu operační paměti, která spočívá v podpoře virtuální
paměti pomocí stránkování, což usnadňuje provozování multitaskingu.

##### Virtualizace systému

Chráněný režim přináší také možnost virtualizace, takže uvnitř jednoho systému (hypervizor) lze
provozovat jiný systém (virtualizovaný), který bude mít dojem, že má počítač jen pro sebe (je však pod
kontrolou hypervizoru).

##### Zpětná kompatibilita

Procesory podporující chráněný režim zachovávají kvůli zpětné kompatibilitě i podporu staršího
reálného režimu. To umožnilo používat již existujícího software (jak aplikační software, tak i operační
systém DOS nebo starší Microsoft Windows).

Procesory rodiny x86 se dodnes z důvodu zpětné kompatibility spouštějí nejprve v reálném režimu a do
chráněného režimu musí být teprve přepnuty, což moderní operační systémy (Microsoft Windows,
Linux, macOS, ...) dělají při bootování hned po aktivaci jádra.

#### Reálný

Reálný mód neboli režim reálných adres (anglicky real mode, real address mode) je v informatice
základní režim mikroprocesorů z rodiny x86. Rozlišuje se až od řady Intel 80286, kdy byl uveden
chráněný režim, ale fakticky odpovídá jedinému pracovnímu režimu starších mikroprocesorů Intel
8086 a Intel 80186. To je také důvod, proč procesory z rodiny x86 (včetně nejmodernějších 64bitových
procesorů x86-64) dodnes z důvodu zpětné kompatibility začínají svůj běh právě v reálném módu a do
jiného režimu je musí explicitně přepnout jádro operačního systému.


Typickými vlastnostmi režimu reálných adres je segmentace paměti s 20bitovou adresací (tedy
nanejvýš 1 MiB přímo adresovatelné paměti) a neomezený přímý přístup do celé paměti i ke všem
perifériím. Nelze tedy zajistit spolehlivé fungování multitaskingu.

##### Adresace

Adresa je v režimu reálných adres určena dvěma registry: segmentovým a offsetovým. Fyzická adresa
je vypočítána jako součet hodnoty v segmentovém registru vynásobené 16 (tedy posunuté o 4 bity
doleva) a hodnoty v offsetovém registru.

Díky přenosu tak může být výsledkem až 21bitové číslo: šestnáctkově 0xFFFF0 + 0xFFFF =
0x10FFEF. Pro 21. bit bylo do standardu IBM PC zavedeno rozšíření, které umožňovalo 21. adresní bit
aktivovat řadičem klávesnice. Na procesorech Intel 80286 a novějších, které měly širší adresní sběrnici,
bylo toto chování emulováno softwarově. Adresy nad hranicí 1 MiB (přesněji do adresy 1 MiB + 64
KiB – 16 bajtů, tj. do adresy 1114095) byly označovány jako HMA (high memory area) a bylo do nich
možné umístit například část systému DOS a uvolnit tak místo v konvenční paměti.

##### Přepínání do reálného režimu

Záměrem firmy Intel při zavádění režimu chráněné virtuální paměti bylo, aby v tomto režimu v
budoucnu běžely všechny operační systémy i jejich programy. Tomu odpovídala i podpora přepínání
režimů: zatímco pro přepnutí z reálného režimu do chráněného dal Intel k disposici snadný postup,
druhým směrem žádný snadný způsob nepřipravil a na procesorech řady 80286 bylo jediným
způsobem resetovat procesor.

Protože režimy se podstatně liší a programy napsané pro jeden z nich je potřeba upravit, aby běžely v
druhém, bylo vzhledem k množství programů pro reálný režim zpočátku nereálné, aby se od jeho
používání zcela upustilo. Řešením bylo používat ono resetování procesoru, byť se jedná o poměrně
nezvyklou a časově náročnou operaci. Při resetování samotného procesoru totiž nedochází ke smazání
paměti a při správném ošetření tedy může operační systém přepnout tam i zpět bez následků.

## Přerušení, přímý přístup do paměti

### Přerušení

Přerušení (anglicky interrupt) je v informatice metoda pro asynchronní obsluhu událostí, kdy procesor
přeruší vykonávání sledu instrukcí, vykoná obsluhu přerušení, a pak pokračuje v předchozí činnosti.
Původně přerušení sloužilo k obsluze hardwarových zařízení, které tak signalizovaly potřebu obsloužit
(tj. odebrat z vyrovnávací paměti vstupně-výstupního zařízení data nebo do ní další data nakopírovat,
odtud označení vnější přerušení). Později byla přidána vnitřní přerušení, která vyvolává sám procesor,
který tak oznamuje chyby vzniklé při provádění strojových instrukcí a synchronní softwarová přerušení
vyvolávaná speciální strojovou instrukcí, která se obvykle používají pro vyvolání služeb operačního
systému.

- proces s vyšši prioritou si vyžádá přerušení, procesor nechá toho, co zrovna dělá a věnuje se prioritnímu procesu, jak ho dodělá, věnuje se tomu, který dělal předtím
- žádá se o čas procesoru
- generuje se IRQ (Interupt ReQuest) hardwarem počítače - generuje ho zařízení na sběrnici


### DMA – Přímý přítup do paměti

DMA (anglicky Direct Memory Access, tj. přímý přístup do paměti) je v informatice způsob přímého
přenosu dat mezi operační pamětí a vstupně/výstupními zařízeními. Data neprocházejí skrze procesor a
lze tak dosáhnout vyššího výkonu (během přenosu dat může procesor zpracovávat jiné strojové
instrukce). DMA se používá pro přenos větších objemů dat například řadič pevných disků, grafická
karta, síťová karta, zvuková karta a podobně. DMA je odchylkou od Von Neumannovy architektury
počítače.

#### Princip

Klasická komunikace se vstupně-výstupními zařízeními je realizována pomocí strojových instrukcí IN
(přenáší data ze zařízení do registru procesoru) a OUT (přenáší data z registru procesoru do zařízení),
které tato data (typicky slovo procesoru) přenášejí po datové sběrnici, a adresní sběrnice přitom slouží
k adresaci vstupně-výstupního zařízení (tzv.PIO přenosy). Z hlediska procesoru jsou vstupně-výstupní
zařízení velmi pomalá a procesor musí na reakci zařízení čekat, což velmi zpomaluje výpočetní
rychlost počítače.

DMA je řízené speciálním řadičem, který je součástí základní desky počítače. Přenášení velkých
objemů dat mezi vstupně-výstupními zařízeními a operační pamětí je pak řízeno DMA řadičem a
procesor je brzděn těmito přenosy jen částečně (při blokování sběrnice konfliktem přístupů do paměti)
a může vykonávat jinou činnost. Počítač tak má z hlediska uživatele větší výkon díky paralelizaci
(současnému vykonávání) přenosů dat a činnosti procesoru. Program nejprve řadič DMA naprogramuje
(pomocí několika instrukcí IN a OUT) a o další přenosy se již nemusí programátor starat. Dokončení
přenosu může být signalizováno přerušením, které aktivuje obsluhu přerušení, která může
naprogramovat řadič DMA na další přenosy.

## Zpracování instrukcí

### Jednoduché

Jedná se o následující stupně:

1.Instruction fetch – vyzvednutí instrukce
2.Decode – dekódování instrukce, zároveň se načítají registry
3.Execute – provedení instrukce
4.Access – čtení z paměti
5.Writeback – zápis výsledku do paměti

> 0) programový vstup pro zpracovaní
> 1) radic žádá vstupní zařízení o hodnoty
> 2) vstupni zarizeni prenese hodnoty do operacni pameti
> 3) řadič je informován o načtení dat
> 4) řadič žádá o přenos dat (instrukce) do ALU nebo do výstupního zařízení
> 5) odeslání dat z paměti do ALU nebo do výstupního zařízení
> 6) žádost o provedení instrukce v ALU nebo ve výstupním zařízení
> 7) uložení výsledku operace do operační paměti
> 8) ALU informuje řadič o doručení instrukce
> 9) předání výsledku výpočtu

### Zřetězené

Pipelining, zřetězené zpracování či překrývání strojových instrukcí je způsob zvýšení výkonu
procesoru současným prováděním různých částí několika strojových instrukcí. Základní myšlenkou je
rozdělení zpracování jedné instrukce mezi různé části procesoru a tím i umožnění zpracovávat více
instrukcí najednou.

![Ukázka pipeliningu na obrázku](https://user-images.githubusercontent.com/89984430/163674692-ea01eeb8-df78-44d9-acba-818889f29f0a.png)

Řekněme, že máme model, kdy počítač používá **3** základní moduly při zpracování instrukce: ***fetch, decode, execute,*** tedy 3 moduly. Pokud bychom měli vykonat 4 takovéto cykly, zabralo by nám to 12 taktů

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| - | - | - | - | - | - | - | - | - | - | - | - |
| F | D | E | F | D | E | F | D | E | F | D | E |

Pokud se zamyslíme, uvědomíme si, že každý modul je 2 ze 3 taktů nevyužit. Pokud bychom tedy zpracovávali instrukce „paralelně“, namísto za sebou, určitě bychom dosáhli zrychlení.

| 1 | 2 | 3 | 4 | 5 | 6 | 
| - | - | - | - | - | - | 
| F | D | E |  |  |  |
|  | F | D | E |  |  |
|  |  | F | D | E |  |
|  |  |  | F | D | E |

Jak je vidět, stejné operace jsou nyní dvojnásobně rychlejší (místo 12 taktů pouze 6)

## Jednotky Procesoru

ALU (Arithmetic Logic Unit), FPU (Floating-Point Unit), Řadič – zajišťuje součinnost jednotlivých součástí procesoru , Vektorová jednotka –
matematický koprocesor, registry

## HyperThreading

Hyper-threading (oficiálně Hyper-Threading Technology, též HT Technology, HTT, HT) je v
informatice technologie používaná výrobcem procesorů Intel pro zjednodušené zajištění
vícevláknového paralelního zpracování strojových instrukcí. Technologie vytváří z jednoho
fyzického procesoru dva virtuální procesory tím, že jsou v něm aktivovány dvě řídicí jednotky.
Vůči softwaru systém představuje místo jednoho fyzického dva (logické) procesory. Hyper-
threading umožňuje lépe využít hardware procesoru, snížit odezvu systému (latenci), zrychlit
výpočty (systém s aktivovaným hyper-threadingem je podle typu výpočtů zhruba stejně rychlý
nebo až o třetinu rychlejší).

Rychle přepíná mezi dvěma sadami registrů.

## Možnosti zvětšování výkonu procesoru

- HyperThreading - Viz. předchozí téma
- Superskalarita – některé jednotky jsou v procesoru víckrát
- Přetaktování - Zvýšení taktů procesoru
- Rozšíření šířky slova – 32bit, 64bit
- Zefektivnění mikrokódu
- Predikce skoků – jakési předvídání skoků. Základem je myšlenka, že skoky jsou většinou 	ve smyčkách a reagují na nějakou podmínku, která 10x vyjde a 1x nevyjde.
- Pipelining - zpracování 2 instrukcí najednou
- Přidání víc jader
  - na určité operace jsou vyhrazené a duplikované specializované části procesoru - FPU, ALU
  - instrukce nejdou zpracovávat paralelně - musí se počkat na dokončení rozpracované instrukce
- Velikost procesorové cache - propojuje procesor s RAM

```
Autor: Jiří Jungwirth
Merger: Sádlík Kryštof
Datum: 7.5.2020
```
