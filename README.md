```…``` en ES6
===================
### Table of contents

Décomposition, Spread Operator & rest parameter en ES6
-------------

----------


Trois petits points
-------------

Les trois petits points (...) ne sont pas un opérateur commun en programmation contrairement au = ou au !. C'est ES2015 ou ES6 qui a ajouté cet opérateur à la syntaxe de Javascript et c'est clairement un bonne chose.

Les trois petits points sont en fait deux choses distinctes, le **rest parameter** et le **spread operator.**


La décomposition (destructuring) d'un Array
-------------

La **décomposition** consiste à "décomposer" les structures complexes (tableau, objet) pour en extraire les valeurs, les décomposer en plusieurs valeurs.
Chaque itérable (c'est à dire chaque objet global auquel on peut appliquer la méthode length) peut être décomposer (destructuré).
L'intérêt en ES6 est de rendre ce genre de manipulation plus **simple**, le code plus **lisible** et **scalable**.

Pour chaque exemple nous allons vous montrer une comparaison entre la syntaxe en **ES5** et en **ES6**.

### Décomposition d'un tableau

#### Comment assigner les variables d'un tableau à des varaibles ?

##### **ES5**

```
var animals = ['Hugo', 'Enora', 'Renan', 'Theo']
// nous assignons les valeurs à des variables.
var chien = animals[0]
var chat = animals[1]
var cheval = animals[2]
var singe = animals[3]

console.log(chien, chat, cheval) // Hugo Enora Renan
```

##### **ES6**

```
const animals = ['Hugo', 'Enora', 'Renan', 'Theo']

// nous assignons les valeurs à des variables.
const [chien, chat, cheval, singe] = animals

console.log(chien, chat, cheval) // Hugo Enora Renan
```

Le résultat est le même mais avec la décomposition on gagne en **rapidité d'exécution** et en **lisibilité**.

**[⬆ back to top](#table-of-contents)**

#### Comment récupérer le premier et le troisième élément de mon tableau ?

##### **ES5**
En ES5 on doit récupérer le premier et le troisième éléments du tableau avec leur index.
```
var animals = ['Hugo', 'Enora', 'Renan', 'Theo']

// nous assignons les valeurs à des variables grâce à l'index du tableau
var chien = animals[0]
var singe = animals[3]

// console.log(chien, singe) // Hugo Theo
```

##### **ES6**

```
const animals = ['Hugo', 'Enora', 'Renan', 'Theo']
const [chien,,, singe] = animals

// console.log(chien, singe) // Hugo Theo
```
**[⬆ back to top](#table-of-contents)**

#### Comment assigner les valeurs d'un tablau à des variables avec des valeurs par défault ?

##### **ES5**
```
var animals = ['François', 'Arthur'];

var chien = typeof animals[0] == 'undefined' ? 'Hugo' : animals[0];
var chat = typeof animals[1] == 'undefined' ? 'Enora' : animals[1];
var singe = typeof animals[2] == 'undefined' ? 'Theo' : animals[2];

console.log(chien, chat, singe); // François Arthur Theo
```

##### **ES6**

```
const animals = ['François', 'Arthur']
const [chien = 'Hugo', chat = 'Enora', singe = 'Theo'] = animals

console.log(chien, chat, singe) // François, Arthur, Theo
```

**[⬆ back to top](#table-of-contents)**

#### Comment copier un tableau sans avoir de référence entre les deux, pour garder l'immutabilité de nos tableaux ?

##### **ES5**

On est obligé d'utiliser la method Object.assign, qui copie toutes les valeurs enumerables de notre tableau
Le premier parametre de la methode est l'objet cible (pour nous un tableau), le deuxieme parametre est la source qu'on veut copier.

```var friends = ['renan', 'hugo']
var newFriends = Object.assign([], arr);

// On veut maintenant rajouter un element à notre tableau newFriends, sans affecter friends.

newFriends.push('enora')

console.log(newFriends); // ['renan', 'hugo', 'enora']
console.log(friends); // ['renan', 'hugo'] (inchangé)
```

##### **ES6**

En es6, cela devient beaucoup plus simple et lisible pour copier notre tableau
```
var friends = ['renan', 'hugo']
var newFriends = [...friends]
newFriends.push('enora')
console.log(newFriends); // ['renan', 'hugo', 'enora']
console.log(friends);  // ['renan', 'hugo'] (inchangé)
```
#### Comment manipuler les tableaux dans tous les sens, avec push, unshift, concat et autres...

##### **ES5**

```
 var friends = ['enora', 'hugo'];
```

```
  // method push

  var newFriends = ['theo', 'renan'];
  Array.prototype.push.apply(friends, newFriends);
  console.log(friends) // ['enora', 'hugo', 'theo', 'renan'];
```

```
  // method unshift

  var friendly = ['daniel', 'christopher'];
  Array.prototype.unshift.apply(friends, friendly);
  console.log(friends) // ['daniel', 'christopher', 'enora', 'hugo', 'theo', 'renan'];
```

```
  // method splice

  friends.splice(2, 0, 'julien', 'alexandre');
  console.log(friends) // ['daniel', 'christopher', 'enora', 'julien', 'alexandre', 'hugo', 'theo', 'renan'];
```

```
  // method concat

  var bestFriends = ['camille', 'amine'];
  // On ajoute les éléments de arr2 après ceux de arr1
  var newBestFriends = friends.concat(newBestFriends);

  console.log(newBestFriends) // ['daniel', 'christopher', 'enora', 'julien', 'alexandre', 'hugo', 'theo', 'renan', 'camille', 'amine'];
```


##### **ES6**

```
let friends = ['enora', 'hugo']
```

```
// method push

let newFriends = ['theo', 'renan']
friends.push(...newFriends);
console.log(friends) // ['enora', 'hugo', 'theo', 'renan']
```

```
// method unshift

let friendly = ['daniel', 'christopher']
friends.unshift(...friendly);
console.log(friends) // ['daniel', 'christopher', 'enora', 'hugo', 'theo', 'renan']
```

```
// method splice

let bigFriends = ['julien', 'alexandre']
friends = ['daniel', 'christopher', 'enora', ...bigFriends, 'hugo', 'theo', 'renan']
// On peut ici insérer un tableau dans un autre très facilement.
console.log(friends) // ['daniel', 'christopher', 'enora', 'julien', 'alexandre', 'hugo', 'theo', 'renan']
```

```
// method concat

let bestFriends = ['camille', 'amine'];
let newBestFriends = [...friends, ...bestFriends];

console.log(newBestFriends) // ['daniel', 'christopher', 'enora', 'julien', 'alexandre', 'hugo', 'theo', 'renan', 'camille', 'amine']
```
#### Comment sortir le premier élément du tableau en laissant le reste des éléments dans un tableau.

##### **ES5**

```
var animals = ['singes', 'Enora', 'Renan', 'Theo']
// nous assignons les valeurs à des variables grâce à l'index du tableau
var type = animals[0]

// Pour garder le premier tableau immutable, il faut le copier
var singes = Object.assign([], animals);
singes.shift(); // On retire le premier élément

console.log(type) // 'singes'
console.log(singes) // ['Enora', 'Renan', 'Theo']

// Cette méthode est fastidieuse et nous sommes obligé d'utiliser Object.assign pour garder le premier tableau immutable.
```
##### **ES6**

```
let animals = ['singes', 'Enora', 'Renan', 'Theo']
let [type, ...singes] = animals

console.log(type) // 'singes'
console.log(singes) // ['Enora', 'Renan', 'Theo']

// En es6 le spread operateur garde notre premier tableau immutable, et le code est beaucoup plus lisible et rapide.
```

#### Attention au scope de la décomposition

Lorsqu'on utilise la décomposition, par exemple pour copier un tableau, elle ne s'applique qu'au premier niveau de profondeur.
C'est à dire que la décomposition n'est pas effective sur des tableaux qui seraient présent à l'interieur de notre tableau copié.
Les tableaux internes ne seront pas immutable.

##### **Exemple**

```
const car = [['Mercedes'], ['Renault'], ['Porshe']];
const carCopy = [...a]; // carCopy vaut [['Mercedes'], ['Renault'], ['Porshe']]

// On va appliquer la methode shift à deux reprises sur notre tableau pour retirer le premier élément dans notre premier tableau.
carCopy.shift().shift();

console.log(carCopy) // [[], ['Renault'], ['Porshe']]
console.log(car) // [[], ['Renault'], ['Porshe']]
```

On voit bien que dans cet exemple, le tableau au second niveau est mutable, il y a donc des limites sur la décomposition.
En ES5 le problème persistera car même avec la method Object.assign(), on obtiendra le même résultat.


La décomposition des objets
-------------

La décomposition des objets est relativement la même que celle des tableaux avec quelques spécificités supplémentaires. La principale difference entre ES5 et ES6 est **la syntaxe qui est simplifiée en ES6**.

#### Exemple en ES5

```
// Partons d'un objet `notesHetic`
var notesHetic = {
  JS : 15,
  UX : 14,
}

// La syntaxe en ES5 est la suivante :
var JS = notesHetic.JS
var UX = notesHetic.UX

JS // 15
UX // 14

```
#### Exemple en ES6

```
// Désormais en ES6, la syntaxe est la suivante :
const { JS, UX } = notesHetic
JS // 15
UX // 14

// On peut bien entendu déstructurer la valeur retournée par une fonction, pour peu qu'il s'agisse d'un objet ou d'un tableau
const getnotesHetic = function() {
  return {
    JS: 15,
    UX: 14,
  }
}
const { JS, UX } = getnotesHetic()
JS // 15
UX // 14

```

Le rest parameter
-------------

**Le rest parameter** sert à stocker une liste indéfinie de valeurs sous forme de tableau. On dit paramètre de reste car il est passé en paramètre d'une fonction. Il est possible de ne pas insérer tous les arguments dans le paramètre rest.

L'intérêt de cet opérateur : **assembler plusieurs valeurs dans un tableau.**

#### Exemple en ES5

```
  var myArray = ['fruits', 'pomme', 'poire', 'orange']

    function argsToObject(val1, val2, val3) {
  let object = {};
  var array = [];
  for (let i = 1; i < arguments.length ; i++) {
    array.push(arguments[i])
    }
  object[val1] = array
  return object;
}
```
#### Exemple en ES6

```
// ...values -> récupère tous les paramètres sauf le premier paramètre.
    function argsToObject(keys, ...values) {
        let object = {}
        object[keys] = values

        return object
    }
```

Résultat pour les deux cas :
```
   {
      fruits: ['pomme', 'poire']
    }
```

Qu'on écrive en ES5 ou ES6, le résultat est le même mais la syntaxe est différente. Cependant, en ES6 on a une syntaxe plus courte donc plus légère.

En comparaison, l'objet "arguments" prends soit tout les paramètres soit aucun. Il n'est pas utilisable dans les arrow functions et se révèle moins performant que le rest parameter.

**Note **:  Lorsque le rest parameter est utilisé avec une fonction, l'objet arguments n'est plus disponible à l'intérieur de celle-ci.
