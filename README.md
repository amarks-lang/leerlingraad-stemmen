# Leerlingraad Stemmen — De Linde

Stem-app voor iPads. Kinderen vullen hun naam en groep in en brengen per groep van hun bouw één stem uit: in 5/6 één stem op een kandidaat uit groep 5 en één op een kandidaat uit groep 6 (7/8 net zo). Je kunt zoveel iPads tegelijk gebruiken als je wilt. Elke stem wordt als los bestandje opgeslagen in een GitHub-repo.

## Opzet: twee repo's

| Repo | Inhoud | Zichtbaarheid |
|---|---|---|
| `leerlingraad-stemmen` | deze app (`index.html`, `logo.png`, `qrcode.js`) | openbaar (nodig voor gratis GitHub Pages) |
| `leerlingraad-stemmen-data` | `config.json` (kandidaten) en `stemmen/56/…`, `stemmen/78/…` | **privé** (er staan namen van kinderen in) |

In de app-repo staat geen token en geen leerlingdata.

## Installatie

1. **App-repo**: zet `index.html` en `logo.png` in een openbare repo. Ga naar *Settings → Pages*, kies *Deploy from a branch*, branch `main`, map `/ (root)`. Na een minuutje staat de app op `https://<gebruikersnaam>.github.io/leerlingraad-stemmen/`.
2. **Data-repo**: maak een lege **privé** repo `leerlingraad-stemmen-data` (vink "Add a README" aan, zodat de branch `main` bestaat).
3. **Token**: *GitHub → Settings → Developer settings → Fine-grained tokens → Generate new token*.
   - Repository access: *Only select repositories* → alleen `leerlingraad-stemmen-data`
   - Permissions → Repository → **Contents: Read and write** (verder niets)
   - Vervaldatum: kort, bijvoorbeeld een week na de verkiezing.
4. **Eerste iPad**: open de app-URL in Safari, tik rechtsonder op ⚙, pincode `1234`.
   - *Instellingen*: gebruikersnaam, repo `leerlingraad-stemmen-data`, token, eventueel nieuwe pincode, en kies of deze iPad voor iedereen, alleen 5/6 of alleen 7/8 is. Tik *Opslaan en verbinding testen*.
   - *Kandidaten*: één naam per regel, per groep (5, 6, 7, 8). *Opslaan voor alle iPads* (komt in `config.json`). Een lege groep wordt overgeslagen.
5. **Overige iPads**: op de eerste iPad ⚙ → *Instellingen* → **Andere iPad koppelen**. Kies wie er op die iPad stemt, scan de QR-code met de Camera van de andere iPad en tik op de link. Klaar: instellingen en token staan erop, de kandidaten komen uit de repo. (Het token zit in de QR-code, dus verberg die daarna weer.) Pas je later kandidaten aan, dan nemen de andere iPads dat binnen 30 seconden over (als er niemand aan het stemmen is).
6. **Volledig scherm**: tik rechtsonder op **⛶ Volledig scherm**. Verlaat een kind het per ongeluk, dan gaat de app bij de volgende tik vanzelf weer schermvullend. Met *Begeleide toegang* (Instellingen → Toegankelijkheid, daarna 3× op de zijknop) kunnen kinderen Safari niet uit.

## Tijdens het stemmen

- Kind kiest 5/6 of 7/8 (als de iPad op "iedereen" staat), typt voor- en achternaam, kiest groep, tikt één kandidaat uit groep 5 én één uit groep 6 aan en dan **Stem!** (de knop werkt pas als beide gekozen zijn).
- Na 5 seconden staat het scherm weer klaar voor het volgende kind.
- Een naam die in dezelfde bouw al gestemd heeft wordt geweigerd, ook als dat op een andere iPad was. Hoofdletters en dubbele spaties maken niet uit.
- Elke stem is een eigen bestand, dus iPads die tegelijk stemmen zitten elkaar niet in de weg.
- Valt het internet weg, dan blijft de stem op de iPad bewaard en wordt hij later automatisch verstuurd (onderin staat hoeveel er wachten).

## Uitslag

⚙ → pincode → *Uitslag*. Per groep de stemmen per kandidaat (ververst elke 30 seconden), de winnaar met een ★, en wie er gestemd heeft. Dubbele stemmen (bijvoorbeeld van een offline iPad) tellen maar één keer: de eerste telt.

Een stem verwijderen? Verwijder het bestand in `stemmen/56/` of `stemmen/78/` in de data-repo.

Bestandsnaam van een stem: `<tijd>__<groep>__<stemmer>__g5-<kandidaat>__g6-<kandidaat>.json`.

## Na afloop

Trek het token in en verwijder of archiveer de data-repo als de uitslag binnen is.
