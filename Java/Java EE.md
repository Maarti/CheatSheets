# Java EE cheatsheet


### Servlet

* Le client envoie des requêtes au serveur grâce aux méthodes du protocole HTTP, notamment GET, POST et HEAD.

* Le conteneur web place chaque requête reçue dans un objet HttpServletRequest, et place chaque réponse qu'il initialise dans l'objet HttpServletResponse.

* Le conteneur transmet chaque couple requête/réponse à une servlet : c'est un objet Java assigné à une requête et capable de générer une réponse en conséquence.

* La servlet est donc le point d'entrée d'une application web, et se déclare dans son fichier de configuration web.xml.

* Une servlet peut se charger de répondre à une requête en particulier, ou à un groupe entier de requêtes.

* Pour pouvoir traiter une requête HTTP de type GET, une servlet doit implémenter la méthode doGet() ; pour répondre à une requête de type POST, la méthode doPost() ; etc.

Une servlet n'est pas chargée de l'affichage des données, elle ne doit donc pas s'occuper de la présentation (HTML, CSS, etc.).
* Une page JSP ressemble en apparence à une page HTML, mais en réalité elle est bien plus proche d'une servlet : elle contient des balises derrière lesquelles se cache du code Java.
* Une page JSP est exécutée sur le serveur, et la page finale générée et envoyée au client est une simple page HTML : le client ne voit pas le code de la JSP.
* Idéalement dans le modèle MVC, une page JSP est accessible à l'utilisateur à travers une servlet, et non pas directement.
* Le répertoire /WEB-INF cache les fichiers qu'il contient à l'extérieur de l'application.
* Nulle part dans votre code ne doit être mentionné le répertoire WebContent ! C'est une représentation de la racine de l'application, propre à Eclipse uniquement.
* La méthode forward() de l'objet RequestDispatcher permet depuis une servlet de rediriger la paire requête/réponse HTTP vers une autre servlet ou vers une page JSP.

### Transmission de données

* Un attribut de requête est en réalité un objet stocké dans l'objet HttpServletRequest, et peut contenir n'importe quel type de données.

* Les attributs de requête sont utilisés pour permettre à une servlet de transmettre des données à d'autres servlets ou à des pages JSP.

* Un paramètre de requête est une chaîne de caractères placée par le client à la fin de l'URL de la requête HTTP.

* Les paramètres de requête sont utilisés pour permettre à un client de transmettre des données au serveur.

#### Scopes

* **la page :** les objets créés avec la portée page ne sont accessibles que depuis cette même page, et une fois la réponse retournée au navigateur ces données ne sont plus accessibles ;

* **la requête :** les objets créés avec la portée request ne sont accessibles que depuis les pages qui traitent cette même requête. Si la requête est transmise à une autre page, les données sont conservées, mais sont perdues en cas de redirection ;

* **la session :** les objets créés avec la portée session ne sont accessibles que depuis les pages traitant les requêtes créées dans cette même session. Concrètement, une session correspond à la durée pendant laquelle un visiteur va utiliser l'application, cette durée se terminant lorsque l'utilisateur ferme son navigateur ou encore lorsque l'application le décide (le développeur, pour être exact) ; par exemple via un lien de déconnexion ou encore un temps maximum de validité imposé après lequel la session est automatiquement détruite. Les données ainsi créées ne sont plus accessibles une fois que le visiteur quitte le site ;

* **l'application :** les objets créés avec la portée application sont accessibles depuis toutes les pages JSP de l'application web ! C'est en quelque sorte une variable globale, accessible partout.

### Technologie JSP / Expression Language

#### Objets implicites de la technologie JSP

*(accessibles directement depuis une JSP)*

