# scriptspace-releases

Publiek releasekanaal voor [ScriptSpace CMS](https://scriptspace.nl). De updater in het adminpaneel (Admin, Updates) vraagt bij GitHub de **nieuwste Release** van deze repo op (`releases/latest`) en downloadt de bijbehorende bestanden.

## Wat hoort bij een release

Elke GitHub Release heeft een tag (`v<versie>`, hoofdletter `V` werkt ook) en drie assets:

| Asset | Wat |
|---|---|
| `manifest.json` | Versie, minimale PHP-versie, grootte en SHA-256 van de zip en van elk bestand erin |
| `manifest.json.sig` | Ed25519-handtekening over het manifest |
| `scriptspace-<versie>.zip` | De release zelf |

Laatste release: **0.22.0** (2026-10-01). De bestanden in de hoofdmap van deze repo (`manifest.json`, `scriptspace-0.13.0.zip`, `RELEASE_NOTES.md`) zijn een oudere upload van 0.13.0; de updater gebruikt ze niet, hij leest alleen de Releases.

## Waarom je GitHub niet hoeft te vertrouwen

De site controleert de handtekening, de zip en elk afzonderlijk bestand tegen het ondertekende manifest vóór er iets verandert. Alleen releases ondertekend met de private sleutel die bij `includes/update_pubkey.php` in de CMS hoort, worden geïnstalleerd. De private sleutel staat nooit in een repo en verlaat de computer van de beheerder niet.

## Een nieuwe release maken

Dit gebeurt op de eigen computer, vanuit de repo `scriptspace-cms`:

1. `python3 tools/release.py build` maakt zip, manifest en handtekening en controleert dat de sleutel bij de publieke sleutel hoort.
2. Maak in deze repo een nieuwe GitHub Release met tag `v<versie>` en voeg de drie bestanden toe als assets.
3. De site toont daarna "nieuwe versie beschikbaar". Zelf installeren kan alleen als `'updater' => true` in `config.php` staat (standaard uit).

Zie `docs/DEPLOY.md` in `scriptspace-cms` voor het volledige proces.
