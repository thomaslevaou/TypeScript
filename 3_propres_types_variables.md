# Créez vos propres types de variables

## Aliases et unions de types

On peut créer des **alias de type** en assimilant un type à un autre via un `=` :

```TS
type Age = number;
type Firstname = string;
type Lastname = Firstname;
```

Les alias de type commencent par une majuscule, par convention.
Ils permettent ainsi non seulement de clarifier un peu le code, mais peuvent aussi par exemple permettre de tolérer l'éventualité qu'une variable ait deux types différents, comme dans le code ci-dessous :

```TS
type CodeSecret = string | number;
const code1: CodeSecret = 123;
const code2: CodeSecret = '4@cK3r';
```

On parle alors **d'union de types**.

Une valeur JavaScript peut servir de type TypeScript valide, ce qui permet concrètement de créer des listes de valeurs autorisées :

```TS
type Creature = 'blob' | 'troll' | 'unicorn' | 'dragon';
function fightCreature(target: Creature) {}

fightCreature('dragon'); // OK !
fightCreature('fish'); // Erreur TS
```

## Applications aux objets et tableaux

On peut appliquer les types aux objets, donc l'application permet de rendre réutilisable des objets utilisés dans le code.
Ci-dessous, l'objet `{ life: number }` utilisé au chapitre précédent, devient réutilisable dans un type `Hero` si on en a besoin a d'autres endroits du code :

```TS
type Hero = {
    life: number;
    pet?: string; // Le "?" est là pour dire que la propriété est optionnelle
};
function damage(characterToDamage: Hero, amount: number): number
```

On peut également "fusionner" deux types en un seul type d'objet via le caractère `&`:

```TS
type Character = {
    name: string;
    life: number;
    attack: number;
    defense: number;
};
type Pet = Character;
type Hero = Character & {
    pet?: Pet;
};
```

On dit alors qu'un `Hero` est une **intersection** entre le type `Character` et `{ pet?: Pet }`.

On peut aussi utiliser le mot-clé **interface** pour définir une structure pour les objets :

```TS
interface Character { // Attention, il n'y a alors pas de `=` avant l'accolade ouvrante !
    name: string;
    life: number;
    attack: number;
    defense: number;
};
type Pet = Character; // On garde type ici, car c'est toujours un alias de Character
interface Hero extends Character { // Mais on passera plus par une forme de pseudo-héritage que par une intersection
    pet?: Pet;
};
```

Pour indiquer à TypeScript qu'on veut que tel tableau contienne tel type de valeurs, on peut ajouter `[]` à droite du type souhaité, ou utiliser la notation `Array<>` comme ci-dessous, en utilisant pour l'exemple le type ̀`number`:

```TS
type MyArrayOfNumbers = number[];
type MyArrayOfNumbers = Array<number>;
```
