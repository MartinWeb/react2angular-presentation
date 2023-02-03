class: center, middle

# Migrez vos apps AngularJS vers React
--
count: false
name: subtitle

.animate[
    # au fil de l'eau !]

---

# Agenda

1. Pourquoi migrer ?
2. Comment migrer ?
3. react2angular à la rescousse
4. Démo
5. Retour d'expérience

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
| Refonte à l'état de l'art                 |                                                                                   |
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
| Avantages                                       | Inconvénients                        |
|-------------------------------------------------|--------------------------------------|
| Migration au fil de l'eau                       | Découpage en composants obligatoires |
| Totalement invisible pour l'utilisateur         | Pas à l'état de l'art                |
| Parfaitement intégré dans les cycles de release | Plus long (intégré aux releases)     |]

Plus d'informations : [Guide de migration de la COP Front](https://dev.azure.com/axafrance/CoP%20Front/_git/wiki?path=/migration/index.md&_a=preview)

---

# 3. react2angular à la rescousse

.center[
## [React2angular](https://github.com/coatue-oss/react2angular)

![what is that](https://media.tenor.com/BsvJa7kN1TwAAAAC/what-is-that-what-the-fuck-is-that.gif)]

---
name: react2angular-first-slide

# 3. react2angular à la rescousse

React2angular est un package javascript permettant de convertir un composant React en composant AngularJS. Son équivalent angular2react existe également, et permet cette fois-ci de convertir un composant AngularJS en React.

### Très bien, mais comment ça fonctionne dans les faits ?

.center[![AngularJS vers React](https://raw.githubusercontent.com/coatue-oss/angular2react/master/logo.png)]

---

# 3. react2angular à la rescousse

Prenons un composant AngularJS d'une application.

```javascript
import angular from 'angular';
import template from './dap-distributor-pending.html';

export const DapDistributorPendingComponent: angular.IComponentOptions = {
    template,
};
```

```html
<div class="steps-container">
    <div id="error_details" class="container-fluid">
        <div class="panel panel-default">
            <div class="panel-body text-center">
                <h1>Demande d’autorisation préalable en cours d’instruction par les Engagements.</h1>
                <h2>Votre demande est traitée dans les 48 heures qui suivent la demande.</h2>
            </div>
        </div>
    </div>
</div>
```

---

# 3. react2angular à la rescousse

Après migration en React, il ressemblerait à cela :

```javascript
export const DapDistributorPending = () => (
    <div className="steps-container">
        <div id="error_details" className="container-fluid">
            <div className="panel panel-default">
                <div className="panel-body text-center">
                    <h1>Demande d’autorisation préalable en cours d’instruction par les Engagements.</h1>
                    <h2>Votre demande est traitée dans les 48 heures qui suivent la demande.</h2>
                </div>
            </div>
        </div>
    </div>
);
```

---

# 3. react2angular à la rescousse

Mais comment faire cohabiter des composants React et AngularJS dans la même application ?

- Installer les librairies nécessaires, notamment react2angular
```bash
npm install react2angular react react-dom
```
- Supprimer le composant AngularJS précédemment migré
.center.delete-angular-img[![suppression composant angular](https://i.imgflip.com/78ptjz.jpg)]

---

# 3. react2angular à la rescousse

- Exposez le composant React en AngularJS pour pouvoir l'utiliser dans l'application.

```javascript
import DapDistributorPending from '...';

// déclaration du module AngularJS
.component('dapDistributorPending', react2angular(() => DapDistributorPending))
```

```javascript
import React from 'react';
import { react2angular } from 'react2angular';
import DapDistributorPending from '...';

// Fichier d'index ou directement dans le composant React
const DapDistributorPendingComponent = react2angular(() => <DapDistributorPending />);
export { DapDistributorPendingComponent };

// déclaration du module AngularJS 
.component('dapDistributorPending', DapDistributorPendingComponent)
```

---

# 3. react2angular à la rescousse

Et c'est terminé !

Votre application AngularJS utilisera votre tout nouveau et tout beau composant React.

.center[![c'est magique](https://media4.giphy.com/media/Z5HVfEvnxr67u/giphy.gif?cid=ecf05e47g4hl5gcyw12a8i7w9w62236s2rglfphbq79nt3lw&rid=giphy.gif&ct=g)]

---

# 3. react2angular à la rescousse

Mais encore ?

Une application est rarement aussi simple qu'une somme de composants avec des templates. Elle peut comprendre des composants avec de multiples props, une gestion d'état dans un store, l'utilisation de services propres à AngularJS, du routing, ...

Par exemple : 
- si votre composant demande des props, react2angular vous permet de les passer

```javascript
const DapPendingEngagementAlertComponent = react2angular((props) => 
    <DapPendingEngagementAlert {...props} />);
```
- si vous utilisez redux dans votre application AngularJS, vous pouvez utiliser le package équivalent en React `react-redux`.
- si vous utilisez ui-router pour le routing, vous pouvez utiliser `@uirouter/react-hybrid`

---

# 3. react2angular à la rescousse

Ressources utiles

- [Exemple des prérequis à mettre en place sur le projet Gestion Contrats (tribu IARDPP)](https://dev.azure.com/axafrance/ContractsIARD/_git/Sources/pullrequest/100921)
- [Exemple des prérequis à mettre en place sur le projet MaMaison (tribu IARDPP)](https://dev.azure.com/axafrance/EMRH/_git/Sources/commit/e2c5f929e051191c99cd9cca9f159f06dede477f)
- [Exemple de migration de composants sur le projet MaMaison (tribu IARDPP)](https://dev.azure.com/axafrance/EMRH/_git/Sources/pullrequest/156343)

---

# 4. Démo

.center[![Démo](https://i.imgflip.com/3n1x6c.jpg)]

---

# 5. Retour d'expérience

Migration complète du SA mineur (~10k lignes de code) [Gestion contrats](https://dev.azure.com/axafrance/ContractsIARD) en quelques mois via du Mob Programming.

Migration en cours du SA majeur (~26k lignes de code) [Ma Maison](https://dev.azure.com/axafrance/EMRH) achevée à ~80%.

---

# 5. Retour d'expérience

Tips pour migrer efficacement :
- Commencez par migrer les composants du plus bas niveau dans le DOM
- Commencez par migrer les pages les plus simples de l'application en premier
- Assurez-vous d'une bonne couverture de tests d'intégration du composant avant la migration
- Profitez de la migration pour passer les composants en Typescript
- N'hésitez pas à utiliser les composants du toolkit quand c'est possible (les moins impactants en terme de design)
- Migrez les services AngularJS à la fin

---

# 5. Retour d'expérience

A votre tour de jouer !

.center[![En cours](img/78uf95.gif)]