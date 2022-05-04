# 17. Pokročilé skriptování na straně klienta a serveru

> Validace webových formulářů, JSON, AJAX (využití, události, asynchronnost). Objektově orientovaný přístup
> při programování v PHP (třídy, metody, syntaxe), příklad pro využití OOP v PHP.

---

## Validace webových formulářů

- Validaci můžeme provádět na straně serveru (PHP) nebo na straně klienta (javascript, html)

### Na straně klienta

Validujeme vždy nějaký HTML formulář, ve kterém uživatel zadal nějaké údaje. Například chceme, aby všechny údaje byly
vyplněné nebo aby jméno a příjmení začínalo vždy velkým písmenem.

Co se týče úplného vyplnění formuláře, je možné jej kontrolovat přímo pomocí HTML. k tomu nám pomůže
například `required`.

 ```html
<form action="/odeslat.php" method="post">
  <input type="text" name="fname" required>
  <input type="submit" value="Odeslat">
</form>
```

## JSON - JavaScript Object Notation

- slouží pro výměnu dat
- je textový a nezávislý na jazyce
- jeho datová struktura je:
    - pole
    - objekt
    - číslo
    - řetězec
    - boolean
    - null

### Posílání dat:

``` javascript
const myObj = {name: "John", age: 31, city: "Praha"};
const myJSON = JSON.stringify(myObj);
localStorage.setItem("testJSON", myJSON);
```

**myJSON** – obsahuje `'{"name":"John","age":31,"city":"New York"}'`

**localStorage** – ukládání dat na lokální úložiště a není potřeba data ukládat na server.

### Přijímání dat:

``` javascript
let text = localStorage.getItem("testJSON");
let obj = JSON.parse(text);
document.getElementById("demo").innerHTML = obj.name;
```

## JSONP

- je metoda pro posílání JSON dat asynchronně na server bez použití AJAXu.
- Nepoužívá XMLHttpRequest object (základní objekt v AJAXu), ale používá `<script>`.

``` js
function clickButton() {
  let s = document.createElement("script");
  s.src = "demo_jsonp.php";
  document.body.appendChild(s);
}
```

***

## AJAX

Používá se k asynchronnímu přenosu

- načítá data na pozadí

``` javascript
function loadDoc() {
  const xhttp = new XMLHttpRequest();
  xhttp.onload = function() {
    document.getElementById("demo").innerHTML = this.responseText;
    }
  xhttp.open("GET", "ajax_info.txt", true);
  xhttp.send();
}
```

| Kód                    | Co dělá                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------|
| `new XMLHttpRequest()` | vytvoří nový XMLHttpRequest()                                                                  |
| `send()`               | odesílá požadavek na server pomocí GET nebo POST                                               |
| `responseText`         | vrací data jako string                                                                         |
| `status`               | vrací číslo statusu requestu (**200** - ok, **404** - nebylo nalezeno, **500** - server error) |
| `onload`               | definuje funkci, která se má zavolat, když je požadavek přijat (načten)                        |

## Jquery AJAX

- umožňuje načíst data na pozadí stránky bez nutnosti refreshe

### Metody

| Metoda   | Co dělá                                                                            |
|----------|------------------------------------------------------------------------------------|
| `Load()` | načte data ze serveru a vloží je do elementu `$(selektor).load(URL,data,callback)` |
| `GET`    | zisk dat                                                                           |
| `POST`   | odesílání dat (např. formulář)                                                     |

```js
$.get(URL, callback)

$.post(URL, data, callback)
```

***

## OOP PHP

OOP = objektově orientované programování

- základní jednotkou je objekt
- objekt má atributy a metody

`atributy` – vlastnosti, data, proměnné

`metody` – schopnosti funkce

### Třída

- je to vzor, podle kterého se objekty vytváří

`objekt` = instance

Vytvoření objektu

```php
$karel = new Osoba()

//	zavolání metody
$karel -> pozdrav();

```

### Vytvoření třídy

```php
Class Clovek {

}
```

### Atributy

```php
public $jmeno;    // přístupnost z venku všem uživatelům

protected $jmeno;   // je přístupná uživatelům třídy (rodiče) a podtřídy, která tuto třídu dědí

private $jmeno;    // metoda nebo vlastnost předznačená klíčovým slovem private je přístupná pouze uvnitř třídy

```

### Magické metody

- spouští se v určitých chvílích automaticky

#### Konstruktor

- volá se po vytvoření instance
- pokud chceme u potomka použít jiný konstruktor, musíme jej znovu nadefinovat

```php
public function_construct($jmeno,$prijmeni,$vek,$ide){
  $this -> ide = $ide;
  Parent:__construct($jmeno,$prijmeni,$vek)
}

```

#### Destruktor

- spouští se ve chvíli, kdy chceme objekt převést na textový řetězec

### Pilíře OOP

- Zapouzdření
- Dědičnost
- Polymorfismus

#### Zapouzdření

- umožňuje skrýt některé metody a atributy tak, aby zůstaly použitelné jen pro třídu zevnitř
- zapouzdření rozdělí rozhraní třídy na veřejné (public) a vnitřní (private)

```php
private $pocet = 0; // nepřístupné zvenku
```

- můžeme proměnou nastavit pomocí metody

### Referenční datové typy

- objekty

```php
$a = new Clovek (`Karel`, `Novák`, 30);
$b = $a;
$b -> vek = 50;
// $a i $b teď mají věk roven 50
```

- objekty jsou uloženy v tzv. haldě (heap)
- do `$a` se uložila reference na objekt v haldě
- zkopírováním do `$b` se do `$b` uložil odkaz na objekt v haldě

### Dědičnost

- slouží k vytvoření nových datových struktur na základu starých
- klíčové slovo extends

```php
class Javista extends Clovek {
	public function programuj() {
		echo(`Programuji…`)
  }
}
```

- při využití dědičnosti stačí do nové třídy dopsat to v čem se liší
- není potřeba opisovat již napsaný kód

***

### Volání jiného PHP souboru

Operátory `require` a `require_once` – (require – vloží zadaný soubor vždy, require_once – vloží zadaný soubor, jen
pokud již vložen nebyl)

Tyhle operátory může použít například k vytvoření šablon a načítat tak data a skripty z jiných stránek

V PHP souboru poté další PHP soubor načítáme následovně:

``` php
<?php
require_once('tridy/Clovek.php');

// 'tridy/Clovek.php' - označují cestu k souboru, který chceme načíst
```

### Polymorfismus

- umožňuje používat jednotné rozhraní pro práci s různými typy objektů
- polymorfismus umožňuje přepsat metodu u každé podtřídy tak, aby dělala, co chceme

### Final

- použitím final zakážeme přepsání metody u potomka
- final lze použít i u třídy, danou třídu pak nelze dědit

```
Autor: Marek Matulík
Datum: 4. 5. 2022
```





