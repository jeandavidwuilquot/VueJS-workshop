Si t'es toujours avec nous ton code devrait ressembler à ça:

``` html
<div class="nav-bar"></div>            HTML

<div id="app">
  
  <div class="product">
  
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <a :href="link" target="_blank">Plus de produits dans le même genre</a>
    </div>
    
  </div>
    
</div> 
```

``` js
let app = new Vue({                     JS
  el: '#app',
  data: {
    product: 'Chaussettes',
    image:'jeSaisPasCommentTuTorganises.jpg',
    link:'https://www.amazon.fr/s?k=sex+toys&__mk_fr_FR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss_2',
  } 
})
```
___
## Le rendu conditionnel

Maintenant, nous allons voir comment afficher conditionnellement des éléments avec Vue.

VNous voulons afficher un texte indiquant si notre produit est en stock ou non, en fonction de nos données.

Commence par ajouter une nouvelle propriété "inStock" à tes datas.

``` js
data: {
    product: 'Chaussettes',
    image:'jeSaisPasCommentTuTorganises.jpg',
    link:'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
    inStock:true,
  } 
```
Étant donné que nos data contiennent la nouvelle propriété: inStock

On peut utiliser les directives _v-if_ et _v-else_ pour déterminer quel élément rendre.

```
<p v-if="inStock">Article en stock</p>
<p v-else>Article épuisé</p>
```
Selon la valeur de inStock le rendu sera différent.

On peut ajouter un troisième degré de logique avec _v-else-if_. Pour illustrer notre propos, on check ça dans un nouvel exemple.

Tu peux rajouter ça à tes data:
``` js
inventory:100
```

``` html
<p v-if="inventory > 10">Article en stock</p>
<p v-else-if="inventory <=10 && inventory >0">Article bientôt épuisé</p>
<p v-else>Article épuisé</p>
```
L'élément qui sera rendu est le premier élément dont l'expression est évaluée à true.
___

## Syntaxe conditionnelle suppléméntaire: __v-show__

Si votre application nécessite un élément pour basculer fréquemment sur la page, vous souhaiterez utiliser la v-showdirective. Un élément portant cette directive sera toujours présent dans notre DOM, mais il ne sera visible sur la page que si sa condition est remplie. Cela ajoutera ou supprimera conditionnellement la propriété CSS display: noneà l'élément.

Cette méthode est plus performante que l'insertion et la suppression répétées d'un élément avec _v-if/ v-else_.

``` html
<p v-show="inStock">En stock</p>
```
___

## T'as appris quoi?

* Il y a des directives Vue pour rendre conditionnellement les éléments:
  * v-si
  * v-else-if
  * v-else
  * v-show

* Si ce qui est à l'intérieur des guillemets de la directive est __true__, l'élément      s'affichera.
* Vous pouvez utiliser des expressions à l'intérieur des guillemets de la directive.
* V-show ne fait que basculer la visibilité, il n’insère ni ne supprime l’élément du DOM.

[La suite par ici](list.md)