|Identifiant|Type de l'objet|Description|
|--- |--- |--- |
|pageContext|PageContext|Il fournit des informations utiles relatives au contexte d'exécution. Entre autres, il permet d'accéder aux attributs présents dans les différentes portées de l'application. Il contient également une référence vers tous les objets implicites suivants.|
|application|ServletContext|Il permet depuis une page JSP d'obtenir ou de modifier des informations relatives à l'application dans laquelle elle est exécutée.|
|session|HttpSession|Il représente une session associée à un client. Il est utilisé pour lire ou placer des objets dans la session de l'utilisateur courant.|
|request|HttpServletRequest|Il représente la requête faite par le client. Il est généralement utilisé pour accéder aux paramètres et aux attributs de la requête, ainsi qu'à ses en-têtes.|
|response|HttpServletResponse|Il représente la réponse qui va être envoyée au client. Il est généralement utilisé pour définir le Content-Type de la réponse, lui ajouter des en-têtes ou encore pour rediriger le client.|
|exception|Throwable|Il est uniquement disponible dans les pages d'erreur JSP. Il représente l'exception qui a conduit à la page d'erreur en question.|
|out|JspWriter|Il représente le contenu de la réponse qui va être envoyée au client. Il est utilisé pour écrire dans le corps de la réponse.|
|config|ServletConfig|Il permet depuis une page JSP d'obtenir les éventuels paramètres d'initialisation disponibles.|
|page|objet this|Il est l'équivalent de la référence this et représente la page JSP courante. Il est déconseillé de l'utiliser, pour des raisons de dégradation des performances notamment.|


#### Objets implicites de la technologie EL

|Catégorie|Identifiant|Description|
|--- |--- |--- |
|JSP|pageContext|Objet contenant des informations sur  l'environnement du serveur.|
|Portées|pageScope|Une Map qui associe les noms et valeurs des attributs  ayant pour portée la page.|
| |requestScope|Une Map  qui associe les noms et valeurs des attributsayant pour portée la requête.|
| |sessionScope|Une Map  qui associe les noms et valeurs des attributsayant pour portée la session.|
| |applicationScope|Une Map  qui associe les noms et valeurs des attributsayant pour portée l'application.|
|Paramètres de requête|param|Une Map qui associe les noms et valeurs des paramètres  de la requête.|
| |paramValues|Une Map  qui associe les noms et multiples valeurs ** des paramètresde la requête sous forme de tableaux de String.|
|En-têtes de requête|header|Une Map qui associe les noms et valeurs des paramètres  des en-têtes HTTP.|
| |headerValues|Une Map  qui associe les noms et multiples valeurs ** des paramètresdes en-têtes HTTP sous forme de tableaux de String.|
|Cookies|cookie|Une Map qui associe les noms et instances des cookies.|
|Paramètres d’initialisation|initParam|Une Map qui associe les données contenues dans les  champs <param-name> et <param-value> de  la section <init-param> du fichier web.xml.|

* La technologie EL est fondée sur les JavaBeans et sur les collections Java, et existe depuis la version 2.4 de l'API Servlet.

* Les expressions EL remplacent les actions standard de manipulation des objets.

* Une expression EL permet d'effectuer des tests, interprétés à la volée lors de l'exécution de la page.

* L'interprétation des expressions EL peut être désactivée via une section dans le fichier web.xml.

* Un objet implicite n'est pas géré par le développeur, mais par le conteneur de servlets.

* Chaque objet implicite JSP donne accès à un objet mis à disposition par le conteneur.

* Chaque objet implicite EL est un raccourci vers des données de l'application.

### JSTL

#### Configuration

* la JSTL est composée de cinq bibliothèques de balises standard ;

* elle permet d'éviter l'utilisation de code Java dans les pages JSP ;

* elle permet de réduire la quantité de code à écrire ;

* elle rend le code des pages JSP plus lisible ;

* sous Tomcat, il faut placer son fichier .jar sous /WEB-INF/lib pour qu'elle soit correctement intégrée.

#### Balises
**<c:out>** À utiliser pour afficher les variables car il échappe les caracères XML `<c:out value="<p>Paragraphe</p>">`

**<c:set>** 
```jsp
<c:set var="message" value="Hello" scope="request" />
<c:out value="${requestScope.message}" />
```

[[Voir la liste](http://cs.roosevelt.edu/eric/books/JSP/jstl-quick-reference.pdf)]

## Resources
* [OpenClassroom](https://openclassrooms.com/courses/creez-votre-application-web-avec-java-ee/servlet-avec-vue)

