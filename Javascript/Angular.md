
# Gérer les données

## String interpolation
Récupération et injection d'une variable depuis le TypeScript vers le template HTML.

`<h4>Appareil : {{ appareilName }} -- Statut : {{ getStatus() }}</h4>`


## Property binding
Modifier dynamiquement les propriétés du DOM en fonction de TypeScript.

```
<button [disabled]="!isAuth">Send</button>
```
* Désactive le bouton si `isAuth===false` *

## Event binding

## Two-way binding


## Propriétés personnalisées
