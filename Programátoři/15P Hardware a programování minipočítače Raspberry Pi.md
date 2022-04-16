# 15P. Hardware a programování minipočítače Raspberry Pi

> Architektura ARM-A, popis parametrů a možností – porovnání s PC, rozhraní GPIO a jeho popis. Výběr a instalace
OS, konfigurace. Využití jazyka Python k programování na RPi3. Připojení periferií k RPi3, RPi.GPIO. Princip
programování statických výstupních periferií (řada LED, 7Segm) a dynamických periferií (3x7Segm, reproduktor),
vstupní periferie.

---

## Architektura ARM

- 32/64 bitová mikroprocesorová architektura typu RISC
- Oproti x86 má menší spotřebu energie a produkuje tedy méně tepla
- Používá se v mobilních zařízeních (notebooky, mobily, tablety, atd.)

## Popis parametrů a porovnání s PC

Nejnovější RPi 4

- 64bit čtyřjádrový procesor Broadcom BCM o taktu 1,5 GHz
- RAM 8 GiB (nejvyšší model)
- Napájení USB-C (dříve micro-USB) - 5V
- Dva micro-HDMI porty (s podporou rozlišení 4K, dříve jen jeden HDMI port)
- 4x USB (2x USB 3.0, 2x USB 2.0)
- 2x 15-pinové konektory, CSI (pro kameru) a DSI (pro displej)

Výkon RPi je srovnatelný se starším stolním počítačem nebo levným chytrým telefonem. Běží na něm různé distribuce Linuxu
(Raspbian, Manjaro, atd.) a i jiné OS (například Windows 10 IoT).

## GPIO

