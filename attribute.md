## Liaison d'attribut

On va maintenant se pencher sur les différentes manières de connecter des données aux attributs de vos éléments HTML.

En utilisant l'attribut __v:bind__ affiche une image de chaussette verte (les images et le css ne sont pas loin).

``` html
<div class="nav-bar"></div>            

<div id="app">
  
  <div class="product">
  
    <div class="product-image">
      <img v-bind:src="image" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
    </div>
    
  </div>
    
</div> 
```

``` js
let app = new Vue({                      
  el: '#app',
  data: {
    product: 'Chaussettes',
    image:'jeSaisPasCommentTuTorganises.jpg',
  } 
})

```
Voila! Notre image apparaît. Si la valeur de image devait changer, la _src_ mise à jour correspondra et la nouvelle image apparaîtra.

Ceci est une fonctionnalité très utilisée dans Vue. Parce qu'il est si commun, il y a un raccourci pour v-bind, et c'est juste deux points "__:__"
``` html
<img :src="image"/>
```
___
## T'as appris quoi?
* Les données peuvent être liées à des attributs HTML.
* La syntaxe est __v-bind:__ ou __:__ pour faire court.
* Le nom d'attribut qui vient après le __:__ spécifie l'attribut auquel nous lions les données.
* À l'intérieur des guillemets de l'attribut, nous référençons les données auxquelles elles sont liés.
___
## Bosse un peu

Ajoute un lien vers la page de votre choix en utilisant la directive __v-bind__ . Astuce: utilisez l'attribut  __href__.

T'as réussi c'est cool.

![Gif good boy](https://media.giphy.com/media/l0HlHA1QrGxff7GtW/giphy.gif)

[La suite par ici](condition.md)