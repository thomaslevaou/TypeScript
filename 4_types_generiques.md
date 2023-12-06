# Rendez vos types génériques

Le type `unknown` peut être utilisé en TypeScript pour indiquer qu'on ne sait pas quel type on attend.
Le type `any` existe aussi pour cela, mais il n'est pas recommandé de l'utiliser car buggogène (sur les propriétés des objets par exemple).

Afin d'éviter des duplications de code, il peut être intéressant d'utiliser des **types génériques**. Il s'agit de types pouvant prendre en paramètre un autre type.

On peut appliquer des types génériques aux alias, interfaces et fonctions comme ci-dessous :

```TS
type Shop<T> = {
    name: string;
    owner: Character;
    // Nous utilisons notre paramètre ici, à la place de "unknown"
    items: Array<T>;
};

// Équivalent du type générique que nous venons de voir, avec une interface
interface Shop<T> {
    name: string;
    owner: Character;
    items: Array<T>;
};

// Une fonction générique
function createShop<T>(name: string, owner: Character, items: Array<T>;): Shop<T> {
    return { name, owner, items };
}

// Appel de la fonction générique pour un marchand "d'équipements", dont le nom est "My Armory" et le propriétaire est bob, sans item (qui seraient alors des équipements si le tableau avait des valeurs)
const armory = createShop<Equipment>('My armory', { name: 'Bob', life: 100, attack: 1, defense: 2 }, []);
```

On peut faire pas mal de trucs en plus avec des types génériques (combiner les uns avec les autres, contraindre leurs paramètres, créer des types conditionnels ou même écrire de véritables fonctions, ...) mais c'est hors scope du cours.

Quand on utilise un tableau de données du même type avec un tableau `Array`, on utilise en réalité un type générique.
Le type `Array` pourrait littéralement être défini comme `type Array<T> = T[];`.

Pour nous aider à faire des opérations courantes, TypeScript propose d'autres **utility types**, comme :

- `Partial`, qui rend toutes les propriétés d'un objet optionnelles:

```TS
type Character = {
    // Toutes les propriétés sont requises (elles n'ont pas le signe "?")
    name: string;
    life: number;
    attack: number;
    defense: number;
};
const myCharacter: Partial<Character> = {
    // On ne fournit que le nom, pas le reste des propriétés.
    // On n'a pas d'erreur car "Partial" rend
    // toutes les propriétés optionnelles.
    name: 'Mario',
};
```

- `Record`, qui permet de rendre générique des objets :

```TS
// `CollectionOfNumbers` est un type qui veut dire "objet dont les clés sont des chaînes de caractère, quelle qu'elles soient, et les valeurs des nombres"
type CollectionOfNumbers = Record<string, number>;
const stats: CollectionOfNumbers = {
    age: 45,
    life: 100,
    magic: 10,
    whateverTheNameItMustContainANumber: 20,
};
```

```TS
// On peut passer par une union pour dire par exemple ici "Objet dont les clés sont soit 'life', soit 'attack', soit 'defense', et les valeurs des nombres"
type StatisticNames = 'life' | 'attack' | 'defense';
const stats: Record<StatisticNames, number> = {
    life: 100,
    attack: 10,
    defense: 20,
};
```

Et il y a plein d'autres types utilitaires qui existent, et qui sont accessibles dans la [doc de TypeScript](https://www.typescriptlang.org/docs/handbook/utility-types.html), comme `Omit` utilisé dans l'exercice pour récupérer un objet sans une propriété.
