[JS side-server](https://grafikart.fr/tutoriels/javascript-server-nodejs-2080#autoplay)

## Plusieurs solutions

NodeJS initialement lancé en 2013 est la solution la plus répandue à l'heure actuelle.
Deno est une tentative du créateur de NodeJS de repartir sur de nouvelle base. Même si la technologie est intéréssante elle a du mal à obtenir suffisamment de traction (principalement à cause de son incompatibilité avec l'écosystème NodeJS déjà présent).
Bun est une initiative toute jeune (pas encore stable) qui se veut être une alternative à NodeJS en promettant notamment d'être compatible avec l'existant.

## Le principe de NodeJS

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


![]()
