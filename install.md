md`
# Installation du serveur web et websocket
#### 0. Pr�alable : installation de *node.js*
#### 1. Copier le r�pertoire ./WebsocketServer et ses fichiers dans un r�pertoire d�di� du serveur.
#### 2. Installer les modules compl�mentaires "ws", "socket.io", "express" et "ejs" en ligne de commande avec \`\`npm install\`\` 
#### 3. Modifier l'adresse du serveur dans le javascript client pour l'utilisation de socket.io : dans les fichiers js /public/js remplacer \`\`let socket = io.connect('https://localhost:3001')\`\` par \`\`let socket = io.connect('https://ADRESSE_SERVEUR:3001')\`\`
#### 4. Si besoin (firewall), autoriser les ports 8080 et 3001.
#### 5. Lancer le serveur avec la commande "node server.js depuis le r�pertoire WebsocketServer"

**NB** : les certificats de s�curit� se trouvent dans le r�pertoire ssl. Si besoin, en g�n�rer de nouveaux.
`