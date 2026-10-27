# Wie kan wanneer

Een kleine webapp om met je vrienden, familie of ploeg een datum te prikken. Iedereen zit samen in een groep, tikt in één gedeelde kalender de dagen aan waarop het past en ziet live wanneer de anderen kunnen. Niemand moet iets installeren of een account maken.

## Hoe het werkt

1. **Maak een groep** en geef ze een naam. Je krijgt een uitnodigingslink.
2. **Zet de link in jullie WhatsApp-groep.** Wie hem opent en een naam invult, zit in de groep.
3. **Maak een planning**: je geeft ze alleen een naam, bijvoorbeeld "Etentje".
4. **Iedereen tikt zijn dagen aan** in dezelfde kalender, ook wie de planning maakte. Eén keer tikken is *kan*, nog een keer is *misschien*, een derde keer haalt de dag weg. Met *Snel alle vrijdagen/zaterdagen/zondagen* duid je een hele maand in één keer aan.
5. **Iedereen ziet live** hoeveel mensen elke dag kunnen (het cijfertje in de kalender), welke dag het best past en wie nog niet antwoordde. Wie de planning maakte, prikt de dag en kopieert een aankondiging voor de groep.

Doet iemand mee zonder de app, bijvoorbeeld omdat die in de chat of mondeling antwoordde, dan voeg je die persoon toe bij **Voor anderen** en tik je de dagen voor die persoon aan.

Op de startpagina staat een voorbeeldgroep om alles uit te proberen zonder dat er iets bewaard wordt.

## Toegang en privacy

- Groepen, planningen en antwoorden staan in een Firestore-database van **jouw eigen** Firebase-project (Google). Kies bij het aanmaken een Europese locatie.
- **Alleen leden** kunnen een groep lezen. Lid word je alleen met de uitnodigingslink: die bevat een geheime code. De beveiligingsregels in `firestore.rules` dwingen dat af in de database zelf.
- Elk toestel krijgt automatisch een anoniem account. Er is geen e-mail, wachtwoord of telefoonnummer nodig.
- Binnen een groep vertrouwen de leden elkaar: iedereen kan dagen invullen voor wie zonder app meedoet en mensen toevoegen. De titel en de geprikte dag van een planning past alleen aan wie ze maakte of de beheerder.
- De **beheerder** (wie de groep maakte) kan leden verwijderen en een **nieuwe uitnodigingslink** maken. De oude link werkt dan niet meer; wie al lid is, blijft lid.
- De pagina laadt de Firebase-bibliotheek van `www.gstatic.com` en praat met Firebase. Er zijn geen advertenties, geen analytics en geen tracking.

## Eenmalig instellen: een gratis Firebase-project

Dit doe je één keer, als beheerder van de site. Het gratis Spark-abonnement is ruim voldoende; je hebt geen kredietkaart nodig. De knoppen in de Firebase-console staan meestal in het Engels.

1. **Project maken.** Ga naar <https://console.firebase.google.com>, klik **Create a project** (of *Add project*), kies een naam zoals `wie-kan-wanneer` en zet Google Analytics uit.
2. **Anoniem aanmelden aanzetten.** Ga links naar **Build → Authentication → Get started**. Kies in het tabblad **Sign-in method** de provider **Anonymous**, zet hem aan en klik **Save**.
   Ga daarna naar **Settings → Authorized domains → Add domain** en voeg `<jouw-gebruikersnaam>.github.io` toe (bijvoorbeeld `aron21111.github.io`).
3. **Database maken.** Ga naar **Build → Firestore Database → Create database**. Kies een Europese locatie (bijvoorbeeld `eur3 (Europe)` of `europe-west1 (Belgium)`) en **production mode**.
   Open daarna het tabblad **Rules**, vervang alles door de inhoud van `firestore.rules` uit deze map en klik **Publish**.
4. **De app koppelen.** Klik bovenaan links op het tandwiel → **Project settings**. Kies onderaan bij *Your apps* het web-icoon **`</>`**, geef de app een naam en klik **Register app** (Firebase Hosting is niet nodig). Firebase toont een blok `firebaseConfig = { apiKey: ..., ... }`.
   Open `config.js` en vervang het blok tussen de accolades achter `firebase:` door die waarden.
   Die gegevens zijn niet geheim; ze mogen in een publieke repository staan. Wat iemand mag lezen of schrijven, staat in de regels van stap 3.
5. **Online zetten** (zie hieronder) en de site openen. Maak een groep en test de uitnodigingslink in een privévenster of op je gsm.

Krijg je een melding in de app, dan zegt die meestal welke stap ontbreekt: *Anonymous* staat niet aan (stap 2), de regels zijn niet gepubliceerd (stap 3) of `config.js` klopt niet (stap 4).

## Bestanden

| Bestand | Waarvoor |
| --- | --- |
| `index.html` | De volledige app (HTML, CSS en JavaScript in één bestand) |
| `config.js` | De koppeling met jouw Firebase-project |
| `firestore.rules` | De beveiligingsregels voor de database (plak je in de Firebase-console) |
| `manifest.webmanifest` en `icons/` | Icoon en naam als je de site op je beginscherm zet |
| `fonts/` | Barlow Condensed en Hanken Grotesk, onder de SIL Open Font License (zie de `OFL-*.txt`-bestanden) |

## Online zetten met GitHub Pages

1. Maak een **public** repository aan op GitHub (bijvoorbeeld `wie-kan-wanneer`).
2. Upload alle bestanden en mappen uit deze map, zodat `index.html` in de hoofdmap van de repository staat.
3. Ga naar **Settings → Pages**. Kies bij *Source* **Deploy from a branch**, branch **main**, map **/ (root)**, en klik **Save**.
4. Na een paar minuten staat de site op `https://<jouw-gebruikersnaam>.github.io/<repository-naam>/`.

## Aanpassen

Upload een nieuwe `index.html` (die vervangt de oude). GitHub zet de nieuwe versie binnen een paar minuten online. Groepen en antwoorden staan in Firebase en blijven dus gewoon bestaan.

Pas je `firestore.rules` aan, publiceer de nieuwe versie dan ook in de Firebase-console (stap 3).

Verhuis je de site naar een ander adres, voeg dat domein dan toe bij *Authorized domains* (stap 2). Wie al lid was, opent op het nieuwe adres gewoon opnieuw de uitnodigingslink en kiest zijn naam; de app vraagt dan "Ben jij dat?".

## Goed om te weten

- **Ander toestel of andere browser:** open de uitnodigingslink opnieuw en vul dezelfde naam in. De app vraagt of jij dat bent en neemt je antwoorden over.
- **iPhone/iPad:** Safari kan na 7 dagen zonder bezoek vergeten dat je in een groep zit. Dan werkt hetzelfde: de link opnieuw openen en je naam kiezen.
- **Meldingen:** de app stuurt zelf geen meldingen. Laat de groep weten dat er een nieuwe planning is met de knop *Open in WhatsApp*.
- **Oude planningen:** planningen uit de allereerste versie (alleen in je browser bewaard) worden niet overgenomen. Planningen met vaste dagen uit de eerste groepsversie blijven werken: de antwoorden verschijnen gewoon in de kalender.
- **Testen zonder echt project:** `config.js` kan ook verwijzen naar de lokale Firebase Emulator Suite, met `emulator: { auth: "http://127.0.0.1:9099", host: "127.0.0.1", port: 8080 }` naast `firebase` en een `projectId` die met `demo-` begint.
