# Stručni kurs RAO - Projekat

Ovaj projekat je razvijen u okviru strucnog kursa "Razvoj aplikacija u oblaku (Amazon veb servisi)" i koristi **Leaflet** i **OpenStreetMap (OSM)** za prikaz interaktivne mape Srbije sa markerima punjača. 
Za lokalni razvoj i testiranje AWS servisa koristi se **LocalStack**

### O Leaflet i OpenStreetMap

**Leaflet** je open-source JavaScript biblioteka za interaktivne mape. Koristi se za:
- Prikazivanje markera na mapi (punjači)
- Zoom i pan funkcionalnosti
- Popup prozore sa detaljima

**OpenStreetMap (OSM)** je besplatna, open-source mapa sveta (alternativa Google Maps-u). Leaflet koristi OSM tile servere za učitavanje mapa - tile-ovi se učitavaju sa `tile.openstreetmap.org` CDN-a.

### Funkcionalnosti:

- ✅ **Mapa** - Prikaz punjača na interaktivnoj mapi (Leaflet)
- ✅ **Pretraga po gradu** - Unesi naziv grada i prikaži sve punjače
- ✅ **Detalji punjača** - Klik na marker prikazuje detalje (adresa, broj priključaka, itd.)
- ✅ **Sync OCM** - Dugme za sinhronizaciju podataka sa Open Charge Map API-ja

## Preduslovi

- Docker i Docker Compose instalirani
- Node.js i npm instalirani

## Pokretanje projekta

### 1. Pokreni LocalStack sa Docker Compose

Pokreni LocalStack za simulaciju AWS servisa lokalno:
```bash
docker compose up -d
```

Proveri da li LocalStack radi
```bash
docker ps
```

### 2. Deploy Serverless konfiguracije

Instaliraj serverless dependencije
```bash
npm install
```

Deploy Serverless infrastrukture
```bash
npx serverless deploy
```

### 3. Ažuriranje promenljive `API_ID` u `web/index.html` izlazom sledece naredbe:
```bash
awslocal apigateway get-rest-apis --query 'items[0].id' --output text
```

### 4. Deploy frontend na S3

```bash
npm run deploy-frontend-fixed-bucket
```

Aplikacija će trčati na:

**http://punjaci-website.s3-website.localhost.localstack.cloud:4566/**


## Primer aplikacije

![Primer mape sa punjačima](primerMape.png)

