# Foto's voor Windows

Een Windows-app om foto's en video's van een iPhone lokaal over te zetten, te bekijken, te ordenen en veilig te stellen,
naar het voorbeeld van Apple Foto's. Je foto's blijven op je eigen pc en schijven: geen account, geen cloud.

Deze repo bevat alleen de installers en de updatepakketten. De broncode staat in een privérepo.

## Downloaden en installeren

Download de installer bij de [nieuwste release](https://github.com/estrenuo/photos-clone-releases/releases/latest):

| Je pc | Installer |
|---|---|
| Intel of AMD (de meeste pc's en laptops) | [`FotosApp-win-Setup.exe`](https://github.com/estrenuo/photos-clone-releases/releases/latest/download/FotosApp-win-Setup.exe) |
| ARM, zoals een laptop met Snapdragon, of Windows in Parallels op een Mac met Apple-chip | [`FotosApp-win-arm64-Setup.exe`](https://github.com/estrenuo/photos-clone-releases/releases/latest/download/FotosApp-win-arm64-Setup.exe) |

Weet je het niet zeker, kijk dan in Instellingen › Systeem › Info bij "Systeemtype": staat er x64, neem de eerste; staat
er ARM, de tweede.

De installatie is per gebruiker en vraagt geen beheerdersrechten. De app is niet digitaal ondertekend, dus de eerste
keer toont Windows SmartScreen een waarschuwing: kies "Meer informatie" en dan "Toch uitvoeren".

Voor importeren van een iPhone moet de app **Apple Devices** (uit de Microsoft Store) op de pc staan; die
levert de USB-driver.

De overige bestanden bij een release (`.nupkg`, `releases.*.json`, `RELEASES`) zijn voor de automatische updates, en
de `Portable.zip`-bestanden zijn een versie zonder installatie. Die heb je normaal niet nodig.

## Updates

De app kijkt bij elke start op de achtergrond of er een nieuwere versie is en downloadt die. De update wordt pas bij de
volgende start geïnstalleerd, zodat een lopende import of back-up nooit wordt onderbroken. Zonder internet werkt de app
gewoon door. Een installatie haalt alleen updates voor haar eigen soort pc (x64 of ARM). Wie geen updates wil, zet
`"check_for_updates": false` in `settings.json` in de gegevensmap.

## Wat de app doet

**Bibliotheek.** Bij de eerste start kies je een schijf voor de bibliotheek. De app maakt daar een map
`Fotobibliotheek` met de originelen in `Originelen\JJJJ\MM\`, een database en miniaturen. Is de schijf er niet
(bijvoorbeeld een losgekoppelde externe schijf), dan zegt de app dat en kun je hem opnieuw aansluiten of de
bibliotheek herstellen uit een back-up.

**Importeren van de iPhone.** Via de USB-kabel; de app opent de iPhone alleen-lezen. Een volgende import haalt alleen
op wat nieuw is: onveranderde mappen worden overgeslagen, de nieuwste mappen altijd gelezen, en elke import controleert
een deel van de oudere mappen opnieuw. Duplicaten worden herkend. Gaat de iPhone op slot of los, dan pauzeert de import
en gaat hij vanzelf verder zodra de iPhone terug is, ook na een herstart. Op de accu adviseert de app de lader, en onder
15% pauzeert de import. Vóór de eerste import vraagt de app om op de iPhone "Behoud originelen" aan te zetten en
Automatisch slot op "Nooit", en ze waarschuwt als de iPhone omgezette JPEG's lijkt te leveren in plaats van de
originelen. Een apparaatrapport maakt een inventaris van de iPhone zonder iets te importeren.

**Importeren uit een map.** Dezelfde import werkt voor een map op de pc of op een externe schijf. Ondersteund: HEIC,
HEIF, AVIF, JPEG, PNG, DNG, GIF, TIFF, WebP en BMP, en video in MOV, MP4, M4V, 3GP en AVI. Mislukte bestanden staan
met hun reden in een eigen lijst en kun je opnieuw proberen.

**Live Photos en bewerkte foto's.** Na de import koppelt de app wat bij elkaar hoort: de video van een Live Photo aan
de foto, een bewerkte versie (`IMG_E…`) aan het origineel, en `.AAE`-bestanden als sidecar.

**Tijdlijn.** Drie zoomniveaus: Jaren, Maanden en Alle foto's (per dag). De scrollbalk springt direct naar elke maand.
De tijdlijn tekent alleen wat in beeld is en blijft vlot bij tienduizenden foto's.

**Viewer.** Dubbelklik opent een foto of video. Pijltjes bladeren, Esc sluit, scrollwiel, pinch of + en − zoomen tot
100%, en Ctrl+I toont het infopaneel met de gegevens van de foto, waar je ook een bijschrift en trefwoorden toevoegt.
Video's spelen af met de meegeleverde VLC-onderdelen, dus ook HEVC (H.265) zonder de extensie uit de Microsoft Store,
en HDR-video van de iPhone wordt omgezet voor een gewoon scherm. Een Live Photo speel je af door de LIVE-badge
ingedrukt te houden.

**Albums en favorieten.** Albums maken, hernoemen en verwijderen; foto's toevoegen via het menu of door ze naar een
album in de zijbalk te slepen; een eigen volgorde en een omslagfoto. Favorieten met het hartje of de punt-toets. Zes
slimme albums vullen zich vanzelf: Favorieten, Video's, Live Photos, Schermafbeeldingen, Recent geïmporteerd en
Mislukte imports. Selecteren met klikken, Ctrl/Shift+klikken, een selectiekader of Ctrl+A. Elke actie draai je terug
met Ctrl+Z.

**Recent verwijderd.** Verwijderde foto's blijven 30 dagen bewaard en zijn terug te zetten, ook in hun albums.
Definitief verwijderen vraagt altijd om bevestiging.

**Zoeken.** Ctrl+F zoekt in bestandsnaam, bijschrift, trefwoorden, plaats en albumnaam, zonder onderscheid naar
hoofdletters of accenten. Datums als "2023", "juli 2023" of "zomer 2023" worden vanzelf een filter. Daarnaast zijn er
filters op periode, soort, album, camera en favorieten.

**Plaatsen zonder internet.** Foto's met GPS-coördinaten krijgen een plaatsnaam uit een meegeleverde dataset (plaats,
provincie en land, in het Nederlands waar die naam bekend is). Er gaat niets naar een online dienst.

**Back-up en herstel.** Back-up naar een tweede schijf, die niet op dezelfde fysieke schijf als de bibliotheek mag
staan. Met één klik kopieert de app alleen wat nieuw of veranderd is, controleert elk bestand met een SHA-256-hash en
gaat na een onderbreking verder waar ze was. De back-up bewaart de laatste vijf versies van de database en houdt
definitief verwijderde bestanden nog 90 dagen in een archief. Eens per maand controleert de app een steekproef van de
back-up. Een back-up start nooit vanzelf; de statusbalk toont wanneer de laatste was. Met "Bibliotheek herstellen" bouw
je de bibliotheek vanuit de back-up opnieuw op.

## Waar staat wat

| Wat | Waar |
|---|---|
| De app zelf | `%LOCALAPPDATA%\FotosApp` |
| Instellingen en logboek | `%LOCALAPPDATA%\PhotosClone` |
| Foto's, video's en database | de map `Fotobibliotheek` op de schijf die je bij de eerste start koos |
| Back-up | de map `Fotobackup` op de back-upschijf |

De app en je gegevens staan bewust apart: de app verwijderen of opnieuw installeren laat de instellingen, de
bibliotheek en de back-up ongemoeid.

## Bronvermelding

Plaatsgegevens van [GeoNames](https://www.geonames.org/), onder [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
De app gebruikt onder meer [ExifTool](https://exiftool.org/), [FFmpeg](https://ffmpeg.org/) (LGPL-build),
[LibVLC](https://www.videolan.org/vlc/libvlc.html), [Magick.NET](https://github.com/dlemstra/Magick.NET),
[Avalonia](https://avaloniaui.net/) en [Velopack](https://velopack.io/).
