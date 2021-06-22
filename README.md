# TP2-NodeJS

## URL du pad

https://etherpad.in2p3.fr/p/INUKA-Web

## URL du cours

https://perso.liris.cnrs.fr/lionel.medini/enseignement/M1IF13/revealJS/#cm1-stackjs

## Notes de cours / TP

Pour développer une application, il faut :

- Programmer
- S'appuyer sur des "dépendances" -> dependency management tools

Ensuite, il faut "construire" (ou "packager") l'application complète (à partir des dépendances, des différents modules que vous aurez programmés, ect.). -> build tools

Enfin, il faut le faire "tourner" dans un environnement d'exécution -> runtime

Particularités pour une application Web  :

- Au départ, tout est sur un serveur
- le client est un navigateur
    
### Premier programme en NodeJS

Enregistrer ce fichier avec une extension `.js`
    
```javascript
const http = require('http');
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});


server.listen(3000, '127.0.0.1', () => {
  console.log(`Server running at http://127.0.0.1:3000`);
});
```

Pour exécuter, taper `node` + le nom du ficher 

voila ce j'ai: Server running at http://127.0.0.1:3000/

C'est très bien : ouvrez un navigateur à cette URL...

### Créer un nouveau projet avec NPM

- Créer un nouveau dossier vide
- se placer dedans (grace à la commande "cd")
- taper : npm init (c'est ce qu'on appelle la Command Line Interface, ou CLI de NPM)
  - Quand vous avez tapé npm init, vous répondez aux questions...
  - Quand il vous propose une valeur entre parenthèses, vous appuyez directement sur entrée
  - Quand il vous demande une description, vous tapez du texte, puis entrée
  - Quand il vous demande d'autres renseignements que vous n'avez pas, vous laissez vide et tapez sur entrée
- dans le fichier package.json, dans la section "scripts", rajouter la ligne :<br>
    `"start": "node index.js",`

### Installer une dépendance

Taper `npm install express`

Il rajoute dans le répertoire :

- 1 fichier package-lock.json -> généré et géré automatiquement
- 1 dossier node-modules

### Commencer à programmer l'application

Créer un fichier `index.js`, et mettre juste un affichage dedans :

`console.log('COUCOU !!!')`

### Exécuter l'application

Taper dans la ligne de commande :
 
`npm start`

### Améliorer l'application

- Modifier le fichier index.js pour qu'il corresponde au premier programme Express ici : http://expressjs.com/en/starter/hello-world.html
- On va maintenant récupérer les paramètres de la requête avec "req.query". La documentation est ici : http://expressjs.com/en/5x/api.html

Le code à rajouter : 

```javascript
app.get('/disbonjour', (req, res) => {
  res.send('Bonjour ' + req.query.personne)
})
```

L'URL à taper dans votre navigateur est par exemple : http://localhost:3000/disbonjour?personne=Seraphin

### Créer une page d'accueil pour l'application

- On veut faire un formulaire qui permet de passer des paramètres et d'appeler la route précédente.

Code de la page `index.html` :
    
```html
<!doctype html>
<html>
<head>
        <title>La page qui dit bonjour</title>
</head>
<body>
        <h1>Dites bonjour à qui vous voulez</h1>
        <form action="disbonjour" method="GET">
                <p>Entrez le nom de la personne
                        <input type="text" name="personne">
                        <input type="submit" value="Envoyer">
                </p>
        </form>
</body>
</html>
```

### Servir cette page d'accueil et lier les éléments de l'application

Il faut modifier la fonction de callback de "app.get("/")" pour qu'elle exécute l'instruction suivante :

`res.sendFile('index.html', {"root":"."})`

## &Agrave; faire pour la prochaine fois

- envoyer les paramètres en POST et non en GET : docs à http://expressjs.com/en/5x/api.html#app.post.method et http://expressjs.com/en/5x/api.html#req.body
- faire en sorte que `/disbonjour` renvoie une page HTML (et pas juste du texte) : modifier le contenu de "req.send" en y rajoutant du code HTML
- faire en sorte d'inclure l'horloge côté client qu'on a faite la semaine dernière dans la réponse de disbonjour :
  - rajouter une balise "script" dans la page HTML
  - servir le fichier de script en question à l'aide de http://expressjs.com/en/5x/api.html#res.sendFile (regarder ce qui a été fait pour servir le fichier index.html).
