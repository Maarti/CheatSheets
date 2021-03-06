
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

### Template reference variables [[doc](https://angular.io/guide/template-syntax#ref-vars)]
La syntaxe `#` déclare une variable locale qui référence un élément du DOM dans le template :
```html
<input type="text" #harry>
 {{ harry.value }}
```
On peut récupérer sa valeur depuis TypeScript de cette manière :
```typescript
import { Component, OnInit, ViewChild } from '@angular/core';

// [...]

export class SurveyComponent implements OnInit {
	@ViewChild('harry') scrollTarget;  // reference of #harry element in the template
	
	ngOnInit() {
		this.scrollTarget.nativeElement.scrollIntoView({ behavior: "smooth", block: "start" });  
	}
```

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
Un classe qui permet de centraliser des parties du code (champs, méthodes...).

### 1. Création du Service
Créer un fichier `/services/hero.service.ts` *(par exemple)*
```typescript
export class HeroService {
  private heroes: Hero[] = [];

  constructor() { }

  getHeroes() {
    // [...]
    return this.heroes;
  }
}
```

### 2. Injection du Service dans un Component
Quand Angular créé l'instance d'un Component, il détermine quels Services ce Component a besoin en regardant les types des paramètres de son constructeur. Pour injecter un Service dans un Component, on l'ajoute donc en paramètre de son constructeur :
```typescript
import { HeroService } from '../services/hero.service';
// [...]
constructor(private service: HeroService) { }
```

### 3. Déclarer le Service dans un Provider
Il faut enregistrer notre Service dans au moins un tableau de Provider. Il peut être enregistré à 3 niveaux différents :
* dans `AppModule` : la même instance du service sera utilisée par tous les components de l'application et par les autres services ;
* dans `AppComponent` : tous les components auront accès à la même instance du service mais pas les autres services ;
* dans un autre component : le component lui-même et ses enfants auront accès à la même instance du service, mais pas le reste de l'application.

```typescript
providers: [
  BackendService,
  HeroService,
  Logger
],
```

[OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/ameliorez-la-structure-du-code-avec-les-services)

## Routing [[doc](https://angular.io/guide/router)]
[OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/gerez-la-navigation-avec-le-routing)

### Routes
Définit quel(s) component(s) il faut afficher à quel(s) endroit(s) pour une URL donnée.

Création des routes :
```typescript
import { Routes } from '@angular/router';
// [...]
const appRoutes: Routes = [
  { path: 'appareils', component: AppareilViewComponent }, // Affiche le component AppareilView pour l'url localhost:4200/appareils
  { path: 'auth', component: AuthComponent },
  { path: '', component: AppareilViewComponent }
];
// [...]
  imports: [
    RouterModule.forRoot(appRoutes)
	]
```

Dire à Angular où afficher les components dans le template avec la balise `<router-outlet>` :
```html
<div>
      <router-outlet></router-outlet>
</div>
```

Créer un lien :
```html
<a routerLink="auth">Authentification</a>
```

### Redirect
Redirection et wildcard :
```typescript
const appRoutes: Routes = [
  { path: 'not-found', component: FourOhFourComponent },
  { path: '**', redirectTo: 'not-found' }
]
```

Renvoyer vers une URL après une action :
```typescript
onSignIn() {
    this.authService.signIn().then(
      () => {
        console.log('Sign in successful!');
        this.authStatus = this.authService.isAuth;
        this.router.navigate(['appareils']);
      }
    );
}
```

### Paramètres URL
```typescript
  { path: 'appareils/:id', component: SingleAppareilComponent },
```

Récupérer le paramètre de l'URL :
```typescript
constructor(private route: ActivatedRoute) { }
// [...]
this.id = this.route.snapshot.params['id'];
```

Création d'un lien :
```html
<a [routerLink]="[id]">Détail</a>
```

