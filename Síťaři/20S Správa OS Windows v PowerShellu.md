# 20. Správa OS Windows v PowerShellu

PowerShell je automatizace úloh pro různé platformy a rozhraní pro správu konfigurace, která se
skládá z prostředí příkazového řádku a skriptovacího jazyka. Na rozdíl od většiny prostředí, která
přijímají a vracejí text, je PowerShell postaven nad modulem CLR (Common Language
Runtime) .NET a přijímá a vrací objekty .NET. Tato zásadní změna přináší zcela nové nástroje a
metody pro automatizaci.

Zapíná se napsáním PowerShell do příkazové řádky ve windows.
##  Základní příkazy

- cls - vyčistí příkazovou řádku PS, cls je alias pro Clear-Host
- Get-Alias - Vypíše seznam použitelných aliasů v PS
- Get-History - vypíše historii zadaných příkazů
- .\názevSouboru.přípona - otevře soubor (Vždycky zapínejte PowerShell jako správce,
jinak to nic nebude umět)
- PowerShell ISE - je hlavně pro psaní scriptů
- Start-Transcript - vše co člověk napíše a PS vypíše se uloží do texťáku - není nutné, ale
lepší pro správu
- Get-PSDrive - vypíše dostupné disky
- Get-Help *jakýkoliv příkaz* - vypíše informace o daném příkazu
- Get-Help Get-Command -Examples - vypíše možné použití příkazu
- Get-Command -noun S* - Vypíše všechny příkaz u kterých začíná P.Jméno “S”
- Get-Command -noun service - Vypíše pouze příkazy které mají P.Jméno service
- Get-Service - vypíše všechny dostupné služby. S jednotlivými službami můžeme
manipulovat
- Get-Process - vypiše seznam aktivních procesů
- Start-Process notepad.exe - zapne process
- Stop-Process -Name "NázevProcesu" -Force - ukončí proces
- Get-Process -Name Calculator | Get-Member - vypiš mi proces kalkulačka | (a zároveň)
mi vypiš jeho použitelné vlastnosti a metody
- Get-Process -Name Calculator | Select-Object \* - vypiš mi proces kalkulačka | (a zároveň)
mi vypiš detailně jeho vlastnosti
## Proměnné

- PS C:\Windows\System32> $promenna = 123
- PS C:\Windows\System32> $promenna
> 123
- $promenna2 = Get-Process Calculator
- $promenna
- $promenna2.\*TAB\* - vypíše po jednom vlastnosti proměnné
- $promenna2.kill() - vypne kalkulačku, ale proměnná bude dál existovat
## Cmdlety

Cmdlet patří mezi specializované příkazy v prostředí PowerShellu, které implementují specifické
funkce. Cmdlety jsou pojmenované tak, že začínají slovesem , pak následuje znak pomlčka a pak je
podstatné jméno ( Get-ChildItem ), tento styl pojmenování dovoluje výstižnější pojmenování
jednotlivých příkazů. Cmdlety jako výsledek mohou vrátit objekt a kolekce (případně pole objektů).

