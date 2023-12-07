# Manipulez la syntaxe de TypeScript

## Types primitifs

Les variables TypeScript s'écrivent selon la syntaxe `mot-clé nom-de-la-variable: type-de-la-variable = valeur-de-celle-ci`.
Par exemple, `let maVariable: number = 10`.

Notons que TS peut repérer automatiquement que telle variable doit être une string par exemple, juste en faisant `let fruit = 'fraise';` comme en JS standard. C'est juste moins clair à lire.

TypeScript propose **trois types primitifs**: `number`, `string` et `boolean`.
Attention, en JS les instructions `Boolean`, `Number` et `String` existent aussi, mais signifient autre chose. Les types TypeScript s'écrivent quasiment tout le temps en toutes minuscules !

Le type de retour d'une fonction peut être renseigné de manière similaire avant l'accolade ouvrante de la fonction.

On peut donc alors écrire le code TypeScript suivant :

```TS
function addition(x: number, y: number): number {
    return x + y;
}
const result:number = addition(10, 20);
console.log(result);
```

Une combinaison "nom de la fonction + types des paramètres + type du retour" est appelée la **signature de la fonction**.

Les messages d'erreurs ne sont parfois pas clairs en TS. Si besoin, le site <https://ts-error-translator.vercel.app/> peut aider à dépanner pour aider à comprendre un message d'erreur TS.

Attention TS traduit quand même le code en JS, quand bien même il signale une erreur de compilation.

## Types des objets

On peut déstructurer un objet pour indiquer son type dans une déclaration de fonction, comme visible ci-dessous :

```JS
function damage(characterToDamage: { life: number }, amount: number): number {
    characterToDamage.life -= amount;
    return characterToDamage.life;
}
const result = damage({ life: 100 }, 12);
console.log(result);
```
