## On se lance:

![Gif Cat jump](assets/img/jump.gif)


Maintenant que tu sais comment tu dois faire, tu crées un nouveau projet et on commence par ce simple code:

```
<div id="app">                                                                              HTML
    <h2>{{product}}</h2>
</div>
<script src="main.js"></script>
```

```
let app = new Vue({                                                                          JS
  el: '#app',
  data: {
    product: 'Chaussettes'
   
  } 
})
```
Voilà "Chaussettes" apparaît sur notre page web. Ça a marché. Les données de notre JavaScript apparaissent dans notre code HTML. Mais on a fait quoi en fait.

# On instancie la vue

```
let app= new Vue({options})
```
Une instance de Vue est la racine de notre application. Il est créé en y passant un objet d’options. Tout comme son nom l'indique, cet objet possède diverses propriétés facultatives qui permettent à l'instance de stocker des données et d'effectuer des actions.
___

# Connexion à un élément

```
el:#app,
```
L'instance Vue est ensuite connectée à un élément de votre choix, créant ainsi une relation entre l'instance et cette partie du DOM. En d'autres termes, nous activons Vue sur la div avec l'id de appen définissant '``#app``'l'élément ( el) avec lequel notre instance est connectée.
___

# Mettre des données à sa place

Une instance de Vue a une place pour les données, dans sa propriété data.

```
data:{
    product:"Chaussettes"
}
```
Les données de l'instance sont accessibles depuis l'intérieur de l'élément auquel l'instance est connectée.
___

# Utiliser une expression

Si nous voulons que notre _product_ apparaisse dans notre h1, nous pouvons mettre le _product_à l'intérieur de ces doubles moustaches.

```
<h1>{{product}}</h1>
```
À l'intérieur des doubles moustaches, nous utilisons une expression JavaScript.

![Gif moustache](https://media.giphy.com/media/Yjb1jDhMWswRG/giphy.gif)
___

# Terme important: expression

Les expressions nous permettent d'utiliser les valeurs de données existantes, ainsi que la logique, pour produire de nouvelles valeurs de données.

Lorsque Vue voit l'expression {{ product }}, il reconnaît que nous référençons les données de l'instance de Vue associée et remplace cette expression par la valeur de product, dans ce cas: «Chaussettes».
___

# Présentation de la réactivité

La raison pour laquelle Vue est capable d'afficher immédiatement la valeur de _product_ c'est parce que Vue est réactif . En d'autres termes, les données de l'instance sont liées à chaque endroit où les données sont référencées. Donc, non seulement Vue peut faire apparaître ses données dans le code HTML qui y fait référence, mais ce code HTML sera mis à jour pour afficher de nouvelles valeurs chaque fois que les données référencées seront modifiées.

Pour le prouver, ouvre ta console et change la valeur de notre chaîne de produit. Tape app.product="Ce que tu veux" et regarde ce qu'il se passe.

![Gif fast](https://media.giphy.com/media/lRnUWhmllPI9a/giphy.gif)
___

# T'as appris quoi?

* Comment commencer à écrire une application Vue avec une instance Vue et comment charger des données de base sur la page Web.
* L'instance Vue est la racine de chaque application Vue
* L'instance Vue se connecte à un élément du DOM
* Les données de l'instance Vue peuvent être affichées à l'aide de la syntaxe {{ }}, appelée expression.
* La vue est réactive

[La suite par ici](attribute.md)
