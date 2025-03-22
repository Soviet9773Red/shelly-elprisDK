# shelly-elprisDK
DK1-2 Nordpool spotpris kontrol for Shelly-enheder

[![Licens: AGPL v3](https://img.shields.io/badge/Licens-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

**shelly-elprisDK (tilpasset til DK1-2)** er et projekt til at styre Shelly-enheder.  
Det er baseret på <a href="https://github.com/jisotalo/shelly-porssisahko-en">shelly-porssisahko-en</a> version 3.1.1 og er tilpasset til danske elområder (DK1-2) med API-data fra [Elprisenligenu.dk]([https://www.elprisetjustnu.se/](https://www.elprisenligenu.dk/)).

Udviklet af [@Soviet9773Red](https://github.com/Soviet9773Red) med kærlighed og taknemmelighed til [Jussi Isotalo](http://jisotalo.fi) / [@jisotalo](https://github.com/jisotalo) for den fantastiske kode.  
*Stort tak til GPT o1 – min bedste AI, som for altid vil være en del af koden (og nævnes i testamentet)!*

## Funktionalitet
- Hentning af elpriser fra et dansk API (Nordpool/elprisenligenu.dk).  
- Beregning af de laveste, højeste og gennemsnitlige elpriser samt identifikation af timen med den laveste og højeste pris.  
- Visning af enhedens aktuelle status, konfiguration og historik.  
- Understøttelse af opdatering af konfiguration og styring af udgange (outputs).

## Egenskaber
- Optimeret og minificeret kode til Shelly-enheder.  
- Tilpasset til Shelly 1.5.0 og 1.4.4 med hensyn til begrænsninger (ingen arrow-funktioner, skabelonstrenge etc.).  
- Enkel HTTP-integration til at hente status, konfiguration og historik.

---

## Vigtig information  
**[shelly-elprisSE](https://github.com/Soviet9773Red/shelly-elprisSE)** er en dansk tilpasning af det finske projekt **[shelly Porssisahko](https://github.com/jisotalo/shelly-porssisahko)**, oprindeligt udviklet til Finland og Baltikum. Denne version bruger det danske elpris-API [Elprisenligenu.dk](https://www.elprisenligenu.dk/) i stedet for [Elering](https://elering.ee/) standarddata.

Bemærk, at der ikke er foretaget globale ændringer i funktionaliteten sammenlignet med originalkoden fra [shelly-porssisahko-en](https://github.com/jisotalo/shelly-porssisahko-en) (ver. 3.1.1). For en fuldstændig manual, se [originalkilden.](https://github.com/jisotalo/shelly-porssisahko-en)

---

## Hovedsaglige ændringer (changelog): 
- **API-kald:**  
  Ændret fra den estiske API-adresse i `.csv`-format ([Elering](https://elering.ee/)) til den danske i JSON-format ([Elprisenligenu.dk](https://www.elprisenligenu.dk/)).  
- **Regioner:**  
  Understøttelse af danske elområder DK1-DK2 er blevet tilføjet, mens Finland og Baltikum er fjernet.  
- **Design:**  
  Justeringer af farveskema og overskrifter i fanerne *Status* og *Settings* for bedre at passe til det danske marked.

For at ændre prisforespørgslen til det danske API har jeg tilføjet to nye funktioner: `bldU` og `pTimeL`, samt ændret den eksisterende funktion `getPrices`.  
I HTTP-serverens endpoint er visse dele modificeret, bortset fra den femte og sjette del.

## 📷 Indstillingsvisning
Her er en illustration af info (status) og konfigurationsvisningen:
<table><tr>
      <td><img src="https://github.com/Soviet9773Red/shelly-elprisDK/blob/main/StatP.jpg" width="500"></td>
      <td><img src="https://github.com/Soviet9773Red/shelly-elprisDK/blob/main/SetP.jpg" width="500"></td>
      </tr>
</table>

## Kom i gang:
1. Installér Shelly og tilslut den til WiFi.  
2. Åbn Shelly Web UI i en webbrowser via din lokale netværksadresse.  
3. Gå til *Scripts*-siden og åbn **Settings -> Firmware -> Update**.  
   Opdater firmware til version **1.4.4** eller højere "stable". Ældre versioner understøttes ikke.  
4. Gå til **Settings -> Location and Time**, vælg tidszonen *Europe/Copenhagen* og klik på *Save Settings*.  
5. Gå til **Settings -> Device name**. Sæt et navn på din enhed. -> *Save*  
6. Åbn linket til scriptet på GitHub:  
👉 [shelly-elprisDK_3.1.1dk-rc.js](https://github.com/Soviet9773Red/shelly-elprisDK/blob/main/shelly-elprisDK_3.1.1dk-rc.js)  
   Vælg *Download* eller kopier råfilen. Gem filen i *Notepad* eller på din computer.  
7. Gå til Scripts → Create script og skriv ElprisetDK som Script name.
Indsæt scriptets tekst, klik på Save og derefter Start.

I konsollen vil du se scriptets resultat, omtrent sådan her:

elpris-DK: v.3.1.1dk-rc<br>
elpris-DK: URL: http://192.168.8.160/script/1<br>
elpris-DK: Getting prices for day 0<br> 
elpris-DK: Getting prices for day 1<br> 
elpris-DK: config for #1 read, enabled: 1  
elpris-DK: config for #2 read, enabled: 0  
elpris-DK: config for #3 read, enabled: 0  
elpris-DK: logic for #1 done, cmd: true -> output: true  

8. Åbn scriptets HTTP-endpoint  
   Kopier HTTP-adressen fra konsollen, f.eks. `http://192.168.8.160/script/1`  
   Åbn linket i en ny fane i din webbrowser.  
   Adressen kan variere, men strukturen er: `http://xxx.xxx.x.xxx/script/N` hvor `N` er scriptets ID-nummer.  
   Og `/script/N` er til sidst.

9. Konfigurer scriptets parametre i henhold til [manualen](https://github.com/jisotalo/shelly-porssisahko-en)

---

### Hvis du har problemer med at gemme eller starte scriptet:
- Stop alle scripts. Fjern markeringen af *Run on startup*.  
- Gå til **Settings -> Reboot Device**.  
- Sæt *Run on startup* igen.  
- Hvis du har andre aktive scripts – stop dem.  
- Slet store scripts, hvis du allerede har flere gemt på enheden.  
- Ryd KVS og fjern unødvendige nøgler.

---

### Test

Scriptet er testet på:  
**Shelly Plus 1, Plus 1PM, Pro 3, Plus Plug S**  
Ifølge [Jussi Isotalo](http://jisotalo.fi) [fungerer](https://github.com/jisotalo/shelly-porssisahko-en?tab=readme-ov-file#shelly-devices) det også på:  
**Shelly Plus 2PM, Pro 1, Pro 2, Pro 4PM, Pro 3EM + Switch Add-on, Plus UNI, Plus 1 Mini**  
Jeg har dog ikke selv testet disse.

Jeg har testet scriptet på mine egne enheder og bemærket, at det ikke altid er stabilt ved prisforespørgsler – det kan nogle gange stoppe på grund af hukommelsesoverløb.

Derfor er jeg meget taknemmelig for enhver, der kan hjælpe med test og fejlrapportering.

Netop af denne grund har versionsnummeret endelsen rc (release candidate).


### Støt projektet!
Jeg bliver tit sulten, når jeg koder – 🍔 [giv mig en Big Mac og en kaffe](https://buymeacoffee.com/soviet9773red)

[![Big Mac](https://img.shields.io/badge/Buy%20me%20a%20🍔-Big%20Mac-yellow?style=for-the-badge)](https://buymeacoffee.com/soviet9773red)

Tak skal du have!

