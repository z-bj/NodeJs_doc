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


![](https://github.com/z-bj/NodeJs_doc/blob/master/2023-02-17%2009_19_41-Volta%20-%20The%20Hassle-Free%20JavaScript%20Tool%20Manager%20-%20Brave.jpg)

<hr>


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

<hr>




## À propos de ce tutoriel
Dans ce premier chapitre consacré à NodeJS nous allons voir comment lire et écrire des fichiers.

## Support de import EcmaScript
Par défaut, les version actuelles de NodeJS n'utilisent pas par défaut le système d'import d'EcmaScript et ne comprendront pas la syntaxe avec import. Pour forcer ce support vous avez 2 possibilités.

Changer l'extension de vos fichier pour utiliser .mjs
Ajouter une propriété "type": "module"dans votre package.json (vous pouvez générer ce fichier à l'aide de la commande npm init)
## Les modules NodeJS
Pour importer les modules propre à NodeJS on utilisera le nom du module préfixé par node:.

``` bash

import fs from 'node:fs'
const content = fs.readFileSync('demo.txt')

```

On aura aussi la possibilité de n'importer que la méthodes qui nous intérèsse.

``` bash

import { readFileSync } from 'node:fs'

const content = readFileSync('demo.txt')

```


### Synchrone ou Asynchrone
La plupart des méthodes liées aux fichiers disposent de 3 versions

fs.<nom>Sync permet de faire une opération de manière synchrone (en bloquant votre script)
fs.<nom> permet de faire une opération de manière asynchrone en utilisant un callback en paramètre.
fsPromises.<nom> permet de faire une opération de manière asynchrone en renvoyant une promesse.
En général, on aura tendance à utiliser la version avec les promesses vu qu'elle offre la forme la plus moderne. Par exemple pour lire un fichier on utilisera la méthode de cette manière.
    
    
    
    
    
``` bash
    
import { readFile } from 'node:fs/promises';

try {
  const content = await readFile(fileName, { encoding: 'utf8 });
} catch (err) {
  console.error("Impossible de lire le fichier " + err);
}
    
```


    
    
## Méthodes utiles
    
Pour découvrir les différentes méthodes vous pouvez parcourir la documentation sur le système de fichier mais je vous propose une sélection des méthodes les plus utiles.

readFile permet de lire un fichier (utiliser l'option encoding pour obtenir une chaîne de caractère).
writeFile permet d'écrire dans un fichier (utiliser l'option flag en fonction de ce que vous voulez faire).
copyFile
rename
rm permet de supprimer un fichier.
readdir permet de lire le contenu d'un dossier
stat permet d'obtenir des informations sur un fichier (taille, date de création, date de modification...)

## Attention au chemin
    
Attention, si les chemins que vous passez à ces différentes méthodes sont relatif ils seront résolus par rapport au dossier dans lequel vous éxécutez le script NodeJS (et non pas relativement au fichier JavaScript dans lequel se trouve le code). Si vous voulez récupérer le chemin du fichier courant vous pouvez utiliser import.meta.url


``` bash

import { fileURLToPath } from 'node:url'
import { dirname, join } from 'node:path'

const directory = dirname(fileURLToPath(import.meta.url))
const content = readFile(join(directory, 'demo.txt'))
console.log(content)
    
```



    
## Lecture et écriture plus fine
Pour des opération plus fine sur les fichier il est possible d'utiliser les méthode write et read qu'il faudra utiliser sur un fichier préalablement ouvert.

``` bash
   
    import {open} from 'node:fs/promises'

const fileHandle = await open('hello.txt', 'a+')
try {
    fileHandle.write('Bonjour')
    const firstLetters = await fileHandle.read({position: 4, length: 3})
    console.log(firstLetters.buffer.toString('utf8')) // our
} finally {
    fileHandle.close() // On ferme le fichier quand on a finit de travailler
}
    
```







