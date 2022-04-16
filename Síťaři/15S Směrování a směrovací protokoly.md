# 15S. Směrování a směrovací protokoly

> Statické a dynamické směrování. Výchozí síť, masky, VLSM. Přehled směrovacích protokolů (RIP, RIPv2, EIGRP, OSPF), cena cesty, metrika. VLAN routing, „router on the stick“, NAT. Popis dynamických protokolů, kompatibilita, algoritmy vyhledávání cesty, konfigurace (příkazy pro nastavení Cisco směrovačů).

---

## Směrovač (router)

Je zařízení, které provádí routování, propojuje jednotlivé sítě a dovoluje přeposílání dat mezi nimi.

## Routing

Česky řečeno směrování, ale častěji se používá slovo routování. Jedná se o techniku, která slouží k propojení
jednotlivých sítí (přesněji subnetů). Původním zařízením, určeným pro routování byl router, ale v dnešní době se velmi
využívají L3 switche, firewally nebo pouze servery/počítače. Router přeposílá komunikaci z jedné sítě do jiné.

### Jednotlivé routovací metody

* **distance-vector routing protocol** - routery udržují routovací tabulku s informací o (vektoru) vzdálenosti do dané
  sítě, periodicky routovací tabulku zasílají sousedům, ti si upraví svoji tabulku a tu opět odešlou dál, pro výpočet
  nejlepší cesty se používá jedna (počet hopů u RIP) nebo více metrik (propustnost linky a zpoždění u IGRP). Upraveným
  typem distance-vector protokolu je path-vector protocol.

* **link-state routing protocol** - routery udržují komplexní databázi síťové topologie (vytvořenou pomocí LSA),
  vyměňují si link-state advertisements (LSA), LSA jsou vyvolány nějakou událostí v síti, do svého okolí také odesílá
  Hello pakety, kde zasílá informace o sobě, rychle reaguje na změny topologie, ale spotřebovává více pásma a zdrojů na
  routeru, metrika je komplexní, nejlepší cesta se počítá pomocí Dijkstrova algoritmu shortest path first (SPF)

Dále dělíme dynamické protokoly podle toho, zda jsou určeny pro nasazení uvnitř lokální sítě (přesněji řečeno uvnitř
autonomního systému (AS), který může obsahovat několik LAN) nebo fungují napříč sítěmi (spojují AS dohromady):

* **interior gateway protocol** (IGP) - routuje uvnitř Autonomous System
  (AS)

* **exterior gateway protocol** (EGP) - routuje mezi AS

#### Static routing

* používá se například mezi ISP a firmou, kde není třeba, aby běhal složitý routovací protokol
* pro každou síť je vložen záznam do routovací tabulky
* žádná zátěž
* pouze pro malé sítě

##### Nastavení na Cisco routeru

```
ip route [destination_network] [mask] [next_hop or exit_interface] [administrative_distance] [permanent]
SWITCH (config)#ip route 192.168.50.0 255.255.255.0 192.168.1.1
```

Vysvětlení některých parametrů:

* `next_hop` je IP adresa dalšího routeru v cestě, přesněji, je to adresa interface sousedního routeru, který sousedí s
  tímto routerem
* `exit_interface` je jméno lokálního výstupního interface (třeba s0), přes který vede cesta k cílové síti

#### Default routing

* může se použít pouze na kraji sítě, kde je jeden port, který vede mimo síť
* pokud není definována jiná cesta k dosažení cíle, tak se použije defaultní routa, což je gateway

##### Nastavení na Cisco routeru

```
ip route 0.0.0.0 0.0.0.0 [next_hop or exit_interface]
SWITCH(config)#ip route 0.0.0.0 0.0.0.0 62.102.58.12
```

### Routovací tabulka

Do routovací tabulky se vytváří několik typů záznamů cest (route), záleží na tom, jakým způsobem vznikly. Pakety jsou
podle toho směrovány jedním ze základních způsobů routování.

#### Statické routování

Ručně zadané cesty (záznamy v routovací tabulce), bezpečné a dobré, ale nereflektuje změny v topologii sítě.

#### Dynamické routování

Síť se automaticky přizpůsobuje změnám v topologii a dopravě, automaticky se vypočítávají cesty pomocí routovacího
protokolu.

#### Defaultní routování

Pokud neexistuje jiná cesta, tak se použije defaultní.

### Směrovací protokoly

#### RIP - Routing Information Protocol

* jednoduchý pro konfiguraci a funguje všude
* pro malé a střední sítě
* RIP 1 nepodporuje VLSM
* plýtvá pásmem (velká režijní komunikace)
* pomalá konvergence (rozšiřování)
* hloupá metrika - počet hopů
* posílá celou routovací tabulku svým sousedům
* maximálně 15 hopů

