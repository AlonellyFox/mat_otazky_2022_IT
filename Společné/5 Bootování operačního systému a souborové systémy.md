# 5. Bootování operačního systému a souborové systémy

Master Boot Record, boot sektor, fáze bootování operačního systému, geometrie pevných
disků, metody přístupu na disk, souborový systém FAT32, souborový systém NTFS, linuxové
souborové systémy (ext2, ext3)
---
## Master Boot Record - Hlavní spouštěcí záznam

- Nachází se v **prvním sektoru** pevného disku
- Identifikuje **umístění operačního systému**, aby mohl být **načten do RAM**
- Jeho velikost je **512 bajtů**
   - jedná se o nejmenší adresovatelnou velikost jednoho sektoru v OS Windows.
- Obsahuje tabulku s popisem rozdělení disku
  - což je první místo hned po BIOSu, kam se počítač dostane při svém startu.
- MBR dokáže adresovat **maximálně 2 TB disky**.
- MBR je vždy uložen na samém počátku disku a skládá se ze 2 hlavních částí.

### Master Partition Table - Hlavní tabulka diskových oddílů (MPT)

- Obsahuje informace o diskových oddílech a odkazy na další tabulky disk. oddílů
- Tabulka nemůže obsahovat více než **4** záznamy.
- Disk se dělí na **primární oddíly** (primary partition), jeden oddíl z nich může být
    označený jako **rozšířený oddíl** (extended partition) – v rožšířeném oddíle lze vytvořit
    „libovolný“ počet logických oddílů (omezený velikostí disku či možnostmi OS).

### Hlavní spouštěcí kód – kód zavaděče

- Kód, který je při spuštění PC zaveden BIOSem do paměti počítače.
- Jeho úkolem je načíst do paměti zaváděcí (boot) sektor z oddílu, ze kterého má být
    zaveden OS a spustit ho.


## Fáze bootování operačního systému

- **Bootování = spouštění operačního systému.**
- Bootování se skládá z následujících fází:
    - Diagnostika hardware
    - Kontrola paměti
    - Inicializace vestavěného BIOSu
    - Inicializace doplňkových součástí hardware a jejich BIOSů
    - Nabootování OS
### Boot manager

-    **Boot Manager** = jeho hlavní funkcí je možnost vybrání systému nebo jednotky, ze
    které bude bootování probíhat.

## Geometrie pevných disků
- Skládá se ze **stop** disku (tracks)
   - každá z těchto stop je rozdělena do **sektorů** (sectors)
   - množina všech stop na disku se označuje jako **válec** (cylinder)

### Hlavy disku (heads)

- **Počet čtecích** (zapisovacích) **hlav pevného disku**.
- Tento počet je shodný s počtem aktivních ploch, na které se provádí záznam.
- Většinou každý jednotlivý disk má dvě aktivní plochy a k nim příslušné čtecí
    (zapisovací) hlavy.

#### Stopy disku (tracks)

- **Počet stop na každé aktivní ploše disku**.
- Stopy disku bývají číslovány od nuly, přičemž číslo nula má vnější stopa disku.

#### Cylindry disku (cylinders)

- **Počet cylindrů pevného disku** (tento počet je shodný s počtem stop).
- Číslování cylindrů je shodné s číslováním stop.

#### Sektory disku (sectors)

- **Počet sektorů, na které je rozdělena každá stopa**.
- Sektory bývají číslovány **od jedničky**.
- U většiny pevných disků je počet sektorů na všech stopách stejný.

## Metody přístupu na disk

- **Cylindr-Hlava-Sektor**
   - starší metoda adresace disku pro přístup k datům
    - adresuje disk podle jeho geometrie
    - nevýhoda - **omezená kapacita**, software **musel** umět rozlišovat geometrie disku

- **LBA - Local Block Addressing**
    - novější metoda adresování disku 
    - **není potřeba znát** geometrii disku
    - možné adresovat **až 144 miliónů GB**

## Souborové systémy

### FAT32

- Přináší 32bitové adresy clusterů, kde číslo alokační jednotky využívá 28 bitů, takže
  není vhodný pro ukládání velkých souborů.
- Náchylný k chybám, nemá žurnálování.
- Jednoduchý na implementaci.
- Maximální velikost souboru 4GB.

### NTFS

- Zaveden ve Windows NT (Windows pro IBM PC).
- Obvykle menší clustery než u FAT32.
- Názvy souborů v UTF8.
- Podporuje šifrování.
- Problematická podpora mimo systém Windows.
- Problémy s fragmentací = nutná pravidelná defragmentace (ve Windows 7 se spouští
  automaticky).
- Upravený systém žurnálování (všechny zápisy na disk se zároveň zaznamenávají do
    speciálního souboru).

### ext2

- Linuxový souborový systém.
- Rozšíření původního systému ext.
- Implementovaný v Unixových systémech, standardní volba pro většinu linuxových
    distribucí.

### ext3

- Kompatibilní s ext2.
- Přidáno žurnálování.
- Chybí klasická defragmentace disku a transparentní komprese.
- Kontrola disku jen v režimu read-only.

### Žurnálování

- Vytváření libovolných podrobných **záznamů o prováděné činnosti** (logů).
    - Do žurnálu je zapsáno, co a kde se bude měnit.
    - Je provedena vlastní série změn.
    - Do žurnálu je zapsáno, že operace byla úspěšně dokončena.
    - Záznam v žurnálu je zrušen.
- Pokud dojde v kterémkoliv okamžiku k přerušení, je možné pomocí dat v žurnálu
    uvést systém souborů do konzistentního stavu.

```
Autor: Filip Valenta
Úprava: Radim Gospoš
Datum: 4.5.2022
```
