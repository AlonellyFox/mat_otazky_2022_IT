## 1 - Základy informatiky

### Číselné soustavy

Dopsat
- [ ] bin, dec, hex jsou polyadické čís. soustavy
- [ ] upozornit, že je třeba umět zpaměti 2^0 - 2^10
- [ ] dopsat převod
- [ ] umět odhadnout maximální hodnotu na počet bitů
- [ ] co je to kapacita

---

<!---
velmi velmi raw verze toho, co říkal hapl v BIS, pokud není něco z tohohle dopsáno, tak by se to tam mohlo přihodit

otázka č.1 --------------------------------------------------------------

Hex využití

IPv6
Adresace paměti, čtení paměti
Mac adresa

Dec vs bin
Vyuziti v pocitacich jestli napeti je, nebo neni. (vetsinou kdyz je napeti tak 1, neni napeti 0)



Data mohou přinášet informace
Medium přenáší informace

Data mohou byt i neporozumene hodnoty, pokud jsou data porozumeny, tak se stavaji informaci

Kapacita je maximalni mnozstvi ulozenych dat

Přímý kod

Záporne (-)  ->      1 | 1010
Kladne.  (+) ->      0 | 1010


Napr zpusob dopravy

1011

1.bit = 0, autem nelze
            1, autem lze

2.bit = 0, vlakem nelze
            1, vlakem lze

3.bit = 0, letadlem nelze
            1, letadlem lze

X.bit = 0,xxx nelze
             1,xxx lze


Tldr: bity nemusí znamenat jen čísla, mohou být také stavy, či možnosti


V CMOS pameti nalezneme 01011001
8b dat

01011001 = 89s ale 89s neni mozne v minute

Propustnost
- schopnost media prenest urcity objem dat (maximalni) 
Napr.
Ethernet - 10Mbit/s
FastEthernet - 100Mbit/s

Sběrnice - SATA 3 - 6Gbit/s


Typy prenosu dat

Paralelní
Seriovy

Seriovy je preferovany, kvuli frekvencim

Takt a frekvence

Takt je hodinova a rizena frekvence

Frekvence je frekvence lol

otázka č.6 --------------------------------------------------------------

Co to je Os

Rozhrani umoznujici interfacovani mezi uzivatelem a hardwarem

Rozdeluje se na shell a jadro

Jadro
Rozdeleni
Monoliticke - pouzivane Linuxem
Jadro musi mit veskere drivery nactene v jadru, a dalsi drivery musi byt pridany, a kompilovany primo s jadrem

Mikrojadro - pouzivane Microsoft
Oddelene vrstvy, jadra a ovladace


Typy - 
Jednouzivatelsky
DOS

Viceuzivatelsky
Windows, linux

---
Jednoulohovy 
DOS

Viceulohovy
Win/Linux

--
Multitasking

Preemptivni
Win98 - 11

Presne vyhrazeny cas, pomoci dispeceru, a OS po danem casu vzdy prerazene prostredky


Cooperativni
Win3.1
Win95

Kazda aplikace zodpovedna za prirazeni  rizeni jine aplikace


Shell muze byt terminalovy, nebo graficky, nebo oboji

Evidence procesu

Co je to proces

Kde se bere
Proces vznika z aplikace na disku
(BEZICI) proces - je v RAM
(nebezici) proces - muze byt na disku

Kdo se o ne stara
Cast jadra (dispatcher) 
Prideluje aplikacim ID a prideluje aplikacim prostredky (pamet, procesor, čas)


sorry for shit spelling, byl jsem rád že jsem ho chápal a stíhal zapisovat na phone ok dik cs
-->

---

# 15P
Haplova prezentace by měla stačit

40 pinů - 20 programovatelných
3.3V logická 1
Bluetooth, Wifi
DDR2 RAM 1GB

Bootování z microSD

Srovnání s PC - vše přes USB (pomalé), GPIO
Na Rpi 4 běží i Win10, na 3 ani XP

Číslování pinů BCM / Board

Přísné na napájení - snadno se rozbijí

Instalace OS - flashnutí SD karty, karta do raspberry, instalace...

Pull up down, nastaveni vstupů / výstupů

Umět popsat kód, který dostaneme u maturity. Jestli tam je nastavení vstupů / výstupů, BCM / Board