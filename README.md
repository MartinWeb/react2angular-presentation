# react2angular-presentation
 
## Installation

Aucune installation n'est requise en amont de la présentation, à l'exception d'un serveur web pour faire tourner cette dernière.
Une liste de serveur web se trouve [ici](https://gist.github.com/willurd/5720255)

Par exemple, pour un http-server de NodeJS, il suffit d'installer la dépendance dans npm :

```bash
npm install -g http-server
```

## Lancement

Etant donné que nous avons exporté le markdown de la présentation dans un fichier dédié, la méthode consistant à simplement exécuter le fichier html ne peut être utilisée. Pour que la présentation fonctionne, il faut lancer un serveur http au sein de la solution pour qu'il rende l'ensemble des fichiers statiques.

Pour se faire, il faut se déplacer dans le répertoire du projet :

```bash
cd react2angular-presentation/
```

Puis, lancer simplement le serveur http :

```bash
http-server -p 8000
```