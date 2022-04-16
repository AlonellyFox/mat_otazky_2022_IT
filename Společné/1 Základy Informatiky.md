# 1. Základy informatiky

> Číselné soustavy (dvojková, desítková, šestnáctková), jednotky používané v informatice, data a informace,
kapacita, přímý kód, zakódování informace (po bitech, po skupině bitů), propustnost, typy přenosů dat, takt a
frekvence.

---

## Číselné soustavy

Používají se následující **polyadické** číselné soustavy:

* Dvojková (binární)
* Osmičková (oktalová) - není nutné umět jak se používá a převádí
* Desítková (decimální)
* Šestnáctková (hexadecimální)

První počítače byli na bázi desítkové soustavy, s příchodem Von Neumanna se začala používat binární

### Dvojková

Nabývá hodnot 0 a 1. Používaná v informatice z důvodu lehce rozdělitelným stavům.

* S binární soustavou souvisí Booleova algebra (1/0, true/false)
* Zápor se vyjadřuje dvojkovým doplňkem (tento doplněk vyžaduje bit navíc)
* Pro získaní počtu hodnot v dec je potřeba odečíst číslo, protože i nula se bere jako kladná hodnota. Například počet
  hodnot pro 8 bitů je 2<sup>8</sup> - 1 = 255, používá se pro to [Přímý kód](#přímý-kód)

Ukázka převodu:

| Binární | Decimální |
|---------|-----------|
| 0000    | 0         |
| 0001    | 1         |
| 0010    | 2         |

### Šestnáctková

Nabývá hodnot 0-9 a A-F. Používá se v informatice, kvůli zpříjemnění čtení pro programátory.

| Hexadecimální | Decimální |
|---------------|-----------|
| 0-9           | 0-9       |
| A-F           | 10-15     |

`0x10 = 16(dec)`

### Ruční převod mezi soustavami

Prý že se u této otázky mohou někteří ptát, jak ručně převádět jednotky...

#### Binární -> decimální

Každé číslo dvojkové soustavy lze zapsat pomocí exponentu dvou a tento exponent se postupně zvyšuje pro každou pozici.
Následující tabulka uvádí příklad exponentů pro 4bitové číslo:

|                             |               |               |               |               |
|-----------------------------|:-------------:|:-------------:|:-------------:|:-------------:|
| **Decimální číslo**         |       8       |       4       |       2       |       1       |
| **Dvojkový exponent**       | 2<sup>3</sup> | 2<sup>2</sup> | 2<sup>1</sup> | 2<sup>0</sup> |
| **Pozice v binárním čísle** |       4       |       3       |       2       |       1       |

Na základě této tabulky jsme schopni převést binární číslo `1011`. U každé pozice, kde hodnota je `1`, si zapíšeme
decimální hodnoty dvojkových exponentů a ty pak následně sečteme. Pozice, kde hodnota je `0`, ignorujeme.

|                     |               |                   |               |               |
|---------------------|:-------------:|:-----------------:|:-------------:|:-------------:|
| **Decimální čísla** |       8       |         0         |       2       |       1       |
| **Výpočet**         | 2<sup>3</sup> | 2<sup>2</sup> * 0 | 2<sup>1</sup> | 2<sup>0</sup> |
| **Binární číslo**   |       1       |         0         |       1       |       1       |

8 + 0 + 2 + 1 = **11**\
Převod čísla `1011` bin do dec je `11`.

#### Decimální -> binární

Spočívá v dělení dvěma a zapisováním zbytku dělení, dokud nebude výsledkem nula. Poté obrátíme zapisovaný zbytek.

|                   |        |       |       |       |
|-------------------|:------:|:-----:|:-----:|:-----:|
| **Výpočet**       | 11 / 2 | 5 / 2 | 2 / 2 | 1 / 0 |
| **Výsledek**      |   5    |   2   |   1   |   0   |
| **Zbytek dělení** |   1    |   1   |   0   |   1   |

Zbytek dělení obrácen: `1011`

#### Hexadecimální

Hexadecimální čísla mají dvě možné situace a dva možné způsoby převodu.

##### Jednomístné čísla

V případě jednoduchých, jednomístných hex čísel (třeba A, F, 5, 6) se stačí řídit podle tabulky v kapitole o
[hex soustavě](#šestnáctková).

##### Vícemístná čísla

Každé hex číslo se dá rozdělit do 4 binárních čísel, jako ukazuje následující tabulka:

| hex | bin  |
|:---:|:----:|
|  F  | 1111 |
|  A  | 1010 |
|  8  | 1000 |

Čili, pokud převádíme číslo `FA8` do binárního formátu, vznikne nám `1111 1010 1000`. Tohle číslo pak můžeme převést,
pokud třeba, do desítkového formátu.

## Jednotky používané v informatice

Kilo je 1 000, mega je 1 000 000, giga 1 000 000 000, atd.

* **1 bit** – základní jednotka informace - **1** nebo **0**
* **1 B** (byte) = **8 bitů** (256 hodnot)
* **1 kB** (kilobyte) = **1000 b**
* **1 kiB** (kibibyte) = 2<sup>10</sup> B = **1024 B**
* **1 MiB** (mebibyte) = 2<sup>20</sup> B = **1 048 576 B**
* **Word** = **2 B**
* **Nibble** = **4 b**, polovina Byte

Jednotka *kibi* je víceméně stejná jako *kilo*, akorát je v binární podobě. To platí i u dalších prefixů.

## Data a informace

### Informace

Informaci lze definovat jako zmenšení neurčitosti jevu. Je dekódovaná a lze ji vysílat, přijímat, uchovávat, kódovat,
zpracovávat a vyjadřuje nějakou hodnotu. Informace, které zpracovává počítač jsou (prozatím) několika druhů:

*textové informace (texty, programy...)
*obrazové informace (fotografie, grafiky, video, animace...)
*zvukové informace (zvuky, hudba...)

U informací posuzujeme jejich:

*aktuálnost
*relevanci - adekvátnost potřebě. Informace je relevantní, je-li v ní obsaženo to, co potřebujeme vědět.
*pravdivost - soulad se skutečností

### Data

Data jsou nekódované informace.

### Signál

Signál je nositel informace (dat).

### Kapacita

Kolik dat (paměťové) médium pojme.

## Přímý kód

První možný způsob jak vyjádřit záporné číslo - vyčlenění prvního bitu jako znaménkového bitu. Pokud například binární
číslo 00000001 vyjadřuje jedničku, pak 10000001 označuje −1.

Tento způsob ale komplikuje algoritmy pro praktické počítání – pro sčítání a odčítání jsou potřeba odlišné algoritmy a
nejprve je vždy třeba testovat znaménkový bit a podle výsledku provést sčítání nebo odčítání. Další nevýhodou je, že
existují dvě reprezentace čísla nula – kladná nula a záporná nula. Proto byl později pro záznam záporných čísel zaveden
doplňkový kód.

*Zbytkový text z poznámek:*

> * v doplňku pro 4 bity od -8,7 (8 a 8 hodnot) musíme získat 16 hodnot
> * dvojkový doplněk získám negací \+ 1
> * jak vyjádřit čísla se znaménkem (dvojkový doplněk)

## Zakódování informace v informatice

Veškeré informace uloženy v souborech, kódovány pomocí číslic 0 a 1. Soubory s informací kódovanou známým způsobem jsou
opatřeny známou příponou a zpracovávány programy, které toto kódování znají.

Známý způsob kódování je base64. Jakýkoliv tok binárních informací lze zakódovat a poté následně kýmkoliv dekódovat přes
base64.

## Propustnost

Je veličina, která říká, jaké množství dat je možné přenést za jednotku času. V toto číslo se může reálně měnit. Udává
se v bitech či bytech za sekundu.

## Typy přenosů dat

### Analogový a digitální přenos

Analogový přenos je přenos spojitého proměnného signálu, digitální komunikace je přenos diskrétních zpráv. Tyto
digitální zprávy jsou buďto reprezentovány sledem impulsů prostřednictvím linkového kódu
(základní pásmo) nebo omezeným počtem lineárních průběhů (přeložené pásmo), a to za použití digitální modulace. Modulace
a demodulace se provádí pomocí modemu. Jiná alternativní definice považuje pouze signál v základním pásmu jako digitální
a přenos přeloženého pásma digitálních dat jako formu digitálně-analogového převodu. Přenášená data mohou být digitální
zprávy pocházející z datového zdroje, jako například počítač nebo klávesnice, ale také analogový signál, jako telefonní
hovor nebo video signál, digitalizovaný do bitového proudu.

Digitální přenos nebo přenos dat tradičně patří do oblasti telekomunikací a elektrotechniky. Základní principy přenosu
dat jsou pokryty v oboru datové komunikace. To zahrnuje také počítačové sítě, počítačové komunikační aplikace a síťové
protokoly, například směrování a meziprocesovou komunikaci.

Následující obrázek zobrazuje digitální signál žlutě a analogový modře:

![Ukázka rozdílu mezi analogovým a digitálním přenosem](images/analogový%20a%20digitální%20signál%20-%20light.png#gh-light-mode-only)
![Ukázka rozdílu mezi analogovým a digitálním přenosem](images/analogový%20a%20digitální%20signál%20-%20dark.png#gh-dark-mode-only)

### Sériový a paralelní přenos

V telekomunikacích je sériový přenos sekvenční přenos signálu, zastupující znaky nebo jiný druh dat.

Digitální sériové přenosy jsou realizovány jako bity posílané jeden za druhým přes jeden vodič nebo sekvenčně optickou
cestou. Vzhledem k tomu, že tento způsob nevyžaduje tolik práce se signálem (a existuje menší riziko chyby než u
paralelního přenosu), může být přenosová rychlost po každé jednotlivé cestě větší. To se dá s výhodou použít na delší
vzdálenosti pro kontrolní součet nebo paritní bit.

Paralelní přenos znamená současný přenos signálního prvku znaků nebo jiného druhu údajů. V digitální komunikaci používá
paralelní přenos dva nebo více vodičů, což umožňuje vyšší rychlost přenosu dat, než jaké lze dosáhnout pomocí sériového
přenosu. Tato metoda se v dnešní době používá zejména pouze při komunikaci mezi CPU a RAM. Hlavním problémem je
„zkreslení“ (a přeslechy, to jest kdy signál přeskočí z jednoho vodiče na druhý), protože vodiče při paralelním přenosu
mají odlišné vlastnosti. Kvůli tomu mohou být některé bity přijaty dříve než ostatní, čili všechny vodiče musí být
přesně stejně dlouhé. K řešení tohoto problému se nabízí paritní bit, nicméně paralelní přenos na dlouhé vzdálenosti je
stále méně spolehlivý, protože narušení přenosu je mnohem pravděpodobnější.

## Takt a frekvence

Frekvence, neboli takt procesoru, je udáván v gigahertzech. Tedy udává, kolik cyklických dějů (výpočtů) se stane za
jednu sekundu.

```
Autor: Postaveno na základu Adama Kadlčíka a Kryštofa Sádlíka
Silně přepsáno a upraveno Romanem Táborským
Datum: 6.5.2020
```