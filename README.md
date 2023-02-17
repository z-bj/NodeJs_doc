[JS side-server](https://grafikart.fr/tutoriels/javascript-server-nodejs-2080#autoplay)

## Plusieurs solutions

NodeJS initialement lancé en 2013 est la solution la plus répandue à l'heure actuelle.
Deno est une tentative du créateur de NodeJS de repartir sur de nouvelle base. Même si la technologie est intéréssante elle a du mal à obtenir suffisamment de traction (principalement à cause de son incompatibilité avec l'écosystème NodeJS déjà présent).
Bun est une initiative toute jeune (pas encore stable) qui se veut être une alternative à NodeJS en promettant notamment d'être compatible avec l'existant.

## Le principe de NodeJS

![](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2008_41_59-JavaScript%20c%C3%B4t%C3%A9%20serveur%20%E2%80%94%20Formation%20Apprendre%20le%20JavaScript%20_%20Grafikart%20-%20Brave.jpg)

Le fonctionnement de NodeJS repose sur 2 fondations :

Le moteur JavaScript V8 open source de Google qui va permettre d'éxécuter le code JavaScript.
libuv qui permet de gérer l'I/O de manière asynchrone et qui permettra d'interagir avec le système (fichiers, réseaux...)
On ne va pas trop rentrer dans les détails mais cette combinaison permet d'accéder à des fonctionnalités systèmes de manière non bloquante (comme avec les timers que l'on a vu dans les bases du JavaScript).

``` javascript

import { readFile } from 'fs'

readFile('MonFichier.txt', (err, content) => {
    if (err) {
        throw err;
    }
    console.log('Mon fichier : ', content); 
});
console.log('Autres opérations')

```

Cette approche permet au fil principal (celui qui éxécute le JavaScript) de traiter plusieurs choses pendant que le système travail ce qui permet d'en faire plus.



![structure](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2008_32_23-JavaScript%20c%C3%B4t%C3%A9%20serveur%20%E2%80%94%20Formation%20Apprendre%20le%20JavaScript%20_%20Grafikart%20-%20Brave.jpg)

- V8 stable et puissant
- Node standar library --> library de function ayant attrait au systeme  Modules(reseau, read write files, server web creation.
- Library ecrite en C ---> EVENT LOOP --> eoute les events et executes le code de maniere asynchrone

### Non bloquant

![screen](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2008_40_15-JavaScript%20c%C3%B4t%C3%A9%20serveur%20%E2%80%94%20Formation%20Apprendre%20le%20JavaScript%20_%20Grafikart%20-%20Brave.jpg)

![](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2008_43_44-JavaScript%20c%C3%B4t%C3%A9%20serveur%20%E2%80%94%20Formation%20Apprendre%20le%20JavaScript%20_%20Grafikart%20-%20Brave.jpg)

### Weaknesses 


PHP --> sequentiel

![](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2008_45_53-JavaScript%20c%C3%B4t%C3%A9%20serveur%20%E2%80%94%20Formation%20Apprendre%20le%20JavaScript%20_%20Grafikart%20-%20Brave.jpg)

Node--> async

![](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2008_46_42-JavaScript%20c%C3%B4t%C3%A9%20serveur%20%E2%80%94%20Formation%20Apprendre%20le%20JavaScript%20_%20Grafikart%20-%20Brave.jpg)

### illisible

### Single Thread, ne rien faire qui demande beaucoup de calculs...
> GO, Rust permettent de creer un new thread pour gerer ces taches lourdes.
On peut mettre un systeme de cluster, mais c'est pas simple a utiliser, a la difference de d'autre systeme.

### Bas Niveau, 
la library standard offre peut de fonctionnalité notamennt pour creer des servers web, et on a vite besoin de servrces tiers.

Good!

- Beaucoup d'I/O --> call http / communication avec le syteme de firchier
- Multiplateform, Mac windows linux
- Un seul langage, un anneau pour les gouverner tous.
- facile a apprendre.

NPM, tres grosse communauté.


# À propos de ce tutoriel

Dans ce chapitre nous allons voir comment installer NodeJS sur Linux et MacOS avec Volta. Cet outil va vous permettre de gérer plusieurs version de NodeJS et de pouvoir verrouiller une version spécifique à votre projet.

Pour spécifier la version de NodeJS que l'on souhaite installer on pourra utiliser la commande.

``` bash
volta install node@18

```

Cela permet de définir la version qui sera utilisé par défaut mais lorsque l'on travaille sur un projet il sera préférable de verouiller la version utilisée à l'aide de la commande pin.

``` bash

volta pin node@18
```
Cette commande modifiera le fichier package.json pour ajouter une clef volta qui contiendra les versions des outils utilisés. Si un autre développeur travaille sur le projet avec volta, alors la même version sera utilisé (et téléchargé si nécessaire) lorsqu'il tapera une commande.







