# USL liga – demo

- index.html – samostojna demo stran (odpri z dvoklikom v brskalniku). Objavljena na https://usl-liga-demo.vercel.app
- banner-ozadje-2560.jpg – grafika v ozadju modre glave (2560 × 600, 122 kB); banner-grafika-2560.jpg je različica s fotografijami
- usl-liga-blok.html – ista koda brez ovoja strani; to prilepiš v WPBakery element "Raw HTML" na ssum.um.si

Podatki: Google Sheet https://docs.google.com/spreadsheets/d/1JStZjW54G6rn_6LgHocSUxJDWlfMIqBjkm_V6ni3dik/edit
(listi: Košarka, Nogomet, Odbojka M, Odbojka Ž, Ekipe – imena listov se morajo ujemati s SPORTS v kodi)

Kaj spremeniš v kodi:
- grafika v glavi: atribut data-banner na <div id="usl-liga"> (na ssum.um.si vpiši poln URL slike iz WP medijske knjižnice, npr. https://ssum.um.si/wp-content/uploads/.../banner-ozadje-2560.jpg; prazen atribut = glava je enobarvno modra)
- barve: spremenljivke --usl-* na vrhu <style>, uskladjene s ssum.um.si (--usl-blue #016085, --usl-dark #014a66, --usl-light #a0ceef, --usl-sand #ffde9c)
- ekipe se izrišejo kot barvni krogec s kratico in polnim imenom iz stolpca ime; stolpec logo_url se ne uporablja več
- točkovanje in razvrstitev: var RULES v <script> – usklajeno s Pravilnikom USL UM 2026/2027 (košarka 2/0, nogomet 3/1/0, odbojka 2/0 na dva dobljena niza; razvrstitev po razliki oz. količniku, nato po medsebojni tekmi)
- neopravičen izostanek: v stolpec opomba napiši besedo, ki vsebuje »neopravičen« – koda poražencu odbije 1 točko (vzorec var KAZEN v <script>); samo »Brez boja« kazni ne sproži
- končnica: var PLAYOFF v <script> – koliko mest nad črto se uvrsti v končnico (0 = brez črte); po Pravilniku se v četrtfinale uvrsti prvih 8, zato pusti 8. Črta se izriše samo, če ima lestvica več ekip od te številke
- športi: var SPORTS v <script>

index.html se generira iz usl-liga-blok.html (blok + ovoj strani s pisavo Ubuntu Sans), zato spreminjaj samo usl-liga-blok.html in index.html obnovi iz njega.
