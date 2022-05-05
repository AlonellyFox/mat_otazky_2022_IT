# Databázový systém MySQL

> Nástroj pro správu DB. Založení DB, import/export, údržba, úpravy, zabezpečení (účty, oprávnění). Využití SQL dotazů
> při úpravách. Entity, atributy. Šifrování databáze. Základní příkazy PHP pro práci s MySQL (spojení, výběr, vložení,
> úprava). Funkce pro hashování (dle vhodnosti použití).

---

## Grafický pro správu databáze

`phpMyAdmin` - nástroj pro správu databáze MySQL jazykem PHP prostřednictvím webového rozhraní

Všechny operace popsané zde se dají provést graficky přes zmíněné rozhraní za pomocí lehce viditelných tlačítek.

## Vytvoření databáze

```sql
CREATE DATABASE nazev_databaze;
CREATE TABLE nazev_tabulky (
    sloupec1 datatype;
    sloupec2 datatype;
    ...
);
```

## Export a import databáze

Provádí se graficky přes phpMyAdmin. Při výběru databáze nebo tabulky v bočním menu dostaneme možnost pro export dat.
Import dat probíhá stejným procesem, rovněž přes tlačítko v navigaci.

## Údržba databáze

???

## Úpravy databáze

```sql
ALTER TABLE tabulka ADD nazev_sloupce datatype;  -- přidá sloupce
ALTER TABLE tabulka DROP nazev_sloupce;  -- odstraní sloupec
ALTER TABLE tabulka MODIFY nazev_sloupce datatype;  -- změní datový typ sloupce
```

Tyto úpravy lze i provést v rozhraní phpMyAdmin a u zkoušek snad přijdete na to kde :wink:.

## Zabezpečení

* prevencí využívaní root uživatele a změnou jeho hesla na velmi silné
* odstraněním testovací databáze `mysql_install_db`, která je součástí instalace MySQL serveru
* změnou výchozího portu databáze (3306) na jiný pro zmatení útočníků
* vyžadováním hesla u všech účtů
* šifrováním binary a relay log
    * binary log - log modifikací na serveru
    * relay log - sada číslovaných souborů popisujících změny v databázi

## Entity a atributy

### Entita

Entita je objekt reálného světa, který je schopen nezávislé existence a je jednoznačně rozlišitelný od odstaních
objektů. Je to v podstatě cokoli (osoba, věc, událost), o čem potřebujeme uchovávat informace. Entitou může být např.
student, kniha, výrobek, půjčka. rezervace atd. Informace uchováváme v tabulkách. **Jeden řádek tabulky** potom
představuje **jednu entitu** (jeden záznam).

### Atribut

Údaj, který o entitě evidujeme, třeba jméno, příjmení, datum narození. **V databázích má určený název a datový typ.**

## Šifrování databáze

K šifrování se používá funkce `AES_ENCRYPT` a k dešifrování `AES_DECRYPT`.

```mysql
AES_ENCRYPT(str,key_str)
AES_DECRYPT(crypt_str,key_str)
```

Parametry:

* `str`/`crypt_str` - text k zašifrování či dešifrování
* `key` - šifrovací klíč

Příklad použití:

```mysql
INSERT INTO tabulka VALUES (1, AES_ENCRYPT("text", "zasifrovano"));
```

Tento příklad vloží do tabulky `tabulka` dvě hodnoty do dvou sloupců, `1` a zašifrovaný text "text".

## Použití v PHP

PHP pracuje s databází za pomocí `mysqli` rozšíření.

### Připojení k databázi

```php
$spojeni = new mysqli($nazevserveru, $uzivatelskejmeno, $heslo, $jmenodb);

if (mysqli_connect_error()) {
    die("Spojení selhalo: " . mysqli_connect_error());  // kontola spojení k databázi
}
```

### Výběr dat

Nejprve si vytvoříme proměnnou, do které uložíme SQL dotaz a ten pak pošleme na databázi. Ze získané žádosti potom
můžeme získat všechny řádky a sloupce.

```php
$sql = "SELECT Lastname, Age FROM Persons ORDER BY Lastname";
$result = $mysqli -> query($sql);

$result -> fetch_all(MYSQLI_ASSOC);
```

### Úprava dat

```php
$pozadavek = "INSERT INTO MyGuests (firstname, lastname, email)
VALUES ('John', 'Doe', 'john@example.com')";

// odeslání požadavku přes query
if ($spojeni->query($pozadavek) === TRUE) {
    echo "Úprava byla úspěšná";
} else {
    echo "Chyba: " . $pozadavek . "<br>" . $conn->error;
}
```

## Hashovací funkce

Pro hashování se zpravidla používá jen několik funkcí:

* md5 - víceméně jen pro ověření integrity dat
* sha-256, sha-512 atd. - taky jen pro ověření integrity, složitější na výpočet než md5, má ale větší délku a tedy menší
  šanci pro stejný hash pro jiná data
* crc-32 - používané v sítích na packety
* bcrypt - používá salt, šifrují se přes něj hesla (není to hash funkce)
