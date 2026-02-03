# Departure — Terminal avgangstavle

Et lite Bash-script som gjør terminalen om til en sanntids avgangstavle ved å bruke Entur sitt API.

## Kort om

`departure.sh` henter kommende avganger for en stoppested og viser dem som store, sentrerte tekstblokker (bruker `figlet`) med nedtelling til avgang. Den støtter fargemodus, skjuling av header, valg av antall avganger, hentefrekvens, og transportmåter.

## Forutsetninger

- Linux / Unix-terminal
- Installerte verktøy: `curl`, `jq`, `figlet`

På Debian/Ubuntu kan du installere dem slik:

```bash
sudo apt update
sudo apt install curl jq figlet
```

## Bruksanvisning

Grunnleggende kjøring:

```bash
./departure.sh [OPTIONS]
```

Valg (OPTIONS):
- `-s <name>`    : Sett stasjonsnavn (standard: `Jernbanetorget`)
- `-n <number>`  : Antall avganger som vises (standard: `2`)
- `-m <modes>`   : Transportmåter (f.eks. `bus,tram,metro,rail,water`)
- `-i <seconds>` : Intervall for API-henting (sekunder, standard: `60`)
- `-f <font>`    : Figlet-font (standard: `mini`)
- `-C`           : Deaktiver farger (no-color mode)
- `-H`           : Skjul stasjonsheader og ekstra mellomrom
- `-v`           : Vis versjon
- `-h`           : Vis hjelpeinformasjon

Eksempler:

```bash
# Vis avganger for Nationaltheatret
./departure.sh -s "Nationaltheatret"

# Kjør uten farger og uten header
./departure.sh -C -H

# Vis 5 avganger, oppdater hvert 30. sekund
./departure.sh -n 5 -i 30
```

## Oppførsel og forklaringer

- Scriptet bruker Entur API for å finne stoppested-ID via geokoding og deretter hente estimerte avganger.
- Hvis stoppested ikke finnes vises `Station Not Found`.
- Situasjoner (service alerts) vises i rødt; normale avganger i grønt (med mindre `-C` brukes).
- Nedtelling vises som `HH:MM:SS` dersom det er mer enn en time, ellers `MM:SS`.

## Feilsøking

- Feilmelding "Missing dependencies": installer `curl`, `jq`, `figlet`.
- "Station Not Found": prøv et annet stasjonsnavn eller sjekk nettverk/Entur-tilgang.

## Lisens og forfatter

Scriptet er skrevet av Arnulf Heimsbakk.
