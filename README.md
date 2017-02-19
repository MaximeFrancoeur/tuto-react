# Note sur React


De quoi est composée une classe React ?
* Le state est défini à l’initialisation de la classe par la méthode getInitialState() et l’on peut le mettre à jour par la méthode setState.
* Les props sont passées à l’initialisation et sont définies en dehors de la classe.
* La méthode render() retourne un objet représentant une partie du DOM virtuel.

2 facons de faire des component la premier qui extend Component et la seconde qui son des Component stateless.

La syntaxe " nomFonction = () => {} " nous permet de conserver le contexte `this` du scope courant.


```javascript
Cycle de vie d'un Component :
|__constructor()
|
|__componentWillMount()
|
|__render()
|
|__componentDidMount()
|
|__componentWillUnmount()
```

* Avec componentWillMount, vous pourrez réaliser des opérations avant que votre component ne soit rendu. Vous pouvez par exemple initialiser le state (car toute modification du state dans cette fonction n’implique pas le rechargement du component). Cependant React conseille de réaliser cette opération dans le constructeur, comme nous l’avons fait depuis le début.
* componentDidMount est quant à elle, appelée après le rendu du component. C’est ici que nous réaliserons les futurs appels API.
* Et componentWillUnmount est appelée quand votre component est “démonté”.

```javascript
A chaque changement du State :
|
|__componentWillReceiveProps(nextProps)
|
|__shouldComponentUpdate(nextProps, nextState)
|
|__componentWillUpdate(nextProps, nextState)
|
|__render
|
|__componentDidUpdate(prevProps, prevState)
```

* componentWillReceiveProps(nextProps) est appelée lorsqu’un component, qui est déjà initialisé, reçoit de nouvelles props. Dans cette fonction, on peut comparer les nouvelles props (ici contenues dans l’objet nextProps), avec les anciennes (this.props).

* La fonction shouldComponentUpdate(nextProps, nextState) est appelée à chaque changement du state. On utilise cette fonction afin de faire savoir à React si, oui ou non, le component est affecté par le changement en retournant true ou false. Si l’on retourne false, les méthodes componentWillUpdate(), render(), et componentDidUpdate() ne seront pas appelées.

* componentWillUpdate(nextProps, nextState) est appelée par React juste avant que les nouvelles props et le nouveau state ne soit rendues.

* La fonction componentDidUpdate(prevProps, prevState) est, quant à elle, exécutée après le rendu du nouveau state / des nouvelles props. On utilisera cette fonction pour réaliser des actions sur le DOM ou des appelles d’ API.

Toutes ces fonctions ne sont pas appelées à l’initialisation du component.



## React-Redux


![React-Redux Diagram](https://github.com/MaximeFrancoeur/tuto-react/blob/master/react-redux.png)


Explication sur React plus bas dans cet article : https://anybox.fr/blog/appli-web-histoire-du-dom-react-redux

Action Type : Type d’action qui peuvent être lancer dans l’application
Action : Objet avec une méthode par action qui retourne un objet avec le type d'action + data {} qui est le data qu’on devras faire un traitement comme le modifier.

Container : Le container a pour but de faire le lien entre le state géré par Redux et les props du component. Il définit également des fonctions qui dispatchent des actions afin de mettre à jour le state. Le container connect l’architecture Redux avec le component. 

Reducer (State + Action → nouveau State) : Le Réducteur est donc une fonction souvent simplissime qui consiste à prendre une Action et un état (State) de votre application, puis calculer un nouvel état. Il faut prendre garde à ne pas modifier le State, mais bien à en créer un nouveau par exemple par duplication. Si des sous-objets du State n'ont pas changé, vous pouvez les inclure dans le nouveau State. Ça permet de faire de la comparaison légère en ne tenant compte que des références des sous-objets et non de leur contenu. (https://anybox.fr/blog/appli-web-histoire-du-dom-react-redux)

Pour pouvoir persister notre store nous devons utiliser redux-persist.
