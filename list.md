## Rendu de liste

Nous allons apprendre à afficher des listes sur nos pages Web avec Vue.

Nous voulons pouvoir afficher une liste des cataréstiques de nos produits.
* 80% polyester
* 20% coton
* Unisexe

Rajoute ce tableau au data:

``` js                                  JS
details:["80% polyester","20% coton","Unisexe"]
```

Pour parcourir le tableau et restituer les données, tu dois utiliser la directive _v-for_

``` html                               HTML
<ul>
    <li v-for="detail in details">{{detail}}</li>
</ul>
```
___

# Itération sur les objets

La page de produit que nous construisons doit pouvoir afficher différentes versions du même produit, basées sur un tableau dans nos data variants. Comment pourrions-nous parcourir ce tableau d'objets pour afficher ses données?

``` js
 variants: [
      {
        variantId: 2234,
        variantColor: 'green'    
      },
      {
        variantId: 2235,
        variantColor: 'blue'
      }
    ],
```

Pour afficher la couleur de chaque variante:

``` html
 <div v-for="variant in variants">
        <p>{{ variant.variantColor }}</p>
 </div>
```
Notez qu'il est recommandé d'utiliser un attribut __key__ lors du rendu de tels éléments afin que Vue puisse garder une trace de l'id de chaque nœud. Nous allons ajouter cela maintenant, en utilisant la variantIdpropriété unique de notre variante .

``` html
 <div v-for="variant in variants" :             key="variant.variantId">
        <p>{{ variant.variantColor }}</p>
</div>
```
## T'as appris quoi?

* La __v-for__ directive nous permet d'itérer sur un tableau pour afficher des données.
* Nous utilisons un __alias__ pour l'élément du tableau sur lequel nous effectuons une itération et spécifions le nom du tableau que nous sommes en train de boucler. Ex:v-for="__item__ in items"
Nous pouvons effectuer une boucle sur un tableau d'objets et utiliser la notation par points pour afficher les valeurs des objets.
Lors de l'utilisation, __v-for__ il est recommandé d'attribuer à chaque élément rendu une clé unique __key__.
___
## Bosse un peu:

Ajouter un tableau de tailles données et utilise _v-for_ pour les afficher dans une liste.

![gif easy](https://media.giphy.com/media/zcCGBRQshGdt6/giphy.gif)

[La suite par ici](event.md)