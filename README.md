# Wie kan wanneer

Een kleine webapp om met een WhatsApp-groep een datum te prikken, zonder dat iemand iets moet installeren.

## Hoe het werkt

1. **Kies de mogelijke dagen** in de kalender. Elke dag krijgt een nummer.
2. **Deel het bericht** in de groep (kopiëren, "Delen…" of "Open in WhatsApp"). Iedereen antwoordt met nummers, bijvoorbeeld `1 3 4`, of `2?` als ze twijfelen.
3. **Plak de antwoorden terug** in de app. Die haalt namen en nummers uit de berichten en laat zien welke dag het best past.

De app begrijpt ook antwoorden als `alles`, `alles behalve 2`, `1-3`, `zaterdag`, `14/11` en `2 misschien`. Je kijkt alles na voor je het toevoegt.

## Privacy

- Planningen worden alleen in de browser van de gebruiker bewaard (`localStorage`). Er is geen server en geen database.
- De pagina laadt niets van andere websites: de lettertypes staan mee in de map `fonts/`. Er zijn geen cookies en geen tracking.
- Iedereen die de link opent, krijgt een eigen, lege planner.

## Bestanden

| Bestand | Waarvoor |
| --- | --- |
| `index.html` | De volledige app (HTML, CSS en JavaScript in één bestand) |
| `manifest.webmanifest` en `icons/` | Icoon en naam als je de site op je beginscherm zet |
| `fonts/` | Barlow Condensed en Hanken Grotesk, onder de SIL Open Font License (zie de `OFL-*.txt`-bestanden) |

## Online zetten met GitHub Pages

1. Maak een **public** repository aan op GitHub (bijvoorbeeld `wie-kan-wanneer`).
2. Upload alle bestanden en mappen uit deze map, zodat `index.html` in de hoofdmap van de repository staat.
3. Ga naar **Settings → Pages**. Kies bij *Source* **Deploy from a branch**, branch **main**, map **/ (root)**, en klik **Save**.
4. Na een paar minuten staat de site op `https://<jouw-gebruikersnaam>.github.io/<repository-naam>/`.

## Aanpassen

Upload een nieuwe `index.html` (die vervangt de oude). GitHub zet de nieuwe versie binnen een paar minuten online. Wat gebruikers al bewaard hadden, blijft staan.

Verhuis je de site later naar een eigen domeinnaam, dan zien bestaande gebruikers hun planningen daar niet: browsers bewaren gegevens per website-adres. Ze kunnen dan een back-up downloaden op het oude adres en terugzetten op het nieuwe.

## Goed om te weten

- **Ander toestel of andere browser:** gebruik *Back-up downloaden* en *Back-up terugzetten* onderaan de startpagina.
- **iPhone/iPad:** Safari kan opgeslagen gegevens van een site wissen als je die 7 dagen niet opent. Zet de site op je beginscherm (Deel-knop → Zet op beginscherm); dan gebeurt dat niet. Het beginscherm-icoon heeft wel zijn eigen opslag, los van Safari.
- **Privévenster:** daar wordt niets bewaard; de app meldt dat bovenaan.
