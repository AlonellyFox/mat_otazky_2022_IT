# 20. Spr�va OS Windows v PowerShellu

PowerShell je automatizace �loh pro r�zn� platformy a rozhran� pro spr�vu konfigurace, kter� se
skl�d� z prost�ed� p��kazov�ho ��dku a skriptovac�ho jazyka. Na rozd�l od v�t�iny prost�ed�, kter�
p�ij�maj� a vracej� text, je PowerShell postaven nad modulem CLR (Common Language
Runtime) .NET a p�ij�m� a vrac� objekty .NET. Tato z�sadn� zm�na p�in�� zcela nov� n�stroje a
metody pro automatizaci.

```
Zap�n� se naps�n�m PowerShell do p��kazov� ��dky ve windows.
```
##  Z�kladn� p��kazy

```
- cls - vy�ist� p��kazovou ��dku PS, cls je alias pro Clear-Host
- Get-Alias - Vyp�e seznam pou�iteln�ch alias� v PS
- Get-History - vyp�e historii zadan�ch p��kaz�
- .\n�zevSouboru.p��pona - otev�e soubor (V�dycky zap�nejte PowerShell jako spr�vce,
jinak to nic nebude um�t)
- PowerShell ISE - je hlavn� pro psan� script�
- Start-Transcript - v�e co �lov�k nap�e a PS vyp�e se ulo�� do tex��ku - nen� nutn�, ale
lep�� pro spr�vu
- Get-PSDrive - vyp�e dostupn� disky
- Get-Help *jak�koliv p��kaz* - vyp�e informace o dan�m p��kazu
- Get-Help Get-Command -Examples - vyp�e mo�n� pou�it� p��kazu
- Get-Command -noun S* - Vyp�e v�echny p��kaz u kter�ch za��n� P.Jm�no �S�
- Get-Command -noun service - Vyp�e pouze p��kazy kter� maj� P.Jm�no service
- Get-Service - vyp�e v�echny dostupn� slu�by. S jednotliv�mi slu�bami m��eme
manipulovat
- Get-Process - vypi�e seznam aktivn�ch proces�
- Start-Process notepad.exe - zapne process
- Stop-Process -Name "N�zevProcesu" -Force - ukon�� proces
- Get-Process -Name Calculator | Get-Member - vypi� mi proces kalkula�ka | (a z�rove�)
mi vypi� jeho pou�iteln� vlastnosti a metody
- Get-Process -Name Calculator | Select-Object \* - vypi� mi proces kalkula�ka | (a z�rove�)
mi vypi� detailn� jeho vlastnosti
```
## Prom�nn�

```powershell
- PS C:\Windows\System32> $promenna = 123
- PS C:\Windows\System32> $promenna
> 123
```
```powershell
- $promenna2 = Get-Process Calculator
- $promenna
- $promenna2.\*TAB\* - vyp�e po jednom vlastnosti prom�nn�
- $promenna2.kill() - vypne kalkula�ku, ale prom�nn� bude d�l existovat
```
## Cmdlety

*Cmdlet* pat�� mezi specializovan� p��kazy v prost�ed� PowerShellu, kter� implementuj� specifick�
funkce. Cmdlety jsou pojmenovan� tak, �e za��naj� *slovesem* , pak n�sleduje znak *poml�ka* a pak je
*podstatn� jm�no* ( *Get-ChildItem* ), tento styl pojmenov�n� dovoluje v�sti�n�j�� pojmenov�n�
jednotliv�ch p��kaz�. Cmdlety jako v�sledek mohou vr�tit *objekt a kolekce* (p��padn� pole objekt�).

