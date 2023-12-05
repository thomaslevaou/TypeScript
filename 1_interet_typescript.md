# Découvrez l'intérêt de TypeScript

## Présentation globale

TypeScript, c'est JavaScript avec des types. Toute variable ou fonction a un type associé.
Ainsi, le développeur est prévenu d'éventuelles erreurs de code pendant son écriture, et non pendant son exécution. Ce qui lui fait gagner du temps, même si le code est un peu plus chargé et demande plus de rigueur préalable au développeur.

On dit que JavaScript est **faiblement typé**, quand TypeScript est qualifié de **fortement typé**. On dit aussi que TypeScript est un **superset** de JavaScript: du code en JS pur fonctionne en TypeScript.

On peut configurer le TypeScript avec un fichier de config (`tsconfig.json`) pour paramétrer la sévérité du langage. On peut aussi faire cohabiter des fichiers JS et TS dans un projet sans que ça ne pose de gros problème en soi de compilation.

Le code TypeScript est _compilé_ en JS avant d'être envoyé au navigateur (ce dernier ne comprenant pas le langage JS directement).

## Installation

Afin de ne pas avoir de souci avec le cours, je vais me mettre sur Node 18 (même si la version 20 est sortie en LTS maintenant).

```bash
nvm use 18
mkdir my-project
cd my-project
npm init -y
npm install --save-dev typescript
```

On peut alors créer des fichiers TypeScript. La compilation en JS se fait via la commande suivante :

```bash
npx tsc my-file.ts # tsc pour "TypeScript Compilator" (npx l'utilitaire installé avec node.js pour lancer une commande)
```

Après l'exécution de cette commande, on voit bien le fichier qu'on vient d'écrire en TypeScript, compilé en JavaScript.
Si je modifie volontairement une constante, ou que je souhaite mettre une string à la place d'un number TS, alors lorsque j'exécuterai la commande ci-dessus, la commande me signalera une erreur.

Notons que VS Code signale instantanément les erreurs TypeScript.