``` js                                  JS
 removeFromCart() {
      this.cart -= 1
    }
```
``` html                               HTML
 <button @click="removeFromCart">Remove from cart</button>
```

## Binding, lier le style et les classes

Maintenant, on va apprendre à styler dynamiquement notre code HTML en liant des données à l'attribut style d'un élément et sa classe.

Notre premier objectif est d’utiliser nos variantes de couleurs pour styliser les background-color des _divs_. Puisque nos variantes de couleurs sont “vert” et “bleu”, on veut un div avec un background-color vert  et un div avec un background-color bleu.

On va commencer par ajouter une classe de "color-box" à notre div (cette classe est déjà définie dans notre fichier CSS). Puisque nous affichons toujours les mots «vert» et «bleu» sur la page, nous pouvons utiliser ces strings de couleurs différentes et les lier à notre attribut style, comme suit:

``` html
<div class="color-box"
    v-for="variant in variants" 
    :key="variant.variantId"
    :style="{ backgroundColor: variant.variantColor }">
    <p>@mouseover="updateProduct(variant.variantImage)"</p>
</div> 
```
Nous utilisons un style en ligne pour définir dynamiquement le background-colorde nos divs, en fonction de nos variantes de couleurs ( variant.variantColor).

Maintenant que nos _divs_ sont stylés par le __variantColor__, nous n’avons plus besoin de les AFFICHER. Ainsi, nous pouvons supprimer la balise _p_ et la déplacer __@mouseover__ dans la div même.

``` HTML
 <div class="color-box"
    v-for="variant in variants" 
    :key="variant.variantId"
    :style="{ backgroundColor: variant.variantColor }"
    @mouseover="updateProduct(variant.variantImage)">
</div> 
```
Maintenant, lorsque nous survolons la box bleue et que les chaussettes bleues apparaissent, survolez la boîte verte et les chaussettes vertes apparaissent. C'est pas cool, ça!
Maintenant que nous avons appris à faire la liaison de style, explorons la liaison de classe.

Pour le moment, on a cette propriété dans nos data:

``` js
inStock:true,
```
Lorsque cette valeur booléenne est __false__, on ne devrait pas autoriser les utilisateurs à cliquer sur le bouton “Ajouter au panier”, car il n'y a aucun produit en stock à ajouter au panier. Heureusement, il existe un attribut HTML intégré __disabled__, qui désactivera le bouton.

Comme nous l' avons vu, nous pouvons utiliser l' attribut de liaison pour ajouter l'attribut __disabled__ à chaque fois __inStock__ est __false__, ou plutôt pas __true__ : __!inStock__.

``` html
 <button v-on:click="addToCart" 
    :disabled="!inStock">Add to cart
</button>
```
Maintenant , notre bouton est désactivé chaque fois __inStock__ est évalué comme __false__. Mais cela ne change pas l'apparence du bouton. En d'autres termes, le bouton semble toujours cliquable, même s'il ne l'est pas.

De la même manière que nous venons de nous lier __inStock__ à l'attribut __disabled__ du bouton , nous pouvons lier une classe __disabledButton__ à notre bouton chaque fois que __inStock__ est false. De cette façon, notre bouton est désactivé.

``` html
 <button v-on:click="addToCart" 
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }">
        Add to cart
</button>
```
Ça marche! Le bouton est maintenant grisé quand __inStock = false__.

Si on décompose

``` html
:class="{ disabledButton: !inStock }"
```

Nous utilisons le raccourci de la directive v-bind __:__ pour créer un lien avec la classe __disabled-button__ de notre bouton. Entre parenthèses, nous déterminons la présence de la classe par l'évaluation de la propriété __inStock__ de data.

En d'autres termes, lorsque notre produit n'est pas en stock ( !inStock), la classe __disabledButton__ est ajoutée. Comme la  classe __disabled-button__ applique un background-color gris, le bouton devient gris.

Génial! Nous avons combiné notre nouvelle liaison de classe de compétences avec la liaison d'attributs pour désactiver notre bouton et l'activer en gris lorsque notre produit inStock est false.
___

## T'as appris quoi,
* Les données peuvent être liées à un attribut style.
* Les données peuvent être liées à un élément class.
* Nous pouvons utiliser des expressions à l'intérieur de la liaison de classe d'un élément pour déterminer si une classe doit apparaître ou non.
___
## Qu'est-ce que tu dois savoir d'autre:

``` html
<div :class="classObject"></div>
<div :class="[activeClass,errorClass]"></div>
```
___
## Bosse un peu
Lorsque la valeur inStock est false, liez une classe à la balise _p_ «Rupture de stock» qui ajoute text-decoration: line-through à cet élément.

![Gif working](https://media.giphy.com/media/JIX9t2j0ZTN9S/giphy.gif)

[Il y en a encore](computed.md)