Cmdlet m��e b�t naps�n v jak�mkoliv jazyce, kter� podporuje platformu .NET (nap��klad C#,
VB.NET, IronPython, PHP, J# a jin�).

- Objekty, roury, aliasy

## OBJEKTY

K vytvo�en� objektu v PS je nejprve zapot�eb� pou��t cmdlet **_New-Object_** k vytvo�en� po��te�n�ho
objektu. Tento p��kaz vytvo�� *.NET* nebo *COM* objekt ze sortimentu t��d. Klasick� objekt je *.NET*
zalo�en� na Objektu nebo PSObjektu. Av�ak PSObjekt je preferovan� kv�i probl�m�m, kter� mohou
nstat p�i p�id�v�n� vlastnost� k objektu zalo�en�ho na t��d� Objekt.

K vytvo�en� objektu zalo�en�ho na PSObjektu pot�ebujete pou��t *New-Object* s *�TypeName*
parametrem, abyste specifikovali typ/t��du objektu.

```powershell
$system = New-Object -TypeName PSObject
Kdy� spust�te tento p��kaz, vygeneruje to PSCustomObject a zap�e se do prom�nn� $system
```
## ROURY

Roura zapoj� v�ce p��kaz� a jeden p��kaz, p�ed�v� sv�j v�stup dal��mu p��kazu, ten dal��mu a to a�
do v�sledku na obrazovce.

```
Jednotliv� p��kazy n�m odd�luje 
```
## ALIASY

Rutina Get-Alias z�sk� aliasy v aktu�ln� relaci. To zahrnuje vestav�n� aliasy, aliasy, kter� jste
nastavili nebo importovali, a aliasy, kter� jste p�idali do sv�ho profilu PowerShell.

Ve v�choz�m nastaven� **_Get-Alias_** alias a vrac� n�zev p��kazu. P�i pou�it� parametru Definice z�sk�
Get-Alias n�zev p��kazu a vrac� jeho aliasy.

```powershell
? Get-Alias
[[-Name] <String[]>]
[-Exclude <String[]>]
```

```powershell
[-Scope <String>]
[<CommonParameters>]
? Get-Alias
[-Exclude <String[]>]
[-Scope <String>]
[-Definition <String[]>]
[<CommonParameters>]
```
- P��stup k souborov�mu syst�mu, registru a ��t�m

## REGISTRY

**New-Item -Path "HKCU:\brambora" -** vytvo�� nov� registr
**New-ItemProperty -Path "HKCU:\brambora" -Name Pokus -Value 12345 -PropertyType** string -
p�id�me vlastnosti registru

**Set-ItemProperty -Path "HKCU:\brambora" -Name Pokus -Value 54321 -** zm�na vlastnost�
registru
**Get-Item -Path HKCU:\Brambora -** vyp�e hodnoty registru
**Remove-ItemProperty -Path HKCU:\Brambora -name pokus -** Vyma�e hodnotu registru
**Remove-Item -Path HKCU:\Brambora -** vyma�e registr

## U�IVATEL�

**Get-LocalUser -** vyp�e seznam u�ivatel�
**New-LocalUser "Pepa" -Password 123456 -FullName "Pepa Z Depa" -Description "Pokusn�
kr�l�k" -** Vytvo�� nov�ho u�ivatele Pepa
**Add-LocalGroupMember -Group "Users" -Member "Pepa" -** p��d� u�ivatele pepa do skupiny
Users
**Remove-LocalUser -Name "Pepa" -** odstran� u�ivatele

```
v�ce info => Get-Help LocalUser / Get-Help LocalGroup
```
- Pr�ce s ACL
**_Set-Acl_** m�n� popis zabezpe�en� ur�it� polo�ky, jako je slo�ka nebo kl�� registru, aby odpov�dal
hodnot�m popisu zabezpe�en�, kter� jsi doplnil.

Chcete-li pou��t **_Set-Acl_** , pou�ijte parametr **_Path_** nebo **_InputObject_** k identifikaci polo�ky, jej�
popis zabezpe�en� chcete zm�nit. Potom pomoc� parametr� **_AclObject_** nebo **_SecurityDescriptor_**
zadejte popis zabezpe�en�, kter� maj� hodnoty, kter� chcete pou��t. **_Set-Acl_** pou�ije pou�it� popis
zabezpe�en�.

```powershell
Set-Acl
```
```powershell
[-Path] <String[]>
[-InputObject] <PSObject>
[-AclObject] <Object>
[-ClearCentralAccessPolicy]
[-Passthru]
[-Filter <String>]
```

```powershell
[-Include <String[]>]
[-Exclude <String[]>]
[-WhatIf]
[-Confirm]
[<CommonParameters>]
```
- P��stup k WMI (cmdlet pro wmi, z�sk�n� informac�), Z�sk�v�n� informac� o

## Objektech

```powershell
Get-CimInstance -ClassName Win32_Desktop #Tato funkce vr�t� informace pro v�echny pracovn� plochy, a� u� jsou pou��v�ny.
Get-CimInstance -ClassName Win32_BIOS #T��da WMI Win32_BIOS vr�t� pom�rn� kompaktn� a �pln� informace o syst�mu BIOS v m�stn�m po��ta�i.
Get-CimInstance -ClassName Win32_Processor | Select-Object -ExcludeProperty "CIM*"
```
- Obecn� informace o procesoru m��ete na��st pomoc� Win32_Processor t��dy WMI, i
kdy� budete pravd�podobn� cht�t tyto informace filtrovat
- **Get-CimInstance -ClassName Win32_ComputerSystem -** V�pis v�robce a modelu po��ta�e
- **Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object -Property *user*
-** V�pis m�stn�ch u�ivatel� a vlastn�k�
- **Get-CimInstance -ClassName Win32_LocalTime** - Z�sk�n� m�stn�ho �asu z po��ta�e
- **Get-CimInstance -ClassName Win32_Service | Select-Object -Property
Status,Name,DisplayName -** Pokud chcete zobrazit stav v�ech slu�eb v ur�it�m po��ta�i,
m��ete pou��t Get-Service rutinu m�stn�. Pro vzd�len� syst�my m��ete pou��t
Win32_Service t��dy WMI. Pokud pou�ijete Select-Object k filtrov�n� v�sledk� na stav,
n�zeva Zobrazovan�n�zev, bude v�stupn� form�t t�m�� toto�n� s t�mto form�tem Get-
Service
- Clipboard (schr�nkou � ctrl + c/v)

- **_Set-Clipboard -Value "Tohle je pokus"_** **-** vlo�� tento text do schr�nky a kdy� pak n�kde
zm��nete ctrl+v tak se vlo�� �Tohle je pokus�
- **_Get-Date | Set-Clipboard_** **-** �05/22/2019 23:07:21�
- **_Get-Date |Out-String | Set-Clipboard_** - "st�eda 22. kv�tna 2019 23:07:54�

```
Autor: Zdražil Patrik
Merger: Zdražil Patrik
Datum: 29.4.2022
```