[Delší, ale jednodušší tutoriály na pochopení v angličtině](https://github.com/raspberrypilearning/physical-computing-guide/blob/master/worksheet.md)

[Projekty Raspberry Pi foundation](https://projects.raspberrypi.org/en)

RPi nabízí 40-pinový GPIO (General-purpose input/output) header, což jsou vstupní nebo výstupní piny, dsot z nich se
může libovolně programovat a některé slouží jako ground piny. Jsou využívány k připojení vstupně-výstupních periferií, jako jsou například LED
diody, podporované displeje, tlačítka, reproduktory a mnoho dalších. Piny mají dva způsoby číslování, fyzické pořadí
pinů a BCM.

Na těchto GPIO pinech je možné nastavit dvě logické hodnoty 1 a 0. Díky logické 1 bude na pin přivedeno napětí 3.3V, anebo pomocí logické 0 se dosáhne napětí 0V. Maximální napětí těchto pinů není přesně uvedené, předpoklady jsou
kolem 60 mA.

GPIO také nabízí piny s napětím 5V, 3.3V a GND. Na pinech se také nachází SPI sběrnice a I<sup>2</sup>C
sběrnice. Všechny použitelné piny jsou schopné použít PWM za pomocí knihoven jako `pigpio` a nástavby na ně, jako
`gpiozero`, které používají zabudovaný DMA controller v procesoru RPi.

[Interaktivní přehled všech pinů a číslování](https://pinout.xyz/pinout/3v3_power)

### SPI (Serial Peripheral Interface)

Je sériové periferní rozhraní, používá se mezi řídícími mikroprocesory a integrovanými obvody, komunikace je
řešena pomocí společné sběrnice. U rozhraní SPI je vždy jeden řídicí obvod (Master) a jeden či více periferních
obvodů (Slave). Master řídí celou komunikaci a pomocí signálů SlaveSelect určuje, se kterým periferním zařízením
se právě pracuje.

Master aktivuje signál SlaveSelect (SS) pro obvod s kterým chce komunikovat a uvede jej do log. 0. Poté co je obvod
vybrán, Master na výstupu SCLK (serial clock) začne posílat hodinové pulsy, a zároveň posílá data na výstupu MOSI (
Master Out, Slave In), jakmile přenos skončí, uvede vstup SS do neaktivního stavu.

SPI je plně duplexní sběrnice, takže pokud probíhá i komunikace ze strany Slave -> Master slouží k tomu vodič MISO (
Master In, Slave Out)

### I<sup>2</sup>C

(někdy taky TWI)

Komunikace probíhá na dvou vodičích, datový SDA a hodinový SLC Je zde taky Master a Slave, ale na rozdíl od SPI má
Slave vlastní sedmibitovou adresu (0-127)
Master na vodiči SDA pošle log. 0 a poté nastaví 0 i na lince SCL, tím vznikne „startovací signál“ následně master
začne vysílat hodiny a zároveň posílá na vodič SDA data.

## Instalace operačního systému

Nejjednodušší způsob instalace OS na RPi je si stáhnout NOOBS, připojit RPi k displeji, klávesnici a internetu, vybrat
si operační systémy, o které máme zájem a nainstalovat. Následující kroky už pak závisí na každém z OS.

*Poznámka: NOOBS je nic moc oproti [PINN](https://github.com/procount/pinn), což je fork NOOBS*

## Používání GPIO

### Programování a zapojení 7 segmentového displeje

Dva typy 7 segmentového displeje:

- společná katoda (-) - logická 0 = svítí
- společná anoda (+) - logická 1 = nesvítí

Číslování podle pinů (1-40) (BCM číslování podle GPIO, BOARD podle pozice pinů - v tom případě místo `GPIO.BCM` dáme `GPIO.BOARD`)

```python
GPIO.setmode(GPIO.BOARD)
```

Nastavení pinů pro výstup (musí se provést u všech pinů) například:

```python
GPIO.setup(35, GPIO.OUT) #GPIO
```

Pokud máme společnou anodu, tak 1 nesvítí, 0 svítí (u katody je to naopak).

K displeji máme připojených 7 pinů (nezapojujeme tečku) např:

```python
gpin = [35, 12, 36, 33, 32, 38, 40]
```

Každý pin je připojen k jednomu segmentu:

| Segment | Pin |
|:-------:|-----|
|    A    | 35  |
|    B    | 12  |
|    C    | 36  |
|    D    | 33  |
|    E    | 32  |
|    F    | 38  |
|    G    | 40  |

Chceme-li rozsvítit 5, musíme zapnout segmenty A, C, D, G, F.

Segment rozsvítíme:

```
GPIO.output(cislo_pinu, 0)
```

Zapneme piny 35, 36, 33, 40, 38 Na konci všech programů je vhodné používat:

```
GPIO.cleanup()  # reset pinů
```

### Vstupní periferie

Tlačítka mají čtyři vývody. Vždy dva a dva jsou spojeny dohromady

**Zákmit** - při zmáčknutí procesor zachytí dvě a více po sobě jdoucích stisknutí. Řešení zákmitů:

- Mechanicky – tedy použitím tlačítek bez zákmitů, nicméně ty jsou velmi drahé
- Elektricky – přidáním vhodného kondenzátoru – odfiltruje rychlé pulsy, Schmittův obvod
- Softwarově – nejjednodušší řešení je při každém stisknutí tlačítka počkat třeba 50 milisekund, zkontrolovat
  zda je tlačítko stále stisknuté, a teprve poté dělat nějakou akci. Těmto postupům se říká debouncing

#### Pull Up a Pull Down

Pro nastavení PullUP/PullDOWN přes Python:

```python
GPIO.setup(button_pin, pull_up_down=GPIO.PUD_UP/ GPIO.PUD_DOWN)
# pokud se použije toto nastavení, není nutné dávat Pull Up/Down rezistor fyzicky do obvodu
```

Když stiskneme tlačítko, objeví se na GPIO pinu buď napětí 3.3 V nebo 0 V (zem). Pokud však tlačítko pustíme, pin se
nemá k čemu připojit, je připojený jen tak ke „vzduchu“ a Raspberry vlastně neví, co má měřit. Pokud tohle nestačí jako
definice, [oficiální guide od RPi Foundation má na tohle dobrou analogii](https://github.com/raspberrypilearning/physical-computing-guide/blob/master/pull_up_down.md#an-analogy)
.

Abychom se tomu vyhnuli použijeme Pull Up / Pull Down rezistor, který při nestisknutém tlačítku připojí GPIO pin ke
kladnému napětí, respektive zemi. Při použití Pull Up se tedy tlačítko tváří při zmáčknutí jako logická 0, při použití
Pull Down jako logická 1.

##### Projekt - aktivace LED s tlačítkem

Chtěl jsem to udělat původně v `RPi.GPIO` (se kterým se učilo ve škole xd), ale vůbec mi to nejelo. Tento kód by měl
teoreticky fungovat ale nefunguje:

```python
import RPi.GPIO as GPIO

led = 17
btn = 4
status = False

GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
GPIO.setup(btn, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
GPIO.setup(led, GPIO.OUT)
GPIO.output(led, True)


def toggle():
    global status
    print("xd lmao")
    status = not status
    GPIO.output(led, status)


GPIO.add_event_detect(btn, GPIO.FALLING, callback=toggle)
input()
GPIO.cleanup()
```

Jen FYI, tohle dělá to samé přes gpiozero:

```python
from gpiozero import Button, LED

btn = Button(4, bounce_time=.05)
led = LED(17)

btn.when_activated = led.toggle
btn.when_deactivated = led.toggle
input()
```

```
Editor: Roman Táborský

Autor: Matula Daniel
Datum: 10.5.2020
Merger: Vít Staniček
```