# 8 Prezentační nástroj a multimédia

> Číselné soustavy (dvojková, desítková, šestnáctková), jednotky používané v informatice, data a informace,
kapacita, přímý kód, zakódování informace (po bitech, po skupině bitů), propustnost, typy přenosů dat, takt a
frekvence.

---
## TÓN A JEHO CHARAKTERISTIKA
### Tón a zvuk
Zvuk je podélné (nebo příčné) mechanické vlnění, které vyvolává v lidském uchu zvukový vjem. Člověk je schopen vnímat zvuk o frekvenci přibližně od 16Hz do 16Khz. Zvuky
 s menší frekvencí nazýváme infrazvuk a zvuky s vyšší frekvencí ultrazvuk. Tělesa, 
která kmitají pravidelně (periodicky) nazýváme tóny. Nepravidelně kmitající tělesa nazýváme hluk.

**Hluk**
![Hluk](images/hluk.png#gh-light-mode-only)
![Hluk](images/hluk.png#gh-dark-mode-only)

**Tón**
![Tón](images/ton.png#gh-light-mode-only)
![Tón](images/ton.png#gh-dark-mode-only)

## DIGITALIZACE ZVUKU
Každý akustický signál je spojitý a při jeho záznamu do analogového zařízení je převeden na jinou spojitou veličinu. Každý přenos takového signálu způsobuje ztrátu kvality, nárůst šumu, zkreslení, rušení a zlepšování kvality přenosu má jenom omezené možnosti.
Proto převádíme analogový signál na digitální. Digitalizace zvuku s sebou pokaždé nese ztrátu informace.

### Vzorkování
Pro převod analogového signálu na digitální je třeba signál nejprve vzorkovat, tj. zaznamenat amplitudu signálu pouze v pravidelných časových okamžicích. Vzorky můžou mít jakoukoliv hodnotu. Počtu vzorků (záznamů) za sekundu říkáme vzorkovací frekvence. 

![Vzorkování](images/vzorkovani.png#gh-light-mode-only)
![Vzorkování](images/vzorkovani.png#gh-dark-mode-only)

Používané vzorkovací frekvence:
* 8 kHz: telefony, vysílačky
* 16 kHz: VoIP, aj.
* 22,05 kHz: digitalizace zvukových formátů počátku 20.století
* 32 kHz: miniDV, audio a pod.
* 44,1 kHz: AudioCD
* 48 kHz: profesionální záznam zvuku (magnetofony, mix pulty)
* 96 kHz: DVD-Audio, Blue-ray

### Nyquistův–Shannonův teorém
Aby při vzorkování nedošlo k tzv. aliasingu (výsledný signál obsahuje frekvence, které v něm vůbec nebyli), musí být Nyquist–Shannonova teorému zvolit dvakrát větší vzorkovací frekvenci, než je frekvence nejvyšší. K zabránění aliasingu se ještě
před vzorkováním používá filtr typu dolní propust. 

Rozdělení audioformátů
Bezestrátová komprese
I po komprimaci zachovávají soubory identickou informaci s předlohou. Nedochází tak ke ztrátě kvality obrazu. Obvykle není tak účinná jako ztrátová komprese dat.

WAV (Wave format) byl vytvořen firmou Microsoft pro platformu PC/Windows. Dnes se používá jako univerzální formát. Data uvnitř jsou nezkomprimované navzorkované zvuky podobně jako na Audio CD. Zvuk může být mono či stereo, s různou frekvencí vzorkování a bitovou hloubkou 8 nebo 16 bitů. CD kvalita je Stereo, 44100 Hz, 16 b.
FLAC
Free lossless Audio Codec, kompresní poměr kolem 60%
Kodek FLAC
WMA
Bezeztrátový formát pro Windows Media
Kodek WMA 9 lossless

Ztrátová komprese
Při kompresi zahazují část grafické informace. Používá se tam, kde je možné ztrátu některých informací tolerovat a kde nevýhoda určitého zkreslení je bohatě vyvážena velmi významným zmenšením souboru.
MP3
MP3 (MPEG-1 Audio Layer-3) je standardní technologie a formát pro kompresi zvuku do velmi malého souboru (poměr 1:12 při zachování kvality). Míru komprimace udává takzvaný bitrate, počet bitů, které při přehrávání "spotřebujete" za sekundu. Nejčastěji se setkáte s bitrate 128 Kb/s, občas 192 Kb/s nebo i se soubory s proměnným bitrate. Komprese je založena na ořezání záznamu o zvuky, které lidský mozek stejně nemůže vnímat. Můžete se setkat i se starší verzí MP2. Vhodný pro přenos audio souborů po Internetu.

VQF 
je zvukový formát vyvinutý firmou Yamaha, je to alternativní řešení formátu MP3. Dosahuje lepší komprese než MP3. Není příliš rozšířen.
OGG
je nový formát založený na podobném modelu jako MP3, nicméně obsahuje řadu vylepšení. Například jde snížit bitrate bez nutnosti soubor překódovat. Díky své vysoké kvalitě se na Internetu prosazuje více a více. Používá ho například i ČRo. Jeho předností je i otevřená licence.

Základní pojmy z oblasti grafiky a videa
Digitální Video informace je posloupnost obrázků, které se se rychle střídají tak, aby vznikl dojem plynulého pohybu objektů ve videu. Jeden obrázek se nazývá snímek. Videoinformace se ukládá do multimediálních souborů, jejichž součástí není jenom obraz, ale i zvuk,případně titulky a metainformace.

Softwarové funkce zajišťující kompresi a dekompresi videa jsou zpravidla ukládány v oddělených souborech nazývaných kodek, z počátečních písmen slov KOdér - DEKodér (v angličtině codec)

**Rozlišení** - Počet pixelů videa na šířku a na výšku. Často používaná rozlišení jsou pro malá videa 320×240 a pro větší videa 640×480., u DVD videa bývá 720×576. Vetší rozlišení (například pro HDTV) již nebudou z hlediska tohoto kurzu tak významná. 

**Poměr stran** - Anglicky aspect ratio, podíl šířky a výšky snímku videa. Nejčastější poměr stran je 4:3, jako u klasické televize, u HDTV je to 16:9. 

**Prokládání** - Pro zvýšení iluze vyššího rozlišení při menším datovém toku se někdy používá prokládané řádkování. V jednom snímku jsou obsažené obrazové informace pouze z lichých řádků a v následujícím snímku pouze ze sudých. Tato technologie se používala v analogové televizi a u digitálního videa měla význam v minulosti, při malých datových rychlostech internetového připojení a malých kapacit úložných médií. U prokládaného řádkování polovina informace chybí, což u statickým scén nevadí, protože se informace chybějící poloviny řádků doplní z předchozího snímku. U rychlých pohybů se obrázek u prokládaného videa jakoby rozostří do sudých a lichých řádků, což je zřetelné obzvláště u ostrých hran s kontrastními přechody. Pokud nám nevadí vyšší datový tok, je lépe se prokládanému řádkování vyhnout. 

Frame Rate 	Rychlost snímků za sekundu, jednotkou je fps (Frames per second). Dnes je standardem 25 fps nebo 30 fps. 

Grafické a zvukové formáty

Bezeztrátové
* BMP formát bitmapového obrázku a jeho výhodou je jeho extrémní jednoduchost a dobrá dokumentovanost
* GIF (Graphic Interchange Format) je grafický formát určený pro rastrovou grafiku vytvářenou v počítačích. GIF používá bezeztrátovou kompresi LZW a umožňuje také jednoduché animace. GIF má velké omezení v maximálním počtu 256 (8 bitů) současně použitých barev barevné palety v jednom rámci.
* PNG (Portable Network Graphics) je grafický formát určený pro bezeztrátovou kompresi rastrové grafiky. Byl vyvinut jako zdokonalení a náhrada formátu GIF.
* RAW je soubor nijak neupravených digitalizovaných dat ze snímače digitálního fotoaparátu. Formát souboru RAW není nikým definován a soubory z různých fotoaparátů (i od stejné firmy) se mohou značně lišit.
Ztrátové
JPEG (Joint Photographic Experts Group) je standardní a nejrozšířenější metoda ukládání snímků se ztrátovou kompresí používaná pro ukládání digitálních obrázků ve fotorealistické kvalitě.
HEIF je přípona nového kontejneru pro ukládání obrázků pomocí až dvakrát efektivnější komprese než JPEG (beze ztráty kvality),[1] může obsahovat kódování:
HEIC (High Efficiency Image File Format) je nový formát, který umožňuje vyšší kompresi beze ztráty kvality (používá ho např. fotoaparát v iPhone od roku 2017),[1] je založena na proprietárním kódování H.265
AVIF je obdoba formátu HEIC, ale místo uzavřeného H.265 je použit otevřený formát kódování AV1 (Gimp jej podporuje od konce roku 2020)[2]

Microsoft Powerpoint
Microsoft PowerPoint je nástroj na tvorbu prezentací z kancelářského balíku Microsoft Office od společnosti Microsoft. Prezentace mohou sloužit pro ukázku různých produktů, služeb, či jiných aktivit. Starší verze používaly koncovku „.ppt“.
Tvorba prezentace
Obsah by měl být stručný, heslovitý, případné věty krátké, srozumitelné. srozumitelnost a viditelnost obrázků před prezentací. Videa pouze krátká, k tématu. Minimalizovat použité animace a přechody – volit krátké a přehledné animace stejné v celé prezentaci.
Šablony 
Zajišťují rozložení textu. Šablonu vybíráme tak aby byl text a obrázky čitelné a neprolínaly se s prezentací.