## Guard  [[doc](https://angular.io/guide/router#milestone-5-route-guards)]
Une Guard est un service qu'Angular exécutera au moment où l'utilisateur essaye de naviguer vers la route sélectionnée *(plutôt que d'exécuter du code dans le onInit de chaque Component)*.
[Voir cours OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/gerez-la-navigation-avec-le-routing#/id/r-5089287)

## Observable [[doc](https://angular.io/guide/observables)]
Objet qui émet des informations auxquelles on souhaite réagir.

[Cours OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/observez-les-donnees-avec-rxjs#/id/r-5089338)

## Subject [[doc](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/subjects.md)]
C'est à la fois un Observer et un Observable, il permet de réagir à de nouvelles informations, mais également d'en émettre. Il peut donc servir de proxy entre un groupe de Subscribers et une source.

[Cours OpenClassrooms](https://openclassrooms.com/courses/developpez-avec-angular/observez-les-donnees-avec-rxjs#/id/r-5089444)

## Operators [[doc1](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/operators.md) - [doc2](https://angular.io/guide/rx-library#operators)]
Un opérateur est une fonction située entre l'Observable et l'Observer qui peut modifier les données reçues avant qu'elles n'arrivent à la Subscription.

## Forms
### Template


### Reactive [[doc](https://angular.io/guide/reactive-forms)]


## Change detection
By default Angular run change detection on each component. We can optimize it using **immutable objects** and telling Angular to run change detection on a component's subtree **only if its inputs changed** using `ChangeDetectionStrategy.OnPush` (from [this article](https://blog.thoughtram.io/angular/2016/02/22/angular-2-change-detection-explained.html)).

Moreover, we can use **Observables** and `markForCheck()` an entire tree path of the change detection when a change occurs on the Observable:
```typescript
@Component({
  template: '{{counter}}',
  changeDetection: ChangeDetectionStrategy.OnPush
})
class CartBadgeCmp {

  @Input() addItemStream:Observable<any>;
  counter = 0;

  constructor(private cd: ChangeDetectorRef) {}

  ngOnInit() {
    this.addItemStream.subscribe(() => {
      this.counter++; // application state changed
      this.cd.markForCheck(); // marks path
    })
  }
}
```


## Create customizable component with directives

Generate directive:
```
ng g d shared\directive\modal\modalTitle
```

In the customizable component template, position the modalTitle:
```
<ng-container *ngTemplateOutlet="modalTitle"></ng-container>
<ng-content></ng-content>
```

Select the content thanks to the directive:
```typescript
@ContentChild(ModalTitleDirective, { static: false, read: TemplateRef }) public modalTitle: TemplateRef<any>;
```

In the implementation, use the directive in the content of the customizable component:
```html
<my-modal>
  <ng-template modalTitle> The title </ng-template>
  The body
</my-modal>
```


## [Deploy Angular App on GithubPages](https://alligator.io/angular/deploying-angular-app-github-pages/)
* First install the angular-cli-ghpages globally : `npm install -g angular-cli-ghpages`
* Build project with href location : `ng build --prod --base-href "https://<user-name>.github.io/<repo>/"`
* Deploy : `ngh`

**If the app is in a subfolder** and you have the `index.html could not be copied to 404.html` [error](https://github.com/angular-schule/angular-cli-ghpages/issues/37), set the base href : `ngh --dir dist/[PROJECTNAME]`

## Collaborate
* Clone the repo : `git clone https://github.com/<user-name>/<repo>.git`
* Install node_modules folder : `npm install`
* Run : `npm start`

## Notes
* Check the version of Angular, typescript, rxjs ... : `ng -v`
* Updating Angular Version : [Angular Update Guide](https://update.angular.io/)
* Quickly display values of a form : 
```html
<form [formGroup]="myForm">
	<!-- [...] -->
</form>
<pre>{{ myForm.value | json }}<pre>
```
* "Dropping unreachable code" and other imprecise warnings from ng-packagr
Display the concerned file in the console warning by changing `node_modules/ng-packagr/lib/flatten/uglify.js` line :
```
 const result = terser_1.minify(inputFileBuffer.toString(), {
```
to 
```
 const result = terser_1.minify({ [inputPath]: inputFileBuffer.toString() }, {
```
(from [this commit](https://github.com/pfeigl/ng-packagr/commit/5f8b719419419448ab327259a213f57f909ac814) of [this issue](https://github.com/ng-packagr/ng-packagr/issues/882))

## Resources
* [Angular Docs](https://angular.io/docs)
* [Angular Cheatsheet](https://angular.io/guide/cheatsheet)
* [OpenClassrooms tutorial](https://openclassrooms.com/courses/developpez-avec-angular)
