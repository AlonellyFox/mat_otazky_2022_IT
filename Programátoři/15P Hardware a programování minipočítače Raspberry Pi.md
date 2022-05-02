# 15P. Hardware a programování minipočítače Raspberry Pi

> Architektura ARM-A, popis parametrů a možností – porovnání s PC, rozhraní GPIO a jeho popis. Výběr a instalace OS, konfigurace. Využití jazyka Python k programování na RPi3. Připojení periferií k RPi3, RPi.GPIO. Princip programování statických výstupních periferií (řada LED, 7Segm) a dynamických periferií (3x7Segm, reproduktor), vstupní periferie.

---

## Architektura ARM

- 32/64 bitová mikroprocesorová architektura typu RISC
- Oproti x86 má menší spotřebu energie a produkuje tedy méně tepla
- Používá se v mobilních zařízeních (notebooky, mobily, tablety, atd.)

## Popis parametrů a porovnání s PC

Nejnovější RPi 4

- 64bit čtyřjádrový procesor Broadcom BCM o taktu 1,5 GHz
- RAM 8 GB (nejvyšší model)
- Napájení USB-C (dříve micro-USB) - 5V
- Dva micro-HDMI porty (s podporou rozlišení 4K, dříve jen jeden HDMI port)
- 4x USB (2x USB 3.0, 2x USB 2.0)
- 2x 15-pinové konektory, CSI (pro kameru) a DSI (pro displej)

Výkon RPi je srovnatelný se starším stolním počítačem nebo levným chytrým telefonem. Běží na něm různé distribuce Linuxu
(Raspbian, Manjaro, atd.) a i jiné OS (například Windows 10 IoT).

## GPIO

[Delší, ale jednodušší tutoriály na pochopení v angličtině](https://github.com/raspberrypilearning/physical-computing-guide/blob/master/worksheet.md)

[Projekty Raspberry Pi foundation](https://projects.raspberrypi.org/en)

RPi nabízí 40-pinový GPIO (General-purpose input/output) header, což jsou vstupní nebo výstupní piny, dost z nich se
může libovolně programovat a některé slouží jako ground piny. Jsou využívány k připojení vstupně-výstupních
periferií, jako jsou například LED diody, podporované displeje, tlačítka, reproduktory a mnoho dalších. Piny mají
dva způsoby číslování, fyzické pořadí pinů a BCM.

Na těchto GPIO pinech je možné nastavit dvě logické hodnoty 1 a 0. Díky logické 1 bude na pin přivedeno napětí
3.3V, anebo pomocí logické 0 se dosáhne napětí 0V. Maximální napětí těchto pinů není přesně uvedené, předpoklady jsou
kolem 60 mA.

GPIO také nabízí piny s napětím 5V, 3.3V a GND. Na pinech se také nachází SPI sběrnice a I<sup>2</sup>C sběrnice.
Všechny použitelné piny jsou schopné použít hardware PWM za pomocí knihoven jako `pigpio` a nástavby na ně, jako
`gpiozero`, které používají zabudovaný DMA controller v procesoru RPi.

[Interaktivní přehled všech pinů a číslování](https://pinout.xyz/pinout/3v3_power)

## Instalace operačního systému

Nejjednodušší způsob instalace OS na RPi je si stáhnout NOOBS, připojit RPi k displeji, klávesnici a internetu, vybrat
si operační systémy, o které máme zájem a nainstalovat. Následující kroky už pak závisí na každém z OS.

Alternativní způsob je stáhnout si přímo image operačního systému a ten nahrát na SD kartu přes program
jako [Rufus](https://rufus.ie/en/) nebo
[balenaEtcher](https://www.balena.io/etcher/).

*Poznámka: NOOBS je nic moc oproti [PINN](https://github.com/procount/pinn), což je fork NOOBS*

## Používání GPIO

Příklady kódů pro práci s GPIO se nachází [na moodle](https://moodle.roznovskastredni.cz/course/view.php?id=17#section-1).

### Programování a zapojení 7 segmentového displeje

Dva typy 7 segmentového displeje:

- společná katoda (-) - logická 0 = svítí
- společná anoda (+) - logická 1 = nesvítí

Následující kód inicializuje ve vícerozměrném poli mapu hodnot na displeji a postupně je zobrazuje.

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
vystupy = [4, 17, 18, 23, 24, 25, 5]

# dvourozměrné pole, určuje hodnoty 7 segmentového displeje
# displej se společnou katodou, 0 = svítí, 1 = nesvítí
hodnota = [
    [0, 0, 0, 0, 0, 0, 1],
    [1, 0, 0, 1, 1, 1, 1],
    [0, 0, 1, 0, 0, 1, 0],
    [0, 0, 0, 0, 1, 1, 0],
    [1, 0, 0, 1, 1, 0, 0],
    [0, 1, 0, 0, 1, 0, 0],
    [0, 1, 0, 0, 0, 0, 0],
    [0, 0, 0, 1, 1, 1, 1],
    [0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 1, 0, 0]
]

# nastavíme všechny piny z proměnné vystupy jako výstupní a dáme jim logickou 1, aby nesvítily (společná katoda)
GPIO.setup(vystupy, GPIO.OUT, initial=GPIO.HIGH)

try:
    # postupně prochází všechny čísla na displeji
    while True:
        for cislo in hodnota:
            print(cislo)
            GPIO.output(vystupy, cislo)
            time.sleep(1)
except KeyboardInterrupt:
    GPIO.cleanup()  # mělo by být na konci každého GPIO kódu
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

Tento kód přes `RPi.GPIO` by teoreticky měl fungovat. Bude vždy čekat do stisku tlačítka a jak se tak stane, změní stav
LED.

```python
import RPi.GPIO as GPIO

led = 17
btn = 20

# nastavení LED a tlačítka jako výstup
GPIO.setup(led, GPIO.OUT)
GPIO.setup(btn, GPIO.IN, pull_up_down=GPIO.PUD_UP)

# hodnota LED
value = False

while True:
    GPIO.wait_for_edge(btn, GPIO.RISING)  # čeká na stisk tlačítka
    value = not value
    GPIO.output(led, value)  # rozsvítí/zhasne LED
```

```
Editor: Roman Táborský

Autor: Matula Daniel
Datum: 10.5.2020
Merger: Vít Staniček
```