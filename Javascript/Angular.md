
# Angular cheatsheet

## Données dyamiques

### String interpolation
Pour récupérer et injecter une variable depuis le TypeScript vers le template HTML. On utilise les double-accolades pour le déclarer `{{ }}`.
```html
<h4>Appareil : {{ appareilName }} -- Statut : {{ getStatus() }}</h4>
```


### Property binding
Pour modifier dynamiquement les propriétés du DOM en fonction de TypeScript. On utilise les crochets pour le déclarer `[ ]`.
```html
<button [disabled]="!isAuth">Send</button>
```
*Désactive le bouton si `isAuth===false`*


### Event binding
Pour réagir dans TypeScript aux évènements venant du template HTML. On utilise les parenthèses pour le déclarer `( )`.
```html
<button (click)="onAllumer()">Tout allumer</button>
```
*[Voir la liste des évènements](https://www.w3schools.com/angular/angular_events.asp)*


### Two-way binding
Pour déclarer **et** récupérer le contenu d'un champ *(par exemple)*. On utilise `[( )]` pour le déclarer.

Il faut importer **FormsModule** dans l'app.module.ts :
```typescript
import { FormsModule } from '@angular/forms';

//	[...]

@NgModule({
  // [...]
  imports: [
    FormsModule
  ]
})
//	[...]
```
```html
 <h4>Name : {{ name }}</h4>
  <input type="text" class="form-control" [(ngModel)]="name">
```
=> Il y a **une nouvelle instance** du component pour **chaque réutilisation** de celui-ci. Donc la modification de la variable `name` **n'impacte que l'instance du component en cours**.


### Propriétés personnalisées
Pour déclarer une propriété qui peut être mise à jour via **Property binding**.
```typescript
import { Input } from '@angular/core';

// [...]

// On déclare 2 propriétés grâce à @Input()
@Input() appareilName: string;
@Input() appareilStatus: string;
```

```typescript
appareilOne = 'Machine à laver';
appareilTwo = 'Frigo';
```

```html
<!--	On donne à la propriété appareilName la valeur de la variable appareilOne
	On donne à la propriété appareilStatus la valeur de la string 'éteint' -->
<app-appareil [appareilName]="appareilOne" [appareilStatus]="'éteint'"></app-appareil>
<app-appareil [appareilName]="appareilTwo" [appareilStatus]="'allumé'"></app-appareil>
```
*Si on emploit les crochets pour le property binding et qu'on souhaite y passer un string, il faut le mettre **entre apostrophes**, sinon c'est le nom d'une variable qui est passé. (exemple : `[appareilStatus]="'éteint'"`)*


## Built-in directives

### Les directives structurelles [[doc](https://angular.io/guide/structural-directives)]
*Les directives structurelles sont précédées d'un astérisque* `*`
#### *ngIf
Le composant ne s'affichera que si la condition `*ngIf="condition"` est `true`.
```html
<div *ngIf="appareilStatus === 'éteint'">OFF</div>
```

#### *ngFor
`*ngFor="let obj of myArray"` permet d'ittérer sur `myArray` pour récupérer les propriétés de `obj` grâce au **property binding**.

```typescript
appareils = [
    {
      name: 'Machine à laver',
      status: 'éteint'
    },
    {
      name: 'Frigo',
      status: 'allumé'
    },
    {
      name: 'Ordinateur',
      status: 'éteint'
    }
  ];
```
```html
<app-appareil  *ngFor="let appareil of appareils"
                       [appareilName]="appareil.name"
                       [appareilStatus]="appareil.status"></app-appareil>
```

### Les directives par attribut [[doc](https://angular.io/guide/attribute-directives)]
#### ngStyle
 Permet d'appliquer des styles de manière dynamique.
```html
<h4 [ngStyle]="{color: getColor()}">Appareil {{ getStatus() }}</h4>
```
```typescript
getColor() {
    if(this.appareilStatus === 'allumé') {
      return 'green';
    } else if(this.appareilStatus === 'éteint') {
      return 'red';
    }
}
```

#### ngClasse
Permet d'ajouter des classes dynamiquement.
```html
<li [ngClass]="{'list-group-item': true,
                'list-group-item-success': appareilStatus === 'allumé',
                'list-group-item-danger': appareilStatus === 'éteint'}">
```
On peut également passer directement un objet contenant tous les attributs nécessaires :
```html
<li [ngClass]="myClassObject">
```

## Pipes [[doc](https://angular.io/guide/pipes)]
Permet de modifier l'affichage d'un objet sans en modifier la nature. 
```typescript
lastUpdate = new Date();
```
```html
<p>Mis à jour : {{ lastUpdate }}</p>
<p>Mis à jour : {{ lastUpdate | date }}</p>
<p>Mis à jour : {{ lastUpdate | date: 'short' }}</p>
<p>Mis à jour : {{ lastUpdate | date: 'y MMMM EEEE d' | uppercase }}</p> <!-- Chaîne de Pipes -->

<!-- Affiche
	Mis à jour : Fri Jun 08 2018 14:27:27 GMT-0400 (heure normale de l’Amazonie)
	Mis à jour : Jun 8, 2018
	Mis à jour : 6/8/18, 2:27 PM
	Mis à jour : 2018 JUNE FRIDAY 8 -->
```
**AsyncPipe** permet de gérer les données asynchrones *(attends que la donnée soit reçue avant de continuer d'exécuter la Pipe)*. Très utile pour les données récupérées depuis un serveur externe. ([voir la doc](https://angular.io/guide/pipes#the-impure-asyncpipe))

## Services  [[doc](https://angular.io/guide/architecture-services)]
Permet de centraliser des parties du code.

Un service doit être injecté ; 3 niveaux possibles :
* dans `AppModule` : la même instance du service sera utilisée par tous les components de l'application et par les autres services ;
* dans `AppComponent` : tous les components auront accès à la même instance du service mais pas les autres services ;
* dans un autre component : le component lui-même et ses enfants auront accès à la même instance du service, mais pas le reste de l'application.

[Lifecycle Hooks doc](https://angular.io/guide/lifecycle-hooks)

[OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/ameliorez-la-structure-du-code-avec-les-services)

## Routes [[doc](https://angular.io/guide/router)]
[OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/gerez-la-navigation-avec-le-routing)



## Resources
* [Angular Docs](https://angular.io/docs)
* [Angular Cheatsheet](https://angular.io/guide/cheatsheet)
* [W3schools Angular](https://www.w3schools.com/angular/default.asp)
* [OpenClassrooms tutorial](https://openclassrooms.com/courses/developpez-avec-angular)