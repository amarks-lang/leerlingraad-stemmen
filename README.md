# Leerlingraad Stemmen — De Linde

Stem-app voor iPads. Kinderen tikken hun eigen naam aan, loggen in met hun persoonlijke pincode (van een geprinte stempas) en brengen per groep van hun bouw één stem uit: in 5/6 één stem op een kandidaat uit groep 5 en één op een kandidaat uit groep 6 (7/8 net zo). Je kunt zoveel iPads tegelijk gebruiken als je wilt. Elke stem wordt als los bestandje opgeslagen in een GitHub-repo.

## Opzet: twee repo's

| Repo | Inhoud | Zichtbaarheid |
|---|---|---|
| `leerlingraad-stemmen` | deze app (`index.html`, `logo.png`, `qrcode.js`) | openbaar (nodig voor gratis GitHub Pages) |
| `leerlingraad-stemmen-data` | `config.json` (leerlingen met pincodes, kandidaten) en `stemmen/56/…`, `stemmen/78/…` | **privé** (er staan namen van kinderen in) |

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
   - *Leerlingen*: per groep alle leerlingen, één naam per regel. *Opslaan en pincodes maken* geeft elk kind een eigen pincode van 4 cijfers (bestaande kinderen houden hun code). *Stempassen printen* print kaartjes om te knippen: naam, groep en pincode.
   - *Kandidaten*: één naam per regel, per groep (5, 6, 7, 8). Schrijf de naam precies zoals bij Leerlingen, dan kan de app zien dat een kind niet op zichzelf mag stemmen (je krijgt een melding als een naam niet klopt). *Opslaan voor alle iPads* (komt in `config.json`). Een lege groep wordt overgeslagen.
5. **Overige iPads**: op de eerste iPad ⚙ → *Instellingen* → **Andere iPad koppelen**. Kies wie er op die iPad stemt, scan de QR-code met de Camera van de andere iPad en tik op de link. Klaar: instellingen en token staan erop, de kandidaten komen uit de repo. (Het token zit in de QR-code, dus verberg die daarna weer.) Pas je later kandidaten aan, dan nemen de andere iPads dat binnen 30 seconden over (als er niemand aan het stemmen is).
6. **Volledig scherm**: tik rechtsonder op **⛶ Volledig scherm**. Verlaat een kind het per ongeluk, dan gaat de app bij de volgende tik vanzelf weer schermvullend. Met *Begeleide toegang* (Instellingen → Toegankelijkheid, daarna 3× op de zijknop) kunnen kinderen Safari niet uit.

## Tijdens het stemmen

- Kind kiest 5/6 of 7/8 (als de iPad op "iedereen" staat), dan zijn groep, tikt zijn **eigen naam** aan en typt zijn **pincode** op het cijferscherm.
- Daarna kiest het één kandidaat uit groep 5 én één uit groep 6 en tikt op **Stem!** (de knop werkt pas als beide gekozen zijn).
- **Niet op jezelf**: je eigen naam staat niet tussen de kandidaten.
- **Niet dubbel**: wie al gestemd heeft staat grijs doorgestreept, ook als dat op een andere iPad was.
- **Pincode raden gaat niet**: na 3 foute codes is die naam op die iPad 60 seconden geblokkeerd.
- Na 5 seconden staat het scherm weer klaar voor het volgende kind.
- Elke stem is een eigen bestand, dus iPads die tegelijk stemmen zitten elkaar niet in de weg.
- Valt het internet weg, dan blijft de stem op de iPad bewaard en wordt hij later automatisch verstuurd (onderin staat hoeveel er wachten).

## Uitslag

⚙ → pincode → *Uitslag*. Per groep de stemmen per kandidaat (ververst elke 30 seconden), de winnaar met een ★, wie er gestemd heeft en wie **nog niet**. Dubbele stemmen (bijvoorbeeld van een offline iPad) tellen maar één keer: de eerste telt.

**Na een test opnieuw beginnen**: ⚙ → *Uitslag* → **Stemming resetten**. Na een bevestiging worden alle stemmen gewist; leerlingen, pincodes en kandidaten blijven staan.

Eén losse stem verwijderen? Verwijder het bestand in `stemmen/56/` of `stemmen/78/` in de data-repo.

Bestandsnaam van een stem: `<tijd>__<groep>__<leerling-id>__g5-<kandidaat>__g6-<kandidaat>.json`.

Kind kwijt zijn pas? ⚙ → *Leerlingen* → *Pincodes bekijken*.

## Na afloop

Trek het token in en verwijder of archiveer de data-repo als de uitslag binnen is.
