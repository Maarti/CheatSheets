
# Angular JS

## Gérer les données


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


## Event binding
Pour réagir dans TypeScript aux évènements venant du template HTML. On utilise les parenthèses pour le déclarer `( )`.
```html
<button (click)="onAllumer()">Tout allumer</button>
```
*[Voir la liste des évènements](https://www.w3schools.com/angular/angular_events.asp)*


## Two-way binding
Pour déclarer **et** récupérer le contenu le contenu d'un champ *(par exemple)*. On utilise `[()]` pour le déclarer.

Il faut importer **FormsModule** dans l'app.module.ts :
```typescript
import { FormsModule } from '@angular/forms';
@NgModule({
//...
  imports: [
    FormsModule
  ]
})
```
```html
 <h4>Name : {{ name }}</h4>
  <input type="text" class="form-control" [(ngModel)]="name">
```
**Il y a une nouvelle instance du component pour chaque réutilisation de celui-ci. Donc la modification de la variable `name` n'impacte que l'instance du component en cours.**

## Propriétés personnalisées
