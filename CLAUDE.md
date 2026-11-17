# Randaberghallen – ny nettside (demo)

Dette er et forslag til ny nettside for Randaberghallen (Randaberg svømmehall og idrettshall).
Siden er laget av Christoffer og Lucas. Den kjører på GitHub Pages:
https://christoffer-cell7.github.io/randaberghallen-demo/

Den eksisterende siden randaberghallen.no eies og drives av Randaberg kommune.
Dette er en demo. Den er ikke lansert og er skjult for søkemotorer (noindex).

## Regler som alltid gjelder

1. **Språk:** All tekst på siden skal være bokmål. Snakk norsk med Christoffer. Han har svært lite engelsk, så hold forklaringer korte og enkle.
2. **PC-visningen skal ikke endres** med mindre Christoffer ber om det. Mobil og PC er tunet hver for seg. Etter hver endring skal PC-visningen sammenlignes skjerm for skjerm og være uendret.
3. **Universell utforming:** Siden skal følge WCAG 2.1 A og AA. Sjekk kontrast (minst 4.5:1 for vanlig tekst), alternativ tekst på bilder, lenker med tydelig navn og tastaturbruk. Test med axe-core.
4. **Ikke finn på fakta.** Åpningstider, priser, regler og varer skal komme fra Christoffer, fra hallens ansatte eller fra randaberghallen.no. Hvis noe er usikkert, spør.
5. **Ingen passord, nøkler eller tokens** i repoet, i filer eller i chatten. Hemmeligheter ligger bare i Apps Script-egenskapene til e-postroboten.
6. **Ikke endre siden før Erik har sett den.** Erik Knudsen (leder for hallen) skal se siden på møtet onsdag 18. november 2026 kl. 10.30. Ingenting skal endres på den live siden før møtet.
7. Repoet er offentlig. Skriv aldri private opplysninger (e-postadresser, telefonnumre, interne avtaler) i filer her.

## Slik er prosjektet bygget

- `prototype-1.html` og `prototype-2.html` – to varianter av siden. Hver er én selvstendig HTML-fil (ca. 730 KB) med CSS og JavaScript inni. Bilder ligger ved siden av.
- `innhold.json` – innholdet som skal endres ofte (for eksempel åpningstider, stengte dager, priser). Sidene leser dette ved innlasting.
- `bilder/` – bildene (21 filer).
- `index.html` – enkel startside som peker til prototypene. Den har noindex.

Siden har seks undersider: forside, svømmehall, idrettshall, trimrom, barnebursdag og bestilling/spørsmål.
Kiosken, badstuen og svømmerne på tavlen (animasjon) har egen logikk i JavaScript.

### Mobil
- Mobilregler ligger i `@media (max-width:759px)` nederst i `<style>`.
- Variabelen `lett` er sann på mobil og berøringsskjerm. Svømmerne går halvt så fort på mobil (`SAKTE = lett ? .5 : 1`).

## E-postroboten

Hallen kan endre innhold ved å sende en vanlig e-post til en robot.
- Roboten er et Google Apps Script som kjører hvert minutt på en egen Gmail-konto som Christoffer eier.
- Den leser e-posten, sender den til Claude, og skriver endringene til `innhold.json` via GitHub.
- Bare godkjente avsendere får endre noe. Avsenderen må også bestå SPF/DKIM. Andre får ingen svar og e-posten merkes `Robot/Avvist`.
- Skriver man «angre», rulles forrige endring tilbake.
- Robotkoden ligger ikke i dette repoet. Be Christoffer om tilgang hvis du må endre den.
- Hvis repoet flyttes til en annen GitHub-konto, må `github.eier` og `nettside` i roboten oppdateres, og Christoffer må legge inn ny GitHub-nøkkel selv.

## Hvordan endringer testes

1. Kjør siden lokalt og ta skjermbilder på mobil (375 og 393 px bredde) og PC (1280 og 1920 px).
2. Sammenlign PC før og etter. For å få stabil sammenligning, bruk `?tid=2026-11-11T09:40` i adressen (fast klokkeslett) og skjul animasjonen.
3. Kjør axe-core mot alle seks sider.
4. Sjekk at ingen bilder gir 404.

Playwright med Chrome fungerer bra til dette.

## Hvordan filene lastes opp

Hovedfilene er store. Endringer gjøres som små lister over endringer og settes inn i filen. Kontroller alltid SHA-256 etter at endringen er lagt inn, og se at den live siden på GitHub Pages har fått den nye versjonen (bruk cache:'reload').

## Status

Ferdig:
- Begge prototypene, med innhold fra randaberghallen.no
- Kioskens åpningstider (fra skiltet i hallen)
- Ryddigere mobilvisning og roligere svømmere på mobil
- Tilgjengelighetstest av randaberghallen.no (funn ligger i møtedokumentet)
- E-postroboten er rettet slik at både Christoffer og Erik kan bruke den

Gjenstår etter møtet (ikke begynn før Christoffer sier det):
- Personvernside
- Brukerreglement for idrettshallen
- Videresending fra gamle adresser
- Fjerne noindex og demolinjen
- Få Erik til å bekrefte tider og priser
- Test med skjermleser, Safari og Firefox
- Bildetekster
- Eventuelt flytte repoet til Gardner Solutions sin GitHub-organisasjon

## Avtale (hvis noen spør)

Lucas eier firmaet Gardner Solutions. Christoffer jobber i svømmehallen og hjelper til, men er ikke del av firmaet. Han må alltid si fra til Erik om dette. Tilbudet til hallen: siden gis gratis, drift koster 150 kr i måneden. Markedspris er ca. 20 000 kr. Spørsmål om eierskap og hva som skjer hvis hallen vil avslutte, må Lucas svare på.
