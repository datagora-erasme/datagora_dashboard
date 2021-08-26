# Guide installation Dashboard

## Introduction
Le projet Dashboad est piloté par Erasme  dans le cadre de Datagora dont l'objectif est de mettre en place un tableau de bord modulable applicable à tout type de donné et facilement replicable dans d'autre contexte.Elle permet de visualiser différent KPI sur la végétalisation à travers différents graphes afin d'aider les collctivités à la prise de décision.

---
## Installation 

### 1. Installation server web et version websocket

#### Prérequis
* Installer node.js

* Installer les module complémentaire ws:

'''
    npm install ws
'''
'''
   npm install socket.io
'''
'''
npm install express

'''
npm install ejs

'''
'''
npm install nodemon
'''
### lancer de l'application 

* Lancer le serveur avec la commande "node server.js depuis le repertoire WebsocketServer

'''
   node server.js
'''

* Aller sur le lien https://localhost:3001 pour voir la page d'accueil de l'application

### 



## Intégration du note book sur une page web
Le dashboard à été réalisé en utilisant du d3.js avec les notebook observable.
### Prérequis avoir un compte observable et faire un fork du notebook

#### 0. Allez sur le lien du notebook: https://observablehq.com/@moustapha/modular-dashboard-with-websocket/3?oetm_referrer=https%3A%2F%2Flocalhost%3A3001%2F&oetm_route=%2F%40moustapha%2Fmodular-dashboard-with-websocket%2F3


#### 1. Cliquer sur l'onglet en haut et à droite dans la fenetre qui s'ouvre taper sur Embed cells>

#### 2. Une fenetre s'ouvre et vous avez la possiblité de choisir les cellules à afficher.Nous avons décider de prendre le notebook entier en selectionnant Entire notebook>

#### 3. Puis sur la meme fenetre selectionner l'option iframe et cliquer sur copy pour copier le code dans un fichier.Pour nous c'est le fichier dashboard.ejs dans le repertoire /var/www/erasme/views>

## Dashboard en version websocket
Ajouter des données avec les websocket
'''
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