class: center, middle

# Migrez vos apps AngularJS vers React
# au fil de l'eau !

---

# Agenda

1. Pourquoi migrer ?
2. Comment migrer ?
3. react2angular à la rescousse

---

name: why

# 1. Pourquoi migrer ?

.grid[
.left[
![left-aligned image](img/andularjs_dead.jpg)]
.right[
![Right-aligned image](img/killed_by_google.png)]]

[Note de fin support AngularJS](https://blog.angular.io/discontinued-long-term-support-for-angularjs-cc066b82e65a)

---

name: why-react

# 1. Pourquoi migrer... vers React ?

- Recommendation de la `COP Front` (jusqu'à avis contraire)
- Stack toujours maintenue et qui continue d'évoluer
- Bonne maitrise de la stack au sein d'AXA et sur le marché
- Librairies à disposition en interne pour faciliter développement et maintenance (`toolkits`, ...)

.center[![i just migrate to react](https://i.imgflip.com/78l9y9.jpg)]

---

name: how

# 2. Comment migrer ?

- Effectuer une refonte complète de l'application

.pure-table.pure-table-bordered.pure-table-striped.smaller-font[
| Avantages                                 | Inconvénients                                                                     |
|-------------------------------------------|-----------------------------------------------------------------------------------|
| Implication de l'équipe de développement  | Complexe sur des sujets majeurs, avec des roadmap chargées et de fortes deadlines |
| Refonte à l'état de l'art                 | Presque impossible à mettre en oeuvre dans les faits                              |
| Pas de configuration spécifique au projet |                                                                                   |]

---

# 2. Comment migrer ?
- Effectuer une migration par route

Avoir deux applications : une dans la technologie actuelle, et l'autre dans la technologie cible. Chaque route de l'application redirigera ensuite vers la nouvelle ou vers l'ancienne version.

.pure-table.pure-table-bordered.pure-table-striped.smaller-font[
| Avantages                 | Inconvénients                              |
|---------------------------|--------------------------------------------|
| Refonte à l'état de l'art | Double application (coûts supplémentaires) |
| Facilité de configuration | Pages indépendantes                        |
|                           | Gestion de l'état dans un système externe  |
|                           | Router côté back-end                       |
|                           | Migration plus complexe (page entière)     |]

---

# 2. Comment migrer ?
- Effectuer une migration par composants

Conserver la même application en AngularJS dans laquelle des composants React seront traduits en composants AngularJS au moment de la build.

.pure-table.pure-table-bordered.pure-table-striped.smaller-font[
| Avantages                 | Inconvénients                              |
|---------------------------|--------------------------------------------|
| Refonte à l'état de l'art | Double application (coûts supplémentaires) |
| Facilité de configuration | Pages indépendantes                        |
|                           | Gestion de l'état dans un système externe  |
|                           | Router côté back-end                       |
|                           | Migration plus complexe (page entière)     |]

Plus d'informations : [Guide de migration de la COP Front](https://dev.azure.com/axafrance/CoP%20Front/_git/wiki?path=/migration/index.md&_a=preview)