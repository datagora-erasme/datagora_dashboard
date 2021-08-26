# Guide installation Dashboard

## Introduction
Le projet Dashboad est piloté par Erasme  dans le cadre de Datagora dont l'objectif est de mettre en place un tableau de bord modulable applicable à tout type de donné et facilement replicable dans d'autre contexte.Elle permet de visualiser différent KPI sur la végétalisation à travers différents graphes afin d'aider les collctivités à la prise de décision.

---
## Installation 

### 1. Installation server web  

#### Prérequis
#####  Installer node.js

* Installer les module complémentaire ws:
#### installation de ws

```
    npm install ws
```
#### Installation de socket.IO
```
   npm install socket.io
```
#### Installation de express
```
npm install express

```
#### Tnstallation de ejs

```
npm install ejs

```


* lancer de l'application 

#### Lancer le serveur  depuis le repertoire WebsocketServer

```
   node server.js
'''
ou
'''
nodemon server.js
'''

* Aller sur le lien https://localhost:3001 pour voir la page d'accueil de l'application

#### pour charger un prototype vous pouvez aller sur   dans le dossier  exemples

#### Vous touverez des protos déja enregistrés dénomé myParameters3.json,myParameters4.json, myParameters5.json  que vous pouvez charger ou commencer un nouveau demo en utilisant un proto vierge en chargeant myParameters.json.


#### Pour visuliser les données  utilisées par le dashboard vous pouvez utiliser l’extension simple websocket 

#### Voici les routes pous les donnée:

#### Copier dans URL:

##### DataVegetal  :                       wss://localhost:8080/dataVegetal

##### Espaces Vegetalisées:           wss://localhost:8080/dataEspacesVegetalisesPourcentageLyon

##### DataGeoLyon :                     wss://localhost:8080/dataGeoLyon

##### DataAlignements                  wss://localhost:8080/dataAlignements

##### DataParcsJardins                  wss://localhost:8080/dataParcsJardins

---

## Intégration du note book sur une page web

Le dashboard à été réalisé en utilisant du d3.js avec les notebook observable.

### Prérequis avoir un compte observable et faire un fork du notebook

#### 0. Allez sur le lien du notebook: https://observablehq.com/@moustapha/modular-dashboard-with-websocket/3?oetm_referrer=https%3A%2F%2Flocalhost%3A3001%2F&oetm_route=%2F%40moustapha%2Fmodular-dashboard-with-websocket%2F3


#### 1. Cliquer sur l'onglet en haut et à droite dans la fenetre qui s'ouvre taper sur Embed cells>

#### 2. Une fenetre s'ouvre et vous avez la possiblité de choisir les cellules à afficher.Nous avons décider de prendre le notebook entier en selectionnant Entire notebook>

#### 3. Puis sur la meme fenetre selectionner l'option iframe et cliquer sur copy pour copier le code dans un fichier.Pour nous c'est le fichier dashboard.ejs dans le repertoire /var/www/erasme/views>

## Dashboard en version websocket
Ajouter des données avec les websocket
```
dataVegetal = Generators.observe(notify => {
  const data = [];
  const socket = new WebSocket("wss://localhost:8080/dataVegetal");
  socket.onerror = function(error) {
    notify(Promise.reject(new Error("socket error: " + error.message)));
  };
  socket.addEventListener("open", () => {
    socket.send(
      JSON.stringify({
        hello: { sid: "mystream.binance-btc-usd", isNew: false }
      })
    );
  });
  socket.addEventListener("message", message => {
    if (JSON.parse(message.data).type === "dataVegetal") {
      data.shift();
      data.push(JSON.parse(message.data).value);
      notify(data[0]);
    }
  });
  notify(data[0]);
  return () => socket.close();
})

'''
## Dashboard en version API

###### On peut aussi allimenter le dashboard en utilisant les données de l'API devéloppée ou de datagrandlyon voir https://observablehq.com/@moustapha/dashboard-modulable.

### Exemple sur les données des espaces vegetal

'''
urlEspacesVegetal = "http://localhost:3001/api/espacesvegetal"

'''

'''
vegetal = fetch(urlVegetal).then(response => {
  return response.json();
})
'''
### Exemple 2 sur les données des arbres vegetal
'''
'''
urlVegetal = "http://localhost:3001/api/espacesvegetal"
'''
'''
Espacevegetal = fetch(urlEspaceVegetal).then(response => {
  return response.json();
})
'''
