# Hitster Thuis

Een volledig digitale versie van Hitster die met jullie eigen Spotify-playlist werkt. Eén telefoon gaat rond, de app houdt ieders tijdlijn, tokens en score bij.

**Bestanden:** `index.html` (de hele app), `manifest.json`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`.

## Wat je nodig hebt

- **Spotify Premium** voor de eigenaar van de Spotify-app én voor het account dat afspeelt. Spotify eist dit sinds februari 2026 voor alle apps in Development Mode, en afspelen via de API kan alleen met Premium.
- Een **playlist die je zelf bezit of waaraan je meewerkt**. Andere playlists kan de app niet uitlezen (ook een regel van Spotify). Tip: kopieer een bestaande playlist naar je eigen account.
- Een gratis **GitHub-account** om de app te hosten (Spotify vereist HTTPS).

Wil je eerst alleen de spelflow uitproberen? Open `index.html` en kies **Probeer de demo**. Dan speel je met 38 bekende nummers, zonder audio.

## Stap 1 · Zet de app op GitHub Pages

1. Maak op github.com een nieuwe **public** repository, bijv. `hitster`.
2. Klik **Add file → Upload files** en sleep alle vijf bestanden erin. Klik **Commit changes**.
3. Ga naar **Settings → Pages**. Kies bij *Source*: **Deploy from a branch**, branch **main**, map **/ (root)**. Opslaan.
4. Na een minuutje staat je app op `https://JOUWNAAM.github.io/hitster/`. Dit is je **Redirect URI** (let op de `/` aan het eind).

## Stap 2 · Maak een Spotify-app aan

1. Ga naar [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) en log in met het Premium-account.
2. **Create app**:
   - *App name*: Hitster Thuis (of wat je wilt)
   - *Redirect URI*: plak exact het adres uit stap 1, bijv. `https://JOUWNAAM.github.io/hitster/` en klik **Add**
   - *Which API/SDKs*: vink **Web API** aan
3. Opslaan en kopieer de **Client ID** (de Client Secret heb je níet nodig).
4. **Andere spelers die ook willen inloggen?** Ga naar *User Management* en voeg hun Spotify-e-mailadres toe (maximaal 5). Als alleen jij inlogt en afspeelt, hoef je niets toe te voegen.

## Stap 3 · Eerste keer opstarten

1. Open de app-link in **Safari** op je iPhone.
2. Plak je Client ID en tik **Opslaan** (je kunt hem ook bovenaan in `index.html` bij `CLIENT_ID` invullen, dan hoeft niemand hem in te typen).
3. Tik **Inloggen met Spotify** en geef toestemming.
4. Plak de link van jullie playlist (in Spotify: ··· → Delen → Link kopiëren) en tik **Laden**.
5. Tik **Kaartjes beheren** en loop de jaartallen na (zie hieronder).
6. **Nieuw spel**, namen invullen, spelen!

### Op het beginscherm zetten
In Safari: deelknop → **Zet op beginscherm**. De app opent dan schermvullend.
Let op: een beginscherm-app heeft op iOS een eigen opslag, los van Safari. Je moet daarin dus één keer opnieuw inloggen en de playlist laden. Gaat het inloggen vanuit de beginscherm-app mis, speel dan gewoon in Safari.

## Afspelen

De muziek speelt af via **Spotify Connect**: de app stuurt de Spotify-app op je telefoon (of een speaker/laptop) aan. Spotify's eigen webspeler werkt niet in Safari op de iPhone, daarom gaat het zo.

- Open de Spotify-app en speel kort iets af, zodat je telefoon als "actief apparaat" verschijnt.
- Kies via 🔊 in het spel op welk apparaat het moet spelen. Een speaker is ideaal: dan ziet niemand titel en artiest op het scherm.
- Elk nummer start op een willekeurig punt tussen 30 en 60 seconden, zodat de intro het niet meteen weggeeft. **↻ Ander stukje** speelt een ander fragment.

## Jaartallen corrigeren

Spotify geeft het jaar van het **album** waar het nummer op staat. Bij remasters, live-albums en verzamelalbums is dat vaak te laat (bijv. "Bohemian Rhapsody — 2011 Remaster"). In **Kaartjes beheren** kun je:

- het jaar per nummer aanpassen (geel = aangepast),
- nummers uitsluiten met het vinkje,
- filteren op *Aangepast*, *Uitgesloten* of *Geen jaar*,
- alles **exporteren** als `hitster-jaartallen.json` en op een andere telefoon weer **importeren**.

Tip: voeg bij voorkeur de originele single/album-versies aan je playlist toe, dan hoef je minder te corrigeren.

## Spelregels

- Iedereen begint met één open kaartje.
- Om de beurt speelt een nummer; de speler aan de beurt tikt waar het in zijn tijdlijn hoort en tikt **Vastzetten**.
- Na **Omdraaien** zie je het jaar. Goede plek = kaartje blijft. Fout = weg. Zelfde jaar naast elkaar telt als goed.
- Eerste die het doel haalt (standaard 10, instelbaar) wint.

**Met tokens (aan/uit bij nieuw spel):**
- Start met 2 tokens, maximaal 5.
- Titel + artiest goed geraden vóór het omdraaien: +1 token (de groep beslist, tik op de knop).
- 1 token: nummer overslaan.
- 1 token: **Hitster!** roepen en een andere plek kiezen op de tijdlijn van de speler aan de beurt. Zit die fout en jij goed, dan krijg jij het kaartje. Meerdere spelers kunnen roepen; de eerste met de goede plek wint.
- 3 tokens: een gratis kaartje, direct goed geplaatst.

Het spel wordt automatisch opgeslagen. Sluit je Safari af, dan kun je via **Spel hervatten** verder.

## Problemen?

| Melding | Oplossing |
|---|---|
| *INVALID_CLIENT: Invalid redirect URI* | De Redirect URI in het Dashboard moet exact gelijk zijn aan het adres in de app (staat op het startscherm), inclusief `https://` en de `/` aan het eind. |
| *Kan deze playlist niet lezen* | Je bent geen eigenaar/medewerker van de playlist. Kopieer hem naar je eigen account. |
| *Geen actief Spotify-apparaat* | Open de Spotify-app, speel iets af, tik in het spel op 🔊 → Vernieuwen. |
| *Afspelen geweigerd* | Het account heeft geen Premium. |
| Andere speler kan niet inloggen | Voeg diens Spotify-e-mail toe onder *User Management* in het Dashboard. |

## Technisch

Puur HTML/CSS/JavaScript, geen server. Inloggen via Spotify's Authorization Code-flow met PKCE. Gebruikt de Web API-endpoints na de wijzigingen van februari 2026 (`/playlists/{id}/items`). Alles (inlog, playlist, jaartallen, spelstand) staat in `localStorage` van de browser.
