## Les composants

Nous allons maintenant découvrir le monde merveilleux des composants. Les composants sont des blocs de code réutilisables pouvant avoir à la fois une structure et des fonctionnalités. Ils aident à créer une base de code plus modulable et maintenable.

Nous allons créer notre premier composant, puis apprendre à partager des données avec celui-ci.

Dans une application, nous ne voulons pas que toutes nos données, méthodes, propriétés calculées soient à la racine de l'instance. Sur le long terme, cela deviendrait ingérable. Au lieu de cela, nous voudrons diviser notre code en éléments modulaires de manière à ce qu'il soit plus facile à travailler.

Nous allons commencer par prendre une partie de notre code actuel et l'intégrer dans un nouveau composant de notre produit.

Nous créons le composant comme ceci:

```js
Vue.component('product',{})
```

Le premier argument est le nom que nous avons choisi pour le composant et le second est un objet optionnel, similaire à celui de notre instance Vue initiale.

Dans l'instance Vue, nous avons utilisé la propriété __el__ pour se connecter à un élément du DOM. Pour un composant, nous utilisons la propriété __template__ pour ajouter son code HTML.

Dans cet objet options, nous ajouterons notre modèle.

``` js
Vue.component('product',{
    template:
    <div class="product">
            // Le code HTML de  product vient ici
    </div>
})
```

Il existe plusieurs façons de créer un modèle dans Vue, mais pour l'instant, nous utiliserons un template littéral, avec des back ticks.

Si tout notre code de modèle n'était pas imbriqué dans la  div avec la classe de «product», nous aurions eu cette erreur:

Component template should contain exactly one root element

En d'autres termes, le template d'un component ne peut retourner qu'un seul élément.

Donc ceci fonctionne:
```js
Vue.component('product',{
    template:
    <h1>Je suis un élément unique</h1>
})
```

Et ceci non, car ce sont deux éléments frères:
```js
Vue.component('product',{
    template:
    <h1>Je suis un élément unique</h1>
    <h2>Plus rien ne passe</h2>
})
```

Ainsi, si nous avons plusieurs éléments frères, comme dans notre modèle __product__, ils doivent être enveloppés dans un élément conteneur externe afin que le modèle ait exactement un élément à la racine.

Maintenant nous allons transférer tout notre code html dans notre template. Il ne nous reste plus qu'a ajouter nos données, méthodes et propriétés calculées à partir de l'instance racine dans notre nouveau composant.

Maintenant que notre template est complet avec notre __product__ HTML, nous allons ajouter nos données, méthodes et propriétés calculées à la racine de l'instance dans notre nouveau composant.

```js
Vue.component('product',{
    template:`
    <div class="product">
        ...
    </div>
    `,
    data(){
        return{
            //les data viennent ici
        }
    },
    methods:{
        //les méthodes viennent ici
    },
    computed:{
        //les propriétés calculées viennent ici
    }
})
```

La structure de ce composant est presque identique à celle de notre instance d'origine. Comme t'es fort tu as remarqué que  data est maintenant devenu une fonction? Mais pourquoi ce changement?

Parce que nous voulons réutiliser les composants souvents. Et si nous avions plusieurs composants __product__, nous devons nous assurer de créer une  instance distincte de nos data pour chaque composant. Puisque data est maintenant une fonction qui retourne un objet de données, chaque composant aura ses propres données. Si data ne s'était pas une fonction, chaque composant __product__ partagerait les mêmes data partout où il était utilisé, ce qui irait à l'encontre du but d'être un composant réutilisable.

Maintenant que nous avons déplacé notre code lié au produit dans son propre composant __product__, notre instance ressemble à ceci:

``` js
var app=new vue({
    el:'#app'
})
```
Il ne nous reste plus qu'a insérer notre composant __product__ dans notre fichier index.html.

``` html
<div id="app">
    <product></product>
</div>
```
Notre __product__ s'affiche à nouveau.

Juste pour démontrer la puissance des composants, ajoutons deux composants __product__ supplémentaires , pour voir à quel point il est facile de réutiliser un composant.

``` html
<div id="app">
    <product></product>
    <product></product>
    <product></product>
</div>
```

![Gif multi-clonage](assets/img/clone.gif)

Souvent, dans une application, un composant doit recevoir des données de son parent. Dans ce cas, le parent de notre composant __product__ est l'instance racine elle-même.

