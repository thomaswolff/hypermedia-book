# Building Hypermedia APIs with HTML5 and Node

Personal notes from reading [https://github.com/mamund/Building-Hypermedia-APIs](https://github.com/mamund/Building-Hypermedia-APIs)

## Chapter 3 - JSON hypermedia

<details>
<summary>Installation notes</summary>

### Installation notes

#### Prerequisites

- Docker
- Node
- WSL

#### CouchDB in WSL

```bash
# In WSL
docker run -p 5984:5984 -d --name my-couchdb couchdb:2.3.1
```

Verify installation by going to [http://127.0.0.1:5984/_utils/#/verifyinstall](http://127.0.0.1:5984/_utils/#/verifyinstall)

#### Initialize data

```bash
# In WSL
cd /home/thomas/dev/github.com/other/Building-Hypermedia-APIs/couchdb/collection
./collection_data.sh
```

#### Start server

```bash
# In Windows PowerShell
cd C:\Dev\github.com\Building-Hypermedia-APIs\nodejs\collection
node app.js
# Should output 'Express server listening on port 3000'
```

#### Open client

```bash
# In Windows PowerShell
cd C:\Dev\github.com\Building-Hypermedia-APIs\nodejs\collection\public
http-server
# Should output
# Starting up http-server, serving ./
# Available on:
#   http://160.68.84.139:8080  
#   http://172.17.32.1:8080    
#   http://172.27.0.1:8080     
#   http://192.168.0.19:8080   
#   http://127.0.0.1:8080      
# Hit CTRL-C to stop the server
```

Open [http://localhost:8080](http://localhost:8080) to view `Collection+JSON` client.

</details>

### Presentation notes

#### Use case

Lage en hypermediatype for å støtte lese- og skriveoperasjoner for samlinger av "ting" (f.eks. oppgaveliste).

#### Design av hypermediatypen

Betraktninger av de ulike dimensjonene av en hypermediatype som gjøres fra klientenes perspektiv.

##### Dataformat

Ettersom klientene skal skriver i JavaScript, brukes JSON som dataformat. Dette gjør det enkelt å behandle dataene i JavaScript.

##### Tilstandsoverganger ("state transitions")

###### Hva skal tilstandene inneholde?

- Samlingen av "ting"
- Et enkelt innslag i samlingen
- Liste med mulige spørringer man kan gjøre mot samlingen
- Mal for å legge til eller redigere innslag i samlingen
- Feildetaljer

###### Aktuelle tilstander

- "Collection state"
  - Samlingen av "ting"
  - Spørringer
  - Mal for å opprette innslag
- "Item state"
  - Et enkelt innslag
  - Spørringer
  - Mal for å redigere innslaget
- "Error state"
  - Detaljer om den nyeste feilen som oppstod

###### Tilstandsoverganger

- "Collection state"
  1. -> Velge enkeltinnslag ("Item state")
  2. -> Legge til enkeltinnslag ("Item state")
  3. -> Utføre spørring ("Collection state")
  4. -> Last samlingen på nytt ("Collection state")
- "Item state"
  5. -> Oppdatere innslaget ("Item state")
  6. -> Slette innslaget ("Collection state")
  7. -> Hent innslaget på nytt ("Item state")
  8. -> Gå tilbake til samlingen ("Collection state")

![Skisse](gfx/chapter-3/state-transitions.drawio.svg)

##### Husker ikke begrepet

Generic - `Collection+JSON` er ikke spesifikt for én spesiell "ting", men kan brukes til å modellere alle "ting".

##### Application flow

Intrinsic - hva innebærer det?

##### Format på respons

JSON Schema

#### Server

`Node`-applikasjon laget med:

- `Express.js`
- `ejs` (_Embedded JavaScript templates)
- `CouchDb`

#### Klient

JavaScript-applikasjon som har innebygd forståelse av `Collection+JSON`-hypermedia-formatet. Forøvrig er den eneste koblingen mellom klient og server at klienten har en forhåndsbestemt URL for å nå serveren.
