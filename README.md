# USL liga – demo

- index.html – samostojna demo stran (odpri z dvoklikom v brskalniku). Objavljena na https://usl-liga-demo.vercel.app
- banner-ozadje-2560.jpg – grafika v ozadju modre glave (2560 × 600, 122 kB); banner-grafika-2560.jpg je različica s fotografijami
- usl-liga-blok.html – ista koda brez ovoja strani; to prilepiš v WPBakery element "Raw HTML" na ssum.um.si
- ekipe.html in usl-ekipe-blok.html – druga, samostojna stran s člani ene ekipe (svoj blok, svoja
  koda); z razporedom si ne delita ničesar razen videza, zato ju spreminjaš ločeno
- strelci.csv, kazni.csv, clani_*.csv – datoteke koordinatorja lige. V repozitoriju jih ni (.gitignore)
  in tudi na Vercel ne gredo (.vercelignore), ker vsebujejo imena študentov; na svojem računalniku jih
  imej v tej mapi, na ssum.um.si pa v medijski knjižnici
- demo-strelci.csv, demo-kazni.csv, demo-clani-*.csv – iste postavitve z izmišljenimi imeni, za demo
  na Vercelu

**Bloka sta pripravljena za ssum.um.si**: v atributih data-strelci, data-kazni in data-igralci so
pravi naslovi datotek iz medijske knjižnice. index.html in ekipe.html se iz njiju generirata tako,
da se ti naslovi zamenjajo za datoteke demo-*, povezavi med stranema pa za krajevni imeni – tako na
Vercelu ni nobenega pravega imena. Generator preveri, da v demo straneh ni ostal noben pravi naslov.

Podatki: Google Sheet https://docs.google.com/spreadsheets/d/1JStZjW54G6rn_6LgHocSUxJDWlfMIqBjkm_V6ni3dik/edit
(listi: Košarka, Nogomet, Odbojka M, Odbojka Ž, Ekipe – imena listov se morajo ujemati s SPORTS v kodi)

Kaj spremeniš v kodi:
- grafika v glavi: atribut data-banner na <div id="usl-liga"> (na ssum.um.si vpiši poln URL slike iz WP medijske knjižnice, npr. https://ssum.um.si/wp-content/uploads/.../banner-ozadje-2560.jpg; prazen atribut = glava je enobarvno modra)
- barve: spremenljivke --usl-* na vrhu <style>, uskladjene s ssum.um.si (--usl-blue #016085, --usl-dark #014a66, --usl-light #a0ceef, --usl-sand #ffde9c)
- ekipe se izrišejo kot barvni krogec s kratico in polnim imenom iz stolpca ime; stolpec logo_url se ne uporablja več
- točkovanje in razvrstitev: var RULES v <script> – usklajeno s Pravilnikom USL UM 2026/2027 (košarka 2/0, nogomet 3/1/0, odbojka 2/0 na dva dobljena niza; razvrstitev po razliki oz. količniku, nato po medsebojni tekmi)
- predana tekma ali neopravičen izostanek: v stolpec opomba napiši besedo, ki vsebuje »neopravičen«, »predan« ali »brez boja« – koda poražencu odbije 1 točko (vzorec var KAZEN v <script>)
- izstop ekipe iz tekmovanja: preostale tekme pusti v preglednici, vpiši jim rezultat po pravilniku (pri odbojki 2:0 za nasprotnika, nizi 0:25, 0:25) in v opombo dodaj besedo »izstop« – taka tekma se šteje na lestvici, na razporedu in med rezultati pa je skrita (vzorec var SKRIT v <script>). Pod lestvico se samodejno izpiše, katera ekipa je izstopila. Pozor: beseda »izstop« kjer koli v opombi skrije tekmo, zato je pri navadnih tekmah ne uporabljaj
- končnica: var PLAYOFF v <script> – koliko mest nad črto se uvrsti v končnico (0 = brez črte); po Pravilniku se v četrtfinale uvrsti prvih 8, zato pusti 8. Črta se izriše samo, če ima lestvica več ekip od te številke
- športi: var SPORTS v <script>
- strelci in kazni: atributa data-strelci in data-kazni na <div id="usl-liga"> (poln naslov datoteke iz
  medijske knjižnice; prazen atribut = zavihka ni). Zavihek Strelci se izriše samo pri športu iz var
  STRELCI_SPORT (zdaj nogomet), zavihek Kazni pa samo pri športih iz var KAZNI_SPORTS (košarka in
  nogomet; pri odbojki se kazni ne vodijo). Če kazni pri tistem športu ni, zavihek to izpiše
- povezava na ekipo: atribut data-ekipe na <div id="usl-liga"> – naslov strani s člani ekip. Krogci
  ekip v razporedu in na lestvicah postanejo povezave nanjo (ekipa in šport se dodata v naslov).
  Prazen atribut = krogci niso povezave
- člani ekip: atributi data-igralci, data-liga, data-ekipa in data-sport na <div id="usl-ekipe"> v
  drugem bloku; več datotek s člani ločiš z vejico, data-liga pa je naslov za gumb »Nazaj na ligo«

## Strelci in kazni (blok z razporedom)

Podatki ne smejo v Google preglednico, ker imena študentov ne gredo v Googlove storitve.
Datoteki zato nalagaš v medijsko knjižnico na ssum.um.si in ju po vsakem krogu zamenjaš.

- Format: CSV, iz Excela shranjen kot **»CSV UTF-8 (ločeno z vejico)«**. Navadni »CSV« slovenski Excel
  shrani v kodni tabeli Windows-1250 in č, š, ž se sesujejo. Koda sama prepozna BOM ter ločilo
  (podpičje ali vejica), prazne vrstice na koncu odpadejo.
- Postavitev datotek se ne spreminja – koda se prilagaja njima:
  - strelci: stolpce poišče po besedilu glave (fakulteta / Ime in priimek / število golov), zato
    prestavljen stolpec prikaza ne podre. Datoteka ima samo seštevke, zato prikaza po krogih ni.
  - kazni: naslove (»Kazni košarka«, »Kartoni nogomet«, »prepoved igranja«) poišče po besedilu, kjer
    koli v listu, in bere vrstice pod njimi. Stolpec »prepoved igranja« pripada zadnjemu športu na
    levi, stolpec z vrsto kazni pa imenu levo od sebe. Ime v obliki »Lan Pišek (MF)« se razdeli na
    igralca in ekipo. Če naslov kdo preimenuje, ostane zavihek prazen – to je prvo mesto za pogledat.
  - pri košarki se vodijo samo tehnične napake, zato se vrstica brez vrste kazni izpiše kot
    »Tehnična napaka«.
- Kazni na lestvico ne vplivajo, ker v datoteki ni ne kroga ne odbitka točk. Odbitek za neopravičen
  izostanek še naprej pride iz stolpca opomba v preglednici (var KAZEN).
- V izvornih datotekah sta Đ in đ zapisana kot islandski eth (Ð, ð); koda ju popravi pri branju,
  datoteke ni treba spreminjati.
- Menjava datoteke: WordPress ob nalaganju istega imena naredi novo datoteko (strelci-1.csv …) in
  naslov se spremeni. Z vtičnikom **Enable Media Replace** datoteko zamenjaš na mestu in naslov
  ostane isti; brez njega je treba po vsakem krogu popraviti atribut v bloku. Naložena datoteka je
  javno dostopna v celoti.

## Člani ekipe (druga stran)

Člani ekip so svoja stran s svojim blokom `usl-ekipe-blok.html` in svojim korenskim elementom
`<div id="usl-ekipe">`. Z blokom razporeda nimata skupne kode, zato se lahko spreminjata vsak zase.

Stran prikaže **eno samo ekipo pri enem športu**, brez menija za izbiro – katero, pove naslov
povezave, tako da povezava pelje naravnost na ekipo:

    https://ssum.um.si/clani-ekip/?ekipa=FERI&sport=nogomet

Ena sama stran v WordPressu torej streže vse ekipe; narediš jo enkrat, povezave pa se razlikujejo
samo po koncu naslova. Za `sport` so dovoljene vrednosti `kosarka`, `nogomet`, `odbojka-m` in
`odbojka-z` (šumniki, presledki in podčrtaji niso pomembni), namesto iskalnega dela pa dela tudi
zapis z lojtro, npr. `#FERI-nogomet`. Če bi kdaj hotel za posamezno ekipo pravo svojo stran, pusti
naslov pri miru in kratico vpiši v atributa `data-ekipa` in `data-sport`.

Pod seznamom je gumb »Nazaj na ligo« (naslov iz `data-liga`; če ga ni, se pokaže gumb za korak nazaj po
zgodovini, kadar je obiskovalec prišel s povezave). Glava z grbom in imenom fakultete je poravnana
na sredino, tako kot glave na strani z lestvicami.

**Prvi zapisani član je kapetan** in je posebej označen; pri ženskih disciplinah se izpiše
»igralke« in »kapetanka«. Če ekipe ni na listu Ekipe, stran to pove, prav tako če ekipa pri tistem
športu nima prijavljenih članov; brez ekipe v naslovu izpiše »Ekipa ni izbrana«, podrobnosti za
urednika pa gredo v konzolo brskalnika.

- Iz Google preglednice ta stran vzame samo list Ekipe (kratica, ime, barva) – tam osebnih podatkov ni.
- `data-igralci` sprejme več datotek, ločenih z vejico, po eno na šport – CSV iz Excela ohrani samo
  tisti list, ki je bil odprt ob shranjevanju, zato jih je toliko:
  `data-igralci="…clani_kosarka.csv, …clani_nogomet.csv, …clani_odbojka-m.csv, …clani_odbojka-z.csv"`
  Šport se prebere iz vsebine (stolpec Disciplina), ne iz imena datoteke.
- Postavitev je enaka kot v datoteki koordinatorja: v stolpcu A je disciplina ali zaporedna številka
  igralca, v stolpcu B pa kratica ekipe ali ime igralca. Kratica se upošteva samo, če obstaja na listu
  Ekipe, zato odvečne vrstice ne motijo. Disciplina »Odbojka moški/ženske« se preslika v Odbojka M
  oziroma Odbojka Ž. Vrstni red v datoteki se ohrani, ker iz njega izhaja kapetan.
- Če `data-igralci` pustiš prazen ali datoteke ni, stran izpiše, da seznami še niso objavljeni.
  Pomni, da je datoteka v medijski knjižnici javno dostopna vsakomur, ki pozna njen naslov.

## Kako na ssum.um.si

1. Pasico `banner-ozadje-2560.jpg` naloži v medijsko knjižnico in kopiraj njen poln naslov.
2. V `usl-liga-blok.html` vpiši ta naslov v atribut `data-banner` na prvem `<div>`.
   Če ga pustiš praznega, je glava enobarvno modra in vse ostalo dela naprej.
3. Nova stran → WPBakery → element **Raw HTML** → prilepi **celotno vsebino**
   `usl-liga-blok.html`, od prve vrstice do konca.
4. Google preglednica mora ostati deljena kot »Anyone with the link – Viewer«.
5. Datoteki s strelci in kaznimi naloži v medijsko knjižnico in njuna naslova vpiši v atributa
   `data-strelci` in `data-kazni`. V tem repozitoriju sta vpisani relativni imeni, ki delata samo
   v demu.
6. Za člane ekip naredi **novo stran** in vanjo z elementom **Raw HTML** prilepi celotno vsebino
   `usl-ekipe-blok.html`, nato v atribut `data-igralci` vpiši naslove datotek s člani. Na ekipo se
   potem povezuješ z naslovom te strani in dodatkom `?ekipa=FERI&sport=nogomet`.

Opomba o slogu: tema ssum.um.si tabelam vsiljuje obrobe, odmike in barvo glave
z `!important` (pravila `table`, `table td`, `table th` v njenem style.css).
Blok jih zato prebija z enako oznako – to je edino mesto v kodi, kjer je `!important`
uporabljen, in prvo mesto za pogledat, če tema kdaj spremeni svoje sloge.

index.html se generira iz usl-liga-blok.html (blok + ovoj strani s pisavo Ubuntu Sans), zato spreminjaj samo usl-liga-blok.html in index.html obnovi iz njega.