Definují se pouze sítě, které jsou přímo na tomto routeru, ostatní se naučí pomocí updatů.

##### Nastavení na Cisco

```
SWITCH (config)#router rip
SWITCH(config-router)#network 132.43.54.0
SWITCH(config-router)#network 145.65.76.0
```

#### IGRP - Interior Gateway Routing Protocol

* proprietární Cisco protokol
* nepodporuje VLSM
* jako metriku používá cenu, záleží na pásmu a zpoždění
* maximální počet hopů 255

##### Nastavení na Cisco (33 je číslo AS)
Číslo 33 znamená číslo AS.

```
SWITCH (config)#router igrp 33
SWITCH(config-router)#network 134.43.54.0
SWITCH(config-router)#network 143.56.76.0
```

#### EIGRP - Enhanced Interior Gateway Routing Protocol

* proprietární Cisco protokol
* rychlá konvergence
* redukuje spotřebu pásma pro routovací updaty
* podporuje různé protokoly (apple talk, IPX, IP) a VLSM
* metrika - pásmo, zpoždění (případně i zátěž, spolehlivost)
* routovací update se vyměňují pouze mezi routry ve stejném AS
* maximální počet hopů 255
* bez smyček

Používá tabulku sousedů (informace o přímých sousedech), tabulku topologie (všechny routovací záznamy, které se naučil)
a routovací tabulku (nejlepší routy z tabulky topologie).

##### Nastavení na Cisco (33 je číslo AS)
Číslo 33 znamená číslo AS.

```
SWITCH (config)#router eigrp 33
SWITCH(config-router)#network 172.16.0.0
SWITCH(config-router)#network 10.0.0.0
```

#### OSPF - Open Shortest Path First

* hierarchický systém -- jedna nebo více oblastí je spojena k páteřní oblasti (oblast 0)
* routery posílají linkstate (pásmo a stav interface) informace všem sousedním routrům v oblasti
* routery vytvářejí databázi topologie, což je model celé oblasti
* z databáze se pomocí Dijkstry vypočítá nejkratší cesta a zapíše do routovací tabulky
* neomezený počet hopů
* určeno pro rozsáhlé sítě heterogenní sítě
* podporuje VLSM

**Nastavení na Cisco routeru (1 je ID číslo procesu, pouze lokálně významné):**

1 je ID procesu, významné pouze lokálně. 

```
SWITCH(config)#router ospf 1
SWITCH(config-router)#network 132.43.56.0 0.0.0.255 area 0
SWITCH(config-router)#network 145.54.34.6 0.0.63.255 area 0
```

## Důležité pojmy pro routování

* **router** - zařízení, které provádí routování
* **routing** - routování, přeposílání (forwarding) dat mezi sítěmi
* **route** - cesta, která se použije, zapsaná v routovací tabulce
* **routing table** - routovací tabulka obsahuje záznamy o jednotlivých cestách
* **routing protocol** - routovací protokol slouží ke směrování routovaného protokolu, určuje nejlepší cestu k cíli a posílá routovací informace dalším routerům
* **routed protocol** - routovaný protokol je IP, IPX nebo Apple Talk
* **router on stick** - router, který je připojený do switche pomocí jednoho trunk portu - tzn. máme pouze jeden router a pouze jednu linku, což přináší velkou zátěž na router i linku a problémy při výpadku
* **Variable Length Subnet Masking (VLSM)** - Používá se v Classless Inter-Domain Routing (CIDR). V tomto případě můžeme v subnetu použít různé velikosti masky. Můžeme například použít dohromady subnety 10.0.0.0/26 a 10.0.0.64/28.
* **Autonomní systém** AS (Autonomous System) - skupina IP sítí a routerů, které jsou pod správou jedné (nebo více) jednotek
* **Administrativní vzdálenost** AD (Administrative Distance) - Vlastnost používaná na routrech k určení nejlepší cesty mezi více routovacími protokoly. Definuje spolehlivost protokolu a prioritizuje lepší nižším číslem. Jinak řečeno na routeru může běžet více routovacích protokolů a podle AD se rozhoduje, který se použije. Na Cisco routerech můžeme měnit defaultní hodnoty.
* **split horizon** - Metoda, která slouží k zamezení vzniku smyček v Distance Vector Routing protokolech. Používá se u RIP, IGRP a EIGRP. Funguje tak, že zakazuje posílání routovací cesty zpět na rozhraní, z kterého se naučila.
* **hold-down timer** - Metoda, kterou používají routovací protokoly, aby zabránily zbytečnému nebo předčasnému rozesílání routovacích cest v nestabilním prostředí (ve chvíli, kdy dochází k časté změně stavu). Router čeká určitý čas, než je síť stabilní.

```
Autor: Jakub Tománek
Datum: 5.2.2022
```