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

Maintenant que notre modèle est complet avec notre produit HTML, nous allons ajouter nos données, méthodes et propriétés calculées à partir de l'instance racine dans notre nouveau composant.

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
        //les propriétés viennent ici
    }
})
```

La structure de ce composant est presque identique à celle de notre instance d'origine. Comme t'es fort tu as remarqué que  data est maintenant devenu une fonction? Mais ourquoi ce changement?