Supposons que notre instance racine contienne des données d'utilisateur, spécifiant si l'utilisateur est titulaire d'un compte premium. Si tel est le cas, notre instance ressemble maintenant à ceci:
``` js
let app=new Vue({
    el:'#app',
    data:{
        premium:true
    }
})
```
Si un de nos utilisateur est un membre Premium, toutes ses expéditions sont gratuites.

Cela signifie que nous aurons besoin que notre composant __product__  affiche différentes valeurs pour l'expédition en fonction de la valeur de premium de notre instance racine.

Alors, comment pouvons-nous envoyer __premium__ de l'instance racine, dans son enfant, le composant __product__?

Dans Vue, nous utilisons des __props__ pour gérer ce type de partage de données. Les __props__ sont essentiellement des variables qui attendent d'être renseignées avec les données que leur parent leur envoie.

Nous commencerons par spécifier les __props__ que le composant __product__ s'attend à recevoir en ajoutant un objet props à notre composant.

``` js
Vue.component('product', {
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  // Les data, méthodes, propriétés calculées viennent ici en-dessous
    
  ```

Ensuite, dans notre template, on va créer  un élément qui nous permet d'afficher notre props afin de nous assurer qu'il soit correctement transmis.

``` js
 <p>User is premium: {{ premium }}</p>
```

Notre component __product__ sait qu'il varecevoir une valeur boléenne obligatoire et qu'il dispose d'un emplacement pour afficher ces données.

Maintenant, il nous reste à passer la valeur __premium__dans notre component __product__ . On fait ça à l'aide d'un attribut personnalisable qui nous permet de passer __premium__ dans notre composant.

``` html
<div id="app">
  <product :premium="premium"></product>
</div> 
```

![gif big bang](https://media.giphy.com/media/3osxYACfOYULLSpNjG/giphy.gif)

Alors qu'est-ce qu'on a fait?

On a passé à notre composant __product__ un props, ou un attribut personnalisé , appelé __premium__. Nous lions cet attribut personnalisé __:__ à celui premium qui se trouve dans les data de notre instance.

Maintenant que notre instance racine passe correctement  premium dans son composant enfant __product__ . Maintenant que l'attribut  __premium__ est bien lié aux data de notre instance racine, la valeur actuelle de premium dans les data de notre instance sera toujours envoyée à __product__.

Si nous avons correctement réglé le problème, nous devrions voir: «User is premium: true».

Maintenant que nous passons des data dans notre composant, utilisons-les pour modifier ce que nous affichons pour l'expédition. Rappelez-vous que si premium est true, cela signifie que la livraison est gratuite. Utilisons donc notre __props__ premium dans une propriété calculée appelée shipping.

``` js
 shipping() {
    if (this.premium) {
        return "Free"
    }else{
        return 2.99
    }
}   
```
Maintenant, nous utilisons notre prop ( this.premium), tant que ce sera évalué true, shipping renverra «Free». Sinon, ça retournera 2,99.

Au lieu de dire User is premium: {{ premium }}, utilisons cet élément pour afficher nos coûts d'expédition, en appelant notre propriété calculée  __shipping__ comme ceci:
```
<p>Shipping: {{ shipping }}</p>
```
Et maintenant on voit «Shipping: Free». Pourquoi? Parce que __premium__ est évalué __true__,  et donc shipping retourne «Free».

Nous avons donc passé les data de notre parent à son composant enfant et nous les avons utilisées dans une propriété calculée qui affiche différentes valeurs d’expédition en fonction de la valeur de notre props.

## T'as appris quoi?

* Les composants sont des blocs de code, regroupés dans un élément personnalisé.
* Les composants rendent les applications plus faciles à gérer en divisant le tout en parties récupérables ayant leur propre structure et leur propre comportement.
* Les données dans un composant doivent être une fonction.
* Les props sont utilisés pour transmettre des données du parent à l'enfant.
* Nous pouvons spécifier les exigences (required) que les props qu'un composant reçoit.
* Les props sont introduits dans un composant via un attribut personnalisé.
* Les props peuvent être liés dynamiquement aux données du parent.

## Bosse un peu :
Crée un nouveau component __product-details__ avec un props __details__.

![gif applause](https://media.giphy.com/media/dZo51w9gv37QQ/giphy.gif)

