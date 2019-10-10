## Liaison d'attribut

On va maintenant se pencher sur les différentes manières de connecter des données aux attributs de vos éléments HTML.

En utilisant l'attribut _v:bind_ affiche une image de chaussette verte (les images et le css sont pas loin).

``` html
<div class="nav-bar"></div>            HTML

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
let app = new Vue({                      JS
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
* La syntaxe est v-bind:ou :pour faire court.
* Le nom d'attribut qui vient après le :spécifie l'attribut auquel nous lions les données.
* À l'intérieur des guillemets de l'attribut, nous référençons les données auxquelles nous sommes liés.
___
## Bosse un peu

Ajoutez un lien vers votre objet de données et utilisez-le v-bind pour le synchroniser avec une balise d'ancrage dans votre code HTML. Astuce: vous allez être lié à l' href attribut.

T'as réussi c'est cool

![Gif good boy](https://media.giphy.com/media/l0HlHA1QrGxff7GtW/giphy.gif)

[La suite par ici](condition.md)