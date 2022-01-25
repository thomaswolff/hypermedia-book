# Building Hypermedia APIs with HTML5 and Node

Personal notes from reading [https://github.com/mamund/Building-Hypermedia-APIs](https://github.com/mamund/Building-Hypermedia-APIs)

## Chapter 3 - JSON hypermedia

### Installation notes

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
