## Premier pas avec Vue.js:

![Gif firststep](https://media.giphy.com/media/2D4tYGhHKFYre/giphy.gif)

Pour commencer, tu crées un fichier index.html, ensuite rends-toi sur le site [__Vue.js__](https://fr.vuejs.org/), tu appuies sur le bouton commencer et tu récupères ce lien :

```
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

et tu le mets dans ton fichier index.html. 
Si tu préfères, tu peux aussi _blablabla_   CDN   _blablabla_ . Tu connais la marche à suivre quoi.
___
## Rendu déclaratif

Au cœur de Vue.js, il y a un système qui va nous permettre de faire le rendu des données déclarativement dans le DOM en utilisant simplement cette syntaxe de template :

``` html
<div id="app">                        HTML
  {{ message }}
</div>
```

Tu crées un fichier main.js est tu taps ça dedans:
``` js
let app = new Vue({                                                                           JS
  el: '#app',
  data: {
    message: 'Hello Vue !'
  }
})
```
![Gif magie](https://media.giphy.com/media/NmerZ36iBkmKk/giphy.gif)
```
Hello Vue!
```

Nous venons tout juste de créer notre première application Vue ! Ça ressemble à un simple rendu de template en chaine de caractères, mais sous le capot, Vue effectue un réel travail. Les données et le DOM sont maintenant couplés, et tout est à présent réactif. Comment s’en rendre compte ? Ouvrez juste la console JavaScript de votre navigateur (là maintenant, sur cette page) et attribuez à app.message différentes valeurs. Vous devriez voir le rendu de l’exemple en cours se mettre à jour en concordance.

En plus de l’interpolation de texte, nous pouvons également lier les attributs d’un élément comme ceci :

``` html
<div id="app-2">                                                                            HTML
  <span v-bind:title="message">
    Passez votre souris sur moi pendant quelques secondes
    pour voir mon titre lié dynamiquement !
  </span>
</div>
```
``` js
let app2 = new Vue({                                                                         JS
  el: '#app-2',
  data: {
    message: 'Vous avez affiché cette page le ' + new Date().toLocaleString()
  }
})
```
Ici nous venons de rencontrer quelque chose de nouveau. L’attribut v-bind que vous voyez est appelé une directive. Les directives sont préfixées par v- pour indiquer que ce sont des attributs spéciaux fournis par Vue, et comme vous l’avez peut-être deviné, elles appliquent un comportement réactif spécifique au DOM après rendu. Ici cela veut basiquement dire : « garde l’attribut title de cet élément à jour avec la propriété message de l’instance de Vue ».

Si vous ouvrez votre console JavaScript une nouvelle fois et entrez app2.message = 'un nouveau message', de nouveau vous verrez le HTML lié — dans notre cas l’attribut title — se mettre à jour.
___
## Conditions et boucles

``` html
<div id="app-3">                                                                            HTML
  <p v-if="seen">Maintenant vous me voyez</p>
</div>
```

``` js
let app3 = new Vue({                                                                         JS 
  el: '#app-3',
  data: {
    seen: true
  }
})
```
Côté console entrez __app3.seen = false__. Vous devriez voir le message disparaitre.

Cet exemple démontre que nous pouvons lier des données non seulement aux textes et attributs, mais également à la structure du DOM. De plus, Vue fournit un puissant système d’effets de transition qui peut automatiquement appliquer des effets de transition quand des éléments sont insérés/mis à jour/enlevés par Vue.

Il existe quelques autres directives, chacune avec leur propre fonction spécifique. Par exemple,la directive v-for peut être utilisée pour afficher une liste d’éléments en provenance d’un tableau de données.

``` html
<div id="app-4">                                                                            HTML
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```

``` js
let app4 = new Vue({                                                                          JS
  el: '#app-4',
  data: {
    todos: [
      { text: 'Apprendre JavaScript' },
      { text: 'Apprendre Vue' },
      { text: 'Créer quelque chose de génial' }
    ]
  }
})
```
Dans la console, entrez __app4.todos.push({ text: 'Nouvel élément' })__. Vous devriez le voir ajouté à la liste.
___
## Gestion des entrées utilisateurs

Afin de permettre aux utilisateurs d’interagir avec votre application, nous pouvons utiliser la directive v-on pour attacher des écouteurs d’évènements qui invoquent des méthodes sur nos instances de Vue :

``` html
<div id="app-5">                                                                            HTML
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Message retourné</button>
</div>
```

``` js
var app5 = new Vue({                                                                          JS
  el: '#app-5',
  data: {
    message: 'Hello Vue.js !'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
Notez que dans la méthode, nous avons seulement mis à jour l’état de l’application sans toucher au DOM. Toutes les manipulations de DOM sont prises en charge par Vue, ainsi le code que vous écrivez se concentre sur la logique sous-jacente.

Vue fournit aussi la directive __v-model__ qui fait de la liaison de données bidirectionnelle entre les champs d’un formulaire et l’état de l’application. Une simple formalité :

``` html
<div id="app-6">                                                                            HTML
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```

``` js
var app6 = new Vue({                                                                          JS
  el: '#app-6',
  data: {
    message: 'Hello Vue !'
  }
})
```
___
## Composer avec des composants

Le système de composant est un autre concept important de Vue, car c’est une abstraction qui nous permet de construire de plus grosses applications composées de plus petits composants réutilisables et autonomes. Quand on y pense, presque tous les types d’interfaces applicatives peuvent être abstraits en un arbre de composants.

Dans Vue, un composant est essentiellement une instance de Vue avec des options prédéfinies. Déclarer un composant avec Vue est très simple :

``` js
// Définit un nouveau composant appelé todo-item                                              JS
Vue.component('todo-item', {
  template: '<li>Ceci est une liste</li>'
})
```
Maintenant nous pouvons l’insérer dans le template d’un autre composant :

``` html
<ol>
  <!-- Crée une instance du composant todo-list -->                                         HTML
  <todo-item></todo-item>
</ol>
```

Mais cela donnerait comme rendu le même texte, ce qui n’est pas vraiment intéressant. Nous devrions être capables de passer les données de la portée parente dans le composant enfant. Modifions la définition du composant pour lui permettre d’accepter une __prop__ :

``` js
Vue.component('todo-item', {                                                               JS 
  // Le composant todo-item accepte maintenant une
  // « prop » qui est comme un attribut personnalisé.
  // Cette prop est appelée todo.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```
Maintenant nous pouvons passer la liste dans chaque composant répété en utilisant __v-bind__ :

``` html
<div id="app-7">                                                                            HTML
  <ol>
    <!--
      Maintenant nous fournissons à chaque todo-item l'objet todo
      qu'il représente de manière à ce que son contenu puisse être dynamique.
      Nous avons également besoin de fournir à chaque composant une « clé »,
      mais nous expliquerons cela plus tard.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```

``` js
Vue.component('todo-item', {                                                                  JS
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Légumes' },
      { id: 1, text: 'Fromage' },
      { id: 2, text: 'Tout ce que les humains sont supposés manger' }
    ]
  }
})
```

Ceci n’est qu’un exemple grossier, nous avons réussi à séparer notre application en deux plus petites unités, et chaque enfant est raisonnablement bien découplé de son parent via l’utilisation des props. Nous pouvons maintenant améliorer notre __todo-item__ avec un template et une logique plus complexes sans affecter l’application parente.

Pour une grosse application, il est nécessaire de la diviser entièrement en composants afin de rendre le développement plus abordable. Nous parlerons des composants plus précisément plus tard dans le guide, mais en attendant voici un exemple (imaginaire) de ce à quoi un template d’application pourrait ressembler avec des composants :

``` html
<div id="app">                                                                             HTML
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```
Nous venons juste d’introduire brièvement les fonctionnalités les plus basiques du cœur de Vue.js. Nous allons maintenant coder notre première application, une page pour un produit.

Si vous êtes prêts:
[Allez on se lance](begining.md)

Sinon:
[Carrière alternative](https://mcdonalds.be/fr/emploi/mcjob)