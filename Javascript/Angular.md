
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


## Directives

### Les directives structurelles


### Les directives par attribut


## Resources
* [Angular Docs](https://angular.io/docs)
* [W3schools Angular](https://www.w3schools.com/angular/default.asp)
* [OpenClassrooms tutorial](https://openclassrooms.com/courses/developpez-avec-angular)