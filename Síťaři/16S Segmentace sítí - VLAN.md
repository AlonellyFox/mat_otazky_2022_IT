# 16. Segmentace sítí - Vlan

## Principy segmentace
Principy segmentace
Segmentace se provádí hlavně z důvodu bezpečnosti, 
oddělením několika sítí od sebe. Využívá se při tom jednoduchého řešení pomocí VLAN tzn. 
na jednom kanálu dokážeme vytvořit klidně několik VLAN, kde každá může být na jiné síti. 
Odpadá tím nutnosti mít pro každou síť vlastní switch a router, zároveň nám to ulehčí správu sítě a zvýší výkon.

## VLAN (default, native, management)
Default VLAN: Výchozí VLAN,vždy VLAN 1 a nejde změnit, do této VLAN jsou defaultně přiřazeny všechny porty.
Native VLAN: Defaultně také VLAN 1, nastavuje se u trunk portů (na obou switchích MUSÍ být stejná),všechna komunikace je tagovaná tzn., že komunikace mezi stanicema v VLAN 10 budou mít v hlavičce ID s číslem 10, native VLANa pak slouží pro netagovanou komunikaci (https://www.youtube.com/watch?v=Fmq1E1Qr2W4), z bezpečnostních důvodů je lepší změnit z defaultního nastavení.
Management VLAN: Slouží pro vzdálenou konfiguraci, při konfiguraci nechceš aby komuniaci mezi tebou a síťovým prvkem někdo odposlouchával, tudíž je odsekneš, aby komunikaci neviděli.

### Příklad konfigurace modů vlany
```
vlan 10 -založení VLANy 10
int fa0/1
switchport mode access -změna módu na portu
switchport access vlan 10 -přiřazení portu do VLANy

switchport mode trunk -změna módu na portu
switchport trunk allowed vlan 10,20 -povolené VLANy na trunku
```

## Konfigurace DHCP
```
ip dhcp pool vlan10
network 192.168.1.0 255.255.255.0
default-router 192.168.1.254
dns-server 8.8.8.8
ip dhcp exclude 192.168.1.254
```

## VLAN trunking protocol - VTP
- Cannot be used on non-Cisco switches
- VTP domain must be the same
- One switch must be configured in server mode
- If a VTP password is used, must be configured on all switches

```
první switch

(nutnost nastavit trunk, na porty které spojují switche)

vtp domain yourmom.com
vtp mode server
vtp password heslo
vtp version 2

druhý switch

(nutnost nastavit trunk, na porty které spojují switche)

vtp domain yourmom.com
vtp mode client
vtp password heslo
vtp version 2
```


L2 protokol, který slouží k přenášení informací o VLANách mezi více switchi, 
odpadá tím nutnosti manuální konfigurace VLAN na každém switchi pomocí trunku
VTP spravuje přidávání, mazání a přejmenování VLAN uvnitř VTP domény. 
VTP doména je tvořena síťovými zařízeními, která mají nastaveno stejné jméno domény a 
jsou propojeny pomocí trunku.

Módy VTP domény:
    • server – defaultní mód, spravuje seznam všech VLAN, může vytvářet a mazat VLANy, přijímá a odesílá advertisements přes trunky ve VTP doméně 
    • klient – přijímá konfiguraci ze serveru, udržuje lokální kopii všech VLAN, kterou nelze měnit a nemá ji uloženou v NVRAM, přijímá a odesílá advertisements
    • transparentní – neúčastní se VTP, pracuje samostatně, může vytvářet i mazat VLANy, ale změny jsou lokální, přijímá advertisements,lient mode only receives and forwards VTP updates. Can not create, delete or modify existing VLANs

## Spanning tree protocol 
Spanning Tree Protocol prevents switching loops at layer 2\. 
It elects a root bridge and a root port and does this by sending out BPDUs 
(bridge protocol data units), a blocked port will still receive BPDUs and needs to 
receive them in case it needs to come out of the blocked state (link failure, bandwidth changes).

## Rapid Spanning tree protocol
RSTP byl vymyšlen, aby zkrátil čas konvergence STP z původních 50s na 1 či 2s. 
Základní princip je podobný klasickému STP, ale je upraven pro rychlejší konvergenci při změně topologii. Má integrován ekvivalent Cisco funkcí PortFast, UplinkFast a BackboneFast.
Typy portů/linek:
    • point-to-point – připojení dalšího switche, linka musí být full duplex
    • edge – koncový/hraniční port (PortFast), je do něj připojeno koncové zařízení PC
    • shared – sdílená linka, například hub, linka je half duplex

RSTP can detect a link failure in 6 seconds (3 hello timers, 2 seconds each)

## Per VLAN Spanning Tree
Default for catalyst switches. Cisco proprietary protocol, 
allows for creation of per VLAN spanning tree.

## Rapid PVST+
Rapid PVST+ is the IEEE 802.1w (RSTP) standard implemented per VLAN. 
Each Rapid PVST+ instance on a VLAN has a single root switch. 
You can enable and disable STP on a per-VLAN basis when you are running Rapid PVST+.

Pro každou VLAN běží vlastní samostatná instance STP. Výhodou je, že mohu rozdělit zátěž, 
že každá VLAN komunikuje jinou cestou. Používá dot1q trunk.
Čím více VLAN (více STP instancí), tím větší zatížení přepínače. Klasické STP, 
má pouze jednu STP instanci pro všechny VLANy, což znamená menší HW náročnost. 
Pro PVST+ může existovat max 128 STP instancí.

### Konfigurace STP:
```
spanning-tree mode pvst/rapid-pvst
spanning-tree vlan 10 root primary/secondary	 (nastavení root brdge)
```
## Princip a konfigurace EtherChannelu
Technologie pro agregaci linek. Používá se na switchi/routeru k rozložení zátěže nebo 
zvýšení propustnosti na linkách. Do EtherChannelu se může zapojit 2 až 8 linek (kabelů). 
Používá se např. na páteřních spojích.
Je potřeba, aby byly porty stejného typu (half nebo full duplex), stejný stp protokol, rychlosti a byly zařazené do stejné VLANy nebo 
byly v trunk módu. Výhodou je zvýšení propustnosti, 
odolnost vůči výpadkům a nízké náklady (není nutnost nic upgradovat).
Používají se protokoly PaGP (Cisco proprietární, 16 rozhraní) a LACP 
(veřejně dostupný, 16 rozhraní, pouze 8 active).
Z pohledu switche (nebo routeru) pak bude EtherChannel vypadat jako jeden virtuální kabel.

On/On -Static
Desirable/Desirable -PAgP
Desirable/Auto -PAgP
Active/Active -LACP
Active/Passive -LACP

```
int range fa0/10-11
channel-group 1 mode active/on/desirable
exit
int po1 -virtuální rozhraní vytvořené EtherChannelem
switchport mode trunk
switchport allowed vlan 10
```

## ACL (Access Control List)
Seznam pravidel, který jedná o řízení nebo identifikaci přístupu k nějakému objektu. Nejčastější použití je pro řízení (omezování) síťového provozu, tedy pro filtrování paketů.
- jako základní síťová bezpečnost k blokování nebo povolení (routovaného) provozu
- ke kontrole šířky pásma
- vynucení síťových politik
- identifikaci nebo klasifikaci provozu (pro QoS, NAT apod.)
Dělíme na Standard a Extended
###Standard
-Identifikuje pouze source adresu
-1-99
###Extended
Identifikuje jak source tak destination adresu a umí identifikovat i porty
-100-199
```
access-list 10 deny 192.168.1.0 0.0.0.255

nebo

ip access-list standard 10
deny 192.168.1.0 0.0.0.255
```

## Příkazy pro nastavení Cisco switche
```
copy running-config startup-config	    (uložit aktuální konfiguraci)
show mac-address-table				    (ukáže MAC tabulku)
show running-config				        (ukáže aktuální konfiguraci)
switchport port-security			    (nastavení port security)
clock set hh:mm:ss day:month:year		(nastavení času)
banner motd ……					        (banner se ukáže při zapnutí sw)
enable password ……				        (nastavení hesla)
enable secret ……				    	(zahashované heslo)
```
```
VLAN                                
show vlan brief					    (ukáže správu VLAN)
vlan 10								(vytvoření VLAN)
int vlan 10							(vstup na rozhraní VLAN)
switchport mode trunk/access		(switchport mode)
```

## Zabezpečení L2 portů 
https://www.youtube.com/watch?v=Rnq2LM7YY3Y