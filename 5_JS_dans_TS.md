# Utilisez un projet JavaScript dans un projet TypeScript

Chaque bibliothèque installable via npm, est documentée sur le site de ce dernier.
Si on veut utiliser une bibliothèque JS dans notre projet TS, on doit vérifier le typage (?) de cette librairie.

Trois types d'information sont visibles à ce sujet sur le site de npm:

- le symbole `TS` indique que les types TS sont disponibles pour la bibliothèque: on n'a alors rien à faire;
- le symbole `DT` indique que les _déclarations de types_ peuvent être installées via npm:
Le projet DefinitelyTyped a pour ambition de fournir les fichiers de déclaration de types d’un maximum de librairies JavaScript.
Quand le symbole DT existe, les types doivent être installés via la commande `npm install @types/NOM_DE_LA_LIBRAIRIE`, par exemple `npm install @types/react`, ce qui rend alors la bibliothèque compatible instantanément avec notre projet TS.

- l'absence de symbole à ce sujet sur le site de npm (à droite du nom de la bibiliothèque) indique qu'on doit écrire les types TS nous-mêmes (c'est assez rare heureusement):
Pour ce faire, on va créer un dossier `types` puis un fichier `nom-de-la-biblio.d.ts`, par exemple `to-no-case.d.ts`; et on va écrire dedans la signature de la fonction `toNoCase`, qu'on va utiliser en TS au lieu du JS pour nous :

```TS
declare module "to-no-case" {
    export default function toNoCase(param: string): string; // on a vérifié dans la doc de la biblio avant de déclarer les types hein
}
```

Ainsi, en exécutant ce code avant l'import de la fonction JS, TS sait comment s'en servir, ce qui résout le problème en important ce fichier en plus du module `to-no-case` dont on a besoin ici :

```TS
import './types/to-no-case.d.ts';
import toNoCase from 'to-no-case';
const str = toNoCase('my-string');
```

Et si le problème est fréquent, on peut aussi configurer la clé de configuration `include` du fichier `tsconfig.json`, pour que les fichiers du dossier `types` soient lus par TS (voir la doc si on doit creuser ça en détail).
