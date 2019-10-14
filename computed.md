## Les propriétés calculées (computed properties)

![gif calcul](https://media.giphy.com/media/Cpc4YnZeb11ug/giphy.gif)


Les propriétés calculées sont des propriétés  de l'instance Vue qui calculent une valeur plutôt que de stocker une valeur.

Notre premier objectif est de réussir à d’afficher la string de  __brand__ et la string de __product__.

On rajoute une propriété au data:

``` js
 brand: 'Becode'
 ```

 Nous voulons que __brand__ et __product__ soit combinés en une seule string. En d’autres termes, nous voulons afficher «Becode» dans notre  h1 «chaussettes». Comment pouvons-nous concaténer ces deux valeurs.

Puisque les propriétés calculées calculent une valeur plutôt que de stocker une valeur, ajoutons l'option __computed__  à notre instance et créons une propriété calculée appelée title.

```js
computed: {
        title() {
            return this.brand + ' ' + this.product  
        },
```
C'est assez simple. Quand title est appelé, il concaténe __brand__ et __product__ dans une nouvelle string et retourne cette même string.

Maintenant, tout ce que nous avons à faire est de le mettre __title__ dans le __h1__ de notre page.

Donc au lieu de:

``` html
<h1>{{product}}</h1>
```

``` html
<h1>{{title}}</h1>
```

Chaussettes Becode apparaît dans notre h1

Nous avons pris deux valeurs de nos data et les avons "calculées" de manière à créer une nouvelle valeur. Si nous devions à nouveau mettre __brand__ à jour, disons à «Technifutur», notre propriété calculée n'aurait pas besoin d'être refactorisée. Elle renverrait toujours la string correcte: "Technifutur Socks". Notre propriété calculée __title__ continuerait à utiliser __brand__, comme avant, mais __brand__ aurait maintenant une nouvelle valeur.

C'était un exemple assez simple mais pas tout à fait pratique, nous allons donc travailler sur une utilisation plus complexe d'une propriété calculée.

![Gif here We Go](https://media.giphy.com/media/2GjgvS5vA6y08/giphy.gif)

Pour le moment, nous mettons à jour notre image avec la méthode __updateProduct__. Nous y passons __variantImage__, puis définissons l'image sur la variante actuellement survolée.

``` js
updateProduct(variantImage){
    this.image=variantImage
}
```

Cela fonctionne bien pour le moment, mais si on veut changer plus que l'image en fonction de la variante survolée, nous devrons alors refactoriser ce code. Alors faisons cela maintenant.

Au lieu d’avoir __image__ dans nos données, remplaçons-le par __selectedVariant__ ce que nous initialiserons à 0.

```js
selectVariant:0,

```
Pourquoi l'initialiser à 0? Parce que nous allons définir cela en fonction de l'index sur lequel  nous faisons un mouseover. Nous pouvons ajouter un index à notre v-for, comme ça:

``` html
 <div class="color-box"
        v-for="(variant, index) in variants" 
        :key="variant.variantId"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(variant.variantImage)">
</div> 
```
Maintenant, au lieu de passer en argument __variantImage__, nous allons passer __index__.
```html
@mouseover="updateProduct(index)"
```
Dans notre méthode __updateProduct__, nous allons passer l'index et au lieu de mettre à jour __this.image__, nous mettrons à jour __this.selectedVariant__ avec l'index de la variante actuellement survolée. Et on fait un petit console.log des familles pour nous assurer que tout fonctionne bien.

``` js
  updateProduct: function(index) {  
            this.selectedVariant = index
        }
```

Maintenant, lorsque nous actualisons et ouvrons la console, nous pouvons voir que cela fonctionne. Nous enregistrons 0 et 1 alors que nous survolons l'une ou l'autre variante.

Mais remarquez un warning dans la console parce que nous avons supprimé __image__ et l'avons remplacé par __selectedVariant__. On doit transformer __image__ en une propriété calculée:

``` js
image(){
return this.variants[this.selectedVariant].variantImage
        },
```
![Gif sorcery](https://media.giphy.com/media/a2euXnuLIgVQA/giphy.gif)

On retourne __this.variants__, qui est notre tableau de variantes, et nous utilisons notre __selectedVariant__, 0 ou 1, pour cibler le premier ou le deuxième élément de ce tableau, puis nous utilisons la notation pointée pour cibler son image.

Lorsque nous actualisons, notre image bascule correctement comme avant, mais nous utilisons maintenant une propriété calculée pour gérer cela à la place.

Maintenant que nous avons refactorisé la méthode __updateProduct__ pour mettre à jour du __selectedVariant__, nous pouvons accéder à d’autres data de variants, telles que __variantQuantity__:

``` js
variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: 'jeSaisPasCommentTuTorganises.jpg',
            variantQuantity: 10     
          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: 'jeSaisPasCommentTuTorganises.jpg',
            variantQuantity: 0     
          }
        ],
```
Comme nous l'avons fait avec __image__, supprimons __inStock__ de nos data et transformons-les en une propriété calculée qui utilise les quantités de notre variante.
```js
 inStock(){
return this.variants[this.selectedVariant].variantQuantity
        },
```
Ceci est très semblable à notre propriété calculée __image__, nous visons simplement le __variantQuantity__ plutôt que le __variantImage__.

Maintenant, lorsque nous faisons un hover sur la variante bleue, qui a une quantité null, inStock sera évaluée  false et nous Rupture de stock s'affichera.
___

## T'as appris quoi?
* Les propriétés calculées calculent une valeur plutôt que de stocker une valeur.
* Les propriétés calculées peuvent utiliser les données de votre application pour calculer ses valeurs.
___

## Qu'est-ce que tu dois savoir d'autre:

Les propriétés calculées sont mises en cache, ce qui signifie que le résultat est enregistré jusqu'à ce que ses dépendances changent. Ainsi, lorsque des quantitymodifications seront apportées, le cache sera effacé et ** la prochaine fois que vous accéderez à la valeur de inStock, il renverra un nouveau résultat et le mettra en cache.

Dans cet esprit, il est plus efficace d'utiliser une propriété calculée plutôt qu'une méthode pour une opération coûteuse que vous ne souhaitez pas réexécuter à chaque fois que vous y accédez.

Il est également important de garder à l'esprit que vous ne devez pas transformer votre modèle de données à partir d'une propriété calculée. Vous calculez simplement des valeurs basées sur d'autres valeurs. Gardez ces fonctions pures.
___
[Un peu de courage c'est bientôt fini](component.md)

![Gif courage](https://media.giphy.com/media/b346HapBsg7oQ/giphy.gif)

