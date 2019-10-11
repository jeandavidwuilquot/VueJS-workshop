
``` html                            HTML
 <ul>
    <li v-for="size in sizes">{{ size }}</li>
</ul>
```
``` js                              JS
 sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL']
```
___

## La gestion des événements

Dans cette leçon, nous allons apprendre à écouter les événements DOM que nous pouvons utiliser pour déclencher des méthodes.
On va mettre un bouton qui incrémente le nombre d'articles dans notre panier.

On va ajouter un bouton pour écouter les événements "clic", puis déclencher une méthode lorsque ce clic se produit, afin d'incrémenter le total dans un panier.

On commence par ajouter une nouvelle propriété __cart__ à data pour notre panier.

```js                                   JS
cart:0
```
Dans notre HTML, on crée une div pour notre panier. Nous y ajouterons un élément _p_ pour afficher __cart__ la valeur de nos données.

``` html
<div class="cart">
    <p>Cart({{ cart }})</p>
</div>
```

On ajoute également un buttonpour ajouter des éléments à notre __cart__.
``` html
<button v-on:click="cart +=1">Add to cart</button>
```
Ca fonctionne bien mais ce serait vraiment mieux avec une méthode

``` html
 <button v-on:click="addToCart">Add to cart</button>

```
Comme vous pouvez le constater, addToCar test le nom d’une méthode qui se déclenche lorsque cet événement se produit. Nous n'avons pas encore défini cette méthode, alors faisons-le maintenant, directement sur notre instance.

Comme pour les __data__, l’instance Vue a une propriété facultative pour les méthodes. Nous allons donc écrire notre  méthode __addToCart__ dans cette option.

``` js
methods: {
    addToCart() {
      this.cart += 1
    },
```

Maintenant, lorsque nous cliquons sur notre bouton, notre méthode __addToCart__ est déclenchée, ce qui incrémente la valeur de _cart_, qui est affichée dans notre balise _p_.

Décomposons cela plus loin.

Notre  bouton écoute les événements _clic_ avec la directive _v-on_, ce qui déclenche la méthode __addToCart__. Cette méthode réside dans la propriété _methods_ de l'instance Vue en tant que fonction anonyme. Le corps de cette fonction ajoute 1 à la valeur de __this.cart__. Parce que _this_ fait référence aux données de l'instance dans laquelle nous sommes actuellement, notre fonction ajoute 1 à la valeur de _cart_, car __this.cart__ c'est la propriété _cart_de nos data.

Maintenant que nous avons appris les bases de la gestion des événements dans Vue, examinons un autre exemple.

Premièrement, ajoutons __variantImage__ à chacune de nos variantes.

``` js
 variants: [
      {
        variantId: 2234,
        variantColor: 'green',
        variantImage: 'jeSaisPasCommentTuTorganises.jpg'
      },
      {
        variantId: 2235,
        variantColor: 'blue',
        variantImage: 'jeSaisPasCommentTuTorganises.jpg'
      }
    ],
```

Maintenant, chaque variante a respectivement une image avec des chaussettes vertes et bleues.

Nous voulons être en mesure de survoler la couleur d'une variante avec notre souris et de l' variantImage afficher à l'emplacement actuel de l'image de notre produit.

Nous voulons être en mesure d'afficher la couleur d'une variante en survolant son nom avec la souris.

On va de nouveau utiliserla directive __v-on__, mais cette fois-ci, on va utiliser son raccourci __@__ pour écouter  l'événement mouseover.

``` html
 <div v-for="variant in variants"               :key="variant.variantId">
  <p @mouseover="updateProduct   (variant.variantImage)">{{ variant.variantColor }}</p>
</div>
```

Tu as remarqué qu'on passe __variant.variantImage__ en argument à notre méthode __updateProduct__.

On va écrire cette méthode:
``` js
updateProduct(variantImage) {
      this.image = variantImage
    },
```
Ceci est très similaire à ce que nous avons fait pour augmenter la valeur de _cart_ plus tôt.

Mais ici, nous mettons à jour la valeur de image, et sa valeur mise à jour est maintenant celle de  __variantImage__ la variante sur laquelle nous faisons un mouseover. Nous avons passé l'image de cette variante dans la  méthode __updateProduct__ à partir du gestionnaire d'événements lui-même:

``` html
<p @mouseover="updateProduct(variant.variantImage)"></p>
```
___
## Syntaxe ES6

Au lieu d'écrire une fonction anonyme comme __updateProduct: function(variantImage)__, nous pouvons utiliser le raccourci ES6 et simplement écrire __updateProduct(variantImage)__. Ce sont des manières équivalentes de dire la même chose.
___

## T'as appris quoi?
* La v-on directive est utilisée pour permettre aux éléments d'écouter les événements
* Le raccourci pour v-on est __@__
* Vous pouvez spécifier le type d'événement à écouter:
  * Cliquez sur
passer la souris
tout autre événement DOM
  * La directive v-onpeut déclencher une méthode
  * Les méthodes déclenchées peuvent prendre des arguments
* __this__ fait référence aux données de l'instance Vue actuelle ainsi qu'à d'autres méthodes déclarées à l'intérieur de l'instance

## Bosse un peu:
Crées un nouveau bouton et une nouvelle méthode pour décrémenter la valeur de __cart__.

[Il y en a encore](binding.md)