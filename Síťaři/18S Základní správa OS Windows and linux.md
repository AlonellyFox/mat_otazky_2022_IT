# 18. Základní správa OS Windows and linux

# LINUX

## Init 
je program, který se v unixových systémech spouští jako první. Je to rodič všech programů a jeho PID je nejvyšší možné číslo 1 (PID = Process ID).

## Upstart
Upstart je event-based nahrada za /sbin/init deamona, který se stará o nastartování úloh a služeb při bootu, zastavuje je při shutdownu a dohlíží na ně když systém běží.

## Konfigurační soubory
O porti Windowsu, který používá Registry, Linux používá konfigurační soubory. Každá distribuce používá jiné, takže je tady asi těžko vyjmenuju všechny. Konfig. soubory se dají lehce měnit pomocí textového editoru.

## Root
Root je Superuser účet na Unixech a Linuxech. je to uživatelský účet pro administrativní účely a má typicky nejvyšší opravnění v systému. Obyvkle účet root usera je "root", na jméně však nezáleží root účet dělá jeho ID, které je rovno 0.

## Sudo
Sudo neboli SuperUserDO je příkaz, který se používá pro přístup do souborů a k různým operacím. more víš co je sudo ne kkt pičo.

## Sudoers
Sudoers je soubor, kteří admini používají pro nastavivaní systémových práv uživatelů v Uinuxu a Linuxu.

## konfigurace SSH
### Na Ubuntu 
- nainstaluješ openSSH - sudo apt-get install openssh-server
- config file pak edituješ pomocí sudo nano /etc/ssh/sshd_config

### Na Raspberry OS
- sudo systemctl start ssh
- edituješ pomocí sudo nano /etc/ssh/sshd_config (tam si zapni PermitRootLogin)
- sudo service ssh restart

Jak vidíš je to podobné, i na Archi je to doslova to samé, záleží prostě podle distra, protože linux useři jsou speciální vločky a každý musí mít svůj Linux

##Web server
* Apache HTTP Server
* Ngnix Web Server
* Lighttps Web Server
* Caddy Web Server
* A spousta dalších, protože každý musí být speciální vločka

### Apache HTTP Server

```
Asi nejvíce používaný, takže budu řešit jen tento.
```
Defaultně se stránky nacházejí v /var/www což však můžeš změnit.
Potom manipuluješ se soubory - /etc/apache2/ports.conf a /etc/apache2/sites-enabled/*jméno tvojí stránky :)))xdxdsdtaayfdkzj*
Podle distribucí zase záleží kde se soubory nachaźejí ale je to generaly stejné.

## FTP
FTP neboli File Transfer Protocol, slouží pro převod souborů vzdáleně

Na Ubuntu každý používá **VSFTPD**
- sudo apt install vsftpd
- sudo service vsftps status (měl by běžet)
- udělej si usera pro FTP - sudo adduser *ftpuser*
- udělej si podadresář v jeho home adresáři - sudo mkdir /home/*ftpuser*/FTP
- složku nastav aby ji vlastnil nikdo - sudo chown nobody:nogroup /home/*ftpsuser*/FTP
- nastav oprávnění na složku - sudo chmod a-w /home/*ftpuser*/FTP (a = all, w = write)
- udělej další složku - sudo mkdir /home/*ftpuser*/FTP/files
- dej podadresáři files vlastníka *ftpuser* sudo chown *ftpuser*:*ftpuser* /home/*ftpsuser*/FTP/files
- doporučeno je si zálohovat config soubor - sudo mv /etc/vsftpd.conf /etc/vsftpd.conf.orig
- uděláš tam nový config soubor do kterého dáš: 
```
listen=YES
listen_ipv6=NO
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
chroot_local_user=YES
allow_writeable_chroot=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
force_dot_files=YES
pasv_min_port=40000
pasv_max_port=50000

user_sub_token=$USER
local_root=/home/$USER/ftp
```
-pak to jen restartuješ - sudo system restart vsfpd a si hotový
Je pak doporučeno nastavit TLS pro zašifrování dat

# Terminálové příkazy

## Práce se soubory

- pwd - ti řekne kde si
- cd - chození mezi adresáři
- ls - vypíše existující složky/soubory
- touch - udělá soubor
- mkdir - nová složka
- rmdir - maže složku
- cat - výpis textu ze souboru 
- mv - posune soubor (používá se i pro změnu názvu souboru
- cp - kopíruje soubor
- rm - maže soubor
- find - hledá soubory

## Aktualizace

Zas asi záleží na distru takže pro Ubuntu:

- sudo apt-get update nebo
- sudo apt update
- apt list --upgradable - pro výpis dostupných updatů

## Práce s procesy
- ps -au	list all current processes
- command &	run command in the background
- jobs	list current jobs
- bg %1	push job number 1 to the background
- fg %1	bring job number 1 to the foreground
- kill %1	kill process with job number 1
- kill -9 2132	kill process with PID 2132
- Ctrl-C	kill the process running in foreground
- Ctrl-Z	suspend the process running in foreground
- sleep 15	delay execution for 15 seconds
- xclock	place a running clock on your desktop
- sry nechci to překládat

## Logování

Logy se v Linuxu nacháti v /var/log

Některé z nejdůležitějších systémových logů:
- /var/log/syslog
- /var/log/auth.log - logování loginů, root user akcí apod.
- /var/log/kern.log - logování kenel událostí, errory a varování
- /var/log/cron - logování informací o naplánovaných událostech

# WINDOWS Server

## Active Directory - AD
AD je ryze Microsfotí adresářová služba, běží na Windwos serverech a umožňuje adminům spravovat oprávnění a přístup k síťovým zdrojům.

AD ukládá data jako objekty. Objket je jeden element jako třeba uživatel, skupina aplikace nebo zařízení jako tiskárna.

### AD služby 

- Domain Services
- Lightweight Directory Services
- Lightweight Directory Access Protocol
- Certificate Services
- Active Directory Federation Services
- Rights Management Services

Instalace všeho je jak pro debila, přece jenom je to Windows

## NPS
https://www.youtube.com/watch?v=GSAClWmg8y0

## Logování/Monitorování
U Windowsu použiješ Event viewer neboli Prohlížeč událostí (eventvwr.exe)