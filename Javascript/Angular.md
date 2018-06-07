
# Angular JS

## Gérer les données

### String interpolation
Récupération et injection d'une variable depuis le TypeScript vers le template HTML.

```html
<h4>Appareil : {{ appareilName }} -- Statut : {{ getStatus() }}</h4>
```


### Property binding
Modifier dynamiquement les propriétés du DOM en fonction de TypeScript.

```html
<button [disabled]="!isAuth">Send</button>
```
*Désactive le bouton si `isAuth===false`*

## Event binding
Réagir dans TypeScript aux évènements venant du template HTML.

```html
<button (click)="onAllumer()">Tout allumer</button>
```
*[Voir la liste des évènements](https://www.w3schools.com/angular/angular_events.asp)*

## Two-way binding


## Propriétés personnalisées