Cmdlet může být napsán v jakémkoliv jazyce, který podporuje platformu .NET (například C#,
VB.NET, IronPython, PHP, J# a jiné).

- Objekty, roury, aliasy

## OBJEKTY

K vytvoření objektu v PS je nejprve zapotřebí použít cmdlet *_New-Object_* k vytvoření počátečního
objektu. Tento příkaz vytvoří .NET nebo COM objekt ze sortimentu tříd. Klasický objekt je .NET
založený na Objektu nebo PSObjektu. Avšak PSObjekt je preferovaný kvůi problémům, které mohou
nstat při přidávání vlastností k objektu založeného na třídě Objekt.

K vytvoření objektu založeného na PSObjektu potřebujete použít New-Object s –TypeName
parametrem, abyste specifikovali typ/třídu objektu.

$system = New-Object -TypeName PSObject
Když spustíte tento příkaz, vygeneruje to PSCustomObject a zapíše se do proměnné $system
## ROURY

Roura zapojí více příkazů a jeden příkaz, předává svůj výstup dalšímu příkazu, ten dalšímu a to až
do výsledku na obrazovce.

Jednotlivé příkazy nám odděluje 
## ALIASY

Rutina Get-Alias získá aliasy v aktuální relaci. To zahrnuje vestavěné aliasy, aliasy, které jste
nastavili nebo importovali, a aliasy, které jste přidali do svého profilu PowerShell.

Ve výchozím nastavení *_Get-Alias_* alias a vrací název příkazu. Při použití parametru Definice získá
Get-Alias název příkazu a vrací jeho aliasy.

? Get-Alias
[[-Name] <String[]>]
[-Exclude <String[]>]

[-Scope <String>]
[<CommonParameters>]
? Get-Alias
[-Exclude <String[]>]
[-Scope <String>]
[-Definition <String[]>]
[<CommonParameters>]
- Přístup k souborovému systému, registru a účtům

## REGISTRY

*New-Item -Path "HKCU:\brambora" -* vytvoří nový registr
*New-ItemProperty -Path "HKCU:\brambora" -Name Pokus -Value 12345 -PropertyType* string -
přidáme vlastnosti registru

*Set-ItemProperty -Path "HKCU:\brambora" -Name Pokus -Value 54321 -* změna vlastností
registru
*Get-Item -Path HKCU:\Brambora -* vypíše hodnoty registru
*Remove-ItemProperty -Path HKCU:\Brambora -name pokus -* Vymaže hodnotu registru
*Remove-Item -Path HKCU:\Brambora -* vymaže registr

## UŽIVATELÉ

*Get-LocalUser -* vypíše seznam uživatelů
**New-LocalUser "Pepa" -Password 123456 -FullName "Pepa Z Depa" -Description "Pokusný
králík" -** Vytvoří nového uživatele Pepa
*Add-LocalGroupMember -Group "Users" -Member "Pepa" -* přídá uživatele pepa do skupiny
Users
*Remove-LocalUser -Name "Pepa" -* odstraní uživatele

více info => Get-Help LocalUser / Get-Help LocalGroup
- Práce s ACL
*_Set-Acl_* mění popis zabezpečení určité položky, jako je složka nebo klíč registru, aby odpovídal
hodnotám popisu zabezpečení, které jsi doplnil.

Chcete-li použít *_Set-Acl_* , použijte parametr *_Path_* nebo *_InputObject_* k identifikaci položky, jejíž
popis zabezpečení chcete změnit. Potom pomocí parametrů *_AclObject_* nebo *_SecurityDescriptor_*
zadejte popis zabezpečení, které mají hodnoty, které chcete použít. *_Set-Acl_* použije použití popis
zabezpečení.

Set-Acl
[-Path] <String[]>
[-InputObject] <PSObject>
[-AclObject] <Object>
[-ClearCentralAccessPolicy]
[-Passthru]
[-Filter <String>]

[-Include <String[]>]
[-Exclude <String[]>]
[-WhatIf]
[-Confirm]
[<CommonParameters>]
- Přístup k WMI (cmdlet pro wmi, získání informací), Získávání informací o

## Objektech

Get-CimInstance -ClassName Win32_Desktop #Tato funkce vrátí informace pro všechny pracovní plochy, ať už jsou používány.
Get-CimInstance -ClassName Win32_BIOS #Třída WMI Win32_BIOS vrátí poměrně kompaktní a úplné informace o systému BIOS v místním počítači.
Get-CimInstance -ClassName Win32_Processor | Select-Object -ExcludeProperty "CIM*"
- Obecné informace o procesoru můžete načíst pomocí Win32_Processor třídy WMI, i
když budete pravděpodobně chtít tyto informace filtrovat
- *Get-CimInstance -ClassName Win32_ComputerSystem -* Výpis výrobce a modelu počítače
- *Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object -Property *user
-** Výpis místních uživatelů a vlastníků
- *Get-CimInstance -ClassName Win32_LocalTime* - Získání místního času z počítače
- **Get-CimInstance -ClassName Win32_Service | Select-Object -Property
Status,Name,DisplayName -** Pokud chcete zobrazit stav všech služeb v určitém počítači,
můžete použít Get-Service rutinu místně. Pro vzdálené systémy můžete použít
Win32_Service třídy WMI. Pokud použijete Select-Object k filtrování výsledků na stav,
názeva Zobrazovanýnázev, bude výstupní formát téměř totožný s tímto formátem Get-
Service
- Clipboard (schránkou – ctrl + c/v)

- *_Set-Clipboard -Value "Tohle je pokus"_*
*-* vloží tento text do schránky a když pak někde
zmáčnete ctrl+v tak se vloží “Tohle je pokus”
- *_Get-Date | Set-Clipboard_*
*-* “05/22/2019 23:07:21”
- *_Get-Date |Out-String | Set-Clipboard_* - "středa 22. května 2019 23:07:54”

```
Autor: Zdražil Patrik
Datum: 6. 5. 2022
```