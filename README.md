# Building Hypermedia APIs with HTML5 and Node

Personal notes from reading [https://github.com/mamund/Building-Hypermedia-APIs](https://github.com/mamund/Building-Hypermedia-APIs)

## Chapter 3 - JSON hypermedia

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

### Presentation notes

#### Use case

Lage et hypermediaformat for å støtte lese- og skriveoperasjoner for samlinger av "ting".

#### Design av hypermediaformatet

##### Grunnformat

JSON

Blir valgt fordi det er enkelt å behandle i JavaScript.

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
