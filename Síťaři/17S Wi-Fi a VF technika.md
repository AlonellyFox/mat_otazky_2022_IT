## Využití Wi-Fi a druhy Wi-Fi připojení (WLAN)

- Wi-Fi alias Wireless Fidelity stojí na základech standartů IEEE 802.11 sloužících k bezdrátové komunikaci v počítačových sítích zejména přenosných zařízení a mobilů, není tedy fyzicky zařízení připojit nějakým kabelem k síti.

## Standardy (802.11, a, b, g, n)

| **Standard** | **Označení** | **Rok[GHz]** | **Pásmo[Mbit/s]** | **Max rychlost** | **Fyzická vrstva** |
| --- | --- | --- | --- | --- | --- |
| IEEE 802.11 | - | 1997 | 2.4 | 2 | DSSS a FHSS |
| --- | --- | --- | --- | --- | --- |
| IEEE 802.11a | Wi-Fi 1 | 1999 | 5 | 54 | OFDM |
| IEEE 802.11b | Wi-Fi 2 | 1999 | 2.4 | 11 | DSSS |
| IEEE 802.11g | Wi-Fi 3 | 2003 | 2.4 | 54 | OFDM |
| IEEE 802.11n | Wi-Fi 4 | 2009 | 2.4/5 | 600 | MIMO OFDM |
| IEEE 802.11y | - | 2008 | 3.7 | 54 | - |
| IEEE 802.11ac | Wi-Fi 5 | 2013 | 5 | 3466.8 | MU-MIMO OFDM |
| IEEE 802.11ad | - | 2012 | 60 | 6757 | - |
| IEEE 802.11ax | Wi-Fi 6 | 2019 | 2.4/5/6 | 10530 | MIMO-OFDM |

- Wi-Fi AX doteď není příliš rozšířené, nejvíce je b, g, n a docela už i ac.

## Parametry

**Frekvence** – počet opakování periodického děje za určitý časový úsek, tady v GHz

**Útlum** – kolikrát se zmenší výkon signálu elektromagnetické vlny rozptylem do prostoru, v dB

**Zisk** – poměr účinnosti přeměny energie vůči nějakému referenčnímu vzorku, v dB

**Kanály** – rozděleno na 13 kanálů, přičemž je vhodné nastavit Wi-Fi tak, aby se navzájem nepřekrývaly – mohou se navzájem rušit, používají se kanály 1,6 a 11

**Dosah** – nejdále, kde se v ideálních podmínkách dostane Wi-Fi signál, ovlivněno zdmi, překážkami, stromy,..

**Rychlost přenosu** – pravděpodobně se myslí propustnost? Teoretická až řády GB, praktická okolo stovky MB, spíše méně

**Výpočet vzdálenosti** – netuším

*Antény* – Slouží k vysílání/přijímání signálu Wi-Fi, jsou buď pouze vysílající/přijímající, s technologií MIMO (Multiple-input multiple-output) je možnost využití dvou a více antén současně, čímž se zvýší propustnost, viz níže.

**Fresnelova zóna** – zóna, v které by neměly být žádné překážky typu strom, auto, oběšený Knápek, protože by mohlo dojít k rušení signálu, např. dva vysílače na panelácích mířící na sebe musí na sebe přímo vidět, jinak se signál bude zkreslovat a rušit

**Šíření VF signálu** – vysokofrekvenční signál má tendenci se zohýbat dle zemské osy, tedy „za obzor&quot;, také dokáže proniknout překážkami, či se od nich odrazit

**Modulace** – mění se ní charakter nosného signálu pomocí signálu modulujícího, upravují se tak pro přenos na větší vzdálenosti, příslušně ovlivňuje nějaký z parametrů nosné volny, existují modulace amplitudové – ASK, frekvenční – FSK a fázové – PSK

**MIMO** – Multiple Input Multiple Output – více antén současně vysílá data místo jediné, zvyšuje přenosovou rychlost, evoluce MU-MIMO umožňuje komunikovat s více zařízeními současně tak, že dejme tomu dvě antény vyhradí pro jedno zařízení a dvě antény pro zařízení druhé, proto mají routery alespoň dvě antény standartně.

```
Autor: Kryštof Sádlík
Update: David Kabeláč
Datum: 18.04.2022
```