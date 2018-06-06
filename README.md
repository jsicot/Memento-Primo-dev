# Memento-Primo-dev
## Pré-requis

- Notions en HTML, CSS et éventuellement JS
- Privilégier l'utilisation de Git et Github ([Memento](https://services.github.com/on-demand/downloads/fr/github-git-cheat-sheet.pdf) et [client pour les débutants](https://desktop.github.com/))
- Documentation Ex-Libris ([Primo NUI](https://knowledge.exlibrisgroup.com/Primo/Training/New_Primo_Interface) et [New UI Customization](https://knowledge.exlibrisgroup.com/Primo/Product_Documentation/New_Primo_User_Interface/New_UI_Customization_-_Best_Practices  ))
- [Appréhender la logique MVC (modèle - vue - controleur) d'Angular JS.](https://openclassrooms.com/courses/developpez-vos-applications-web-avec-angularjs/qu-est-ce-qu-angularjs)
	- Le [**component**](https://docs.angularjs.org/guide/component) = jour le rôle de la vue;
	- Le controleur (https://code.angularjs.org/snapshot/docs/guide/controller)	
	- L'objet [**$scope**](https://docs.angularjs.org/guide/scope) = joue donc le rôle du modèle.
- Comprendre la notion de [*directive*](https://docs.angularjs.org/guide/directive) dans Angular JS. 
	- Les *directives* sont utilisées lorsque l'on souhaite modifier ou transformer le DOM (Document Object Model).
- Appréhender le framework [Material Design d'Angular](https://material.angularjs.org/latest/) : module d'intégration qui permet d'obtenir facilement une interface responsive
- Savoir utiliser une console web (de préférence celle du navigateur Chrome)

## Techonologies utilisées
- [NodeJS](https://nodejs.org/fr/) : framework de développement Javascript
- [Gulp](https://gulpjs.com/) :un task runner qui permet d'automatiser certaines tâches de développement (création d'un serveur web local, rafraîchissement automatique du navigateur à chaque modification de fichier, préprocesseurs Sass ou LESS, optimisation des CSS, JavaScript et images)
- [Npm](https://www.npmjs.com/) : un gestionnaire de « packages » (ie librairies, modules, plugins) Node.js


## Philosophie et objectifs
- Tout client (quelque soit sa configuration) doit pouvoir créer facilement une vue pour son institution
- Possibilité d'intervenir sur de nombreux éléments sans forcément toucher au JS
- La personnalisation est possible directement en local, permet de se libérer du backend de Primo. Aucun accès ssh, sftp au serveur distant n'est nécessaire
- Joue le rôle de serveur proxy en utilisant l'API REST de Primo
- S'appuie sur le *customization package*, c-à-d un ensemble de fichiers (HTML, CSS et JS + Images) qui permettent de surcharger/outrepasser les templates natifs de l'interface Primo Explore
- ExLibris a prévu de nombreuses directives permettant de *hooker* l'interface

## Installation. [todo](https://github.com/ExLibrisGroup/primo-explore-devenv#installation). 


Optionnel : [installer Git](https://git-scm.com/downloads).

1. Télécharger (ou cloner via git) l'environnement de développement via [Github](https://github.com/ExLibrisGroup/primo-explore-devenv)

	- `git clone https://github.com/ExLibrisGroup/primo-explore-devenv.git`

2. [Installer nodejs v6.9.2](https://nodejs.org/download/release/v6.9.2/)

3. Installer Npm : `npm install npm@3.3.12 -g`

4. Installer Gulp : `npm install -g gulp`

5. Aller dans le dossier racine de l'environnement de dev : `cd /path/to/your/project/folder/primo-explore-devenv`

6. Installer les dépendances nodesjs (ie packages npm) : `npm install`

7. Téclécharger ou cloner le [primo-explore-package](https://github.com/ExLibrisGroup/primo-explore-package "primo-explore-package repository")) depuis Github et le placer dans le dossier `/path/to/your/project/folder/primo-explore-devenv/primo-explore/custom`
	- choisir de préférence la dernière version stable (dernier tag)

```sh
# Get new tags from the remote
$ git fetch --tags
 
# Get the latest tag name
$ latestTag=$(git describe --tags `git rev-list --tags --max-count=1`)
 
# Checkout the latest tag
$ git checkout $latestTag
```

8. Renommer ce dossier en fonction de l'identifiant de votre vue Primo

9.  Éditer le fichier de configuration Gulp (dans `/path/to/your/project/folder/primo-explore-devenv/gulp/config.js`) pour changer le **proxy server** : `var PROXY_SERVER = http://your-server:your-port`. 
	- Utiliser l'url de l'instance production ou de la sandbox de votre frontend Primo. La vue déclarée ci-dessus doit exister. 
	- Si votre instance est en *https*, indiquez cette dernière avec le port, comme ceci : `var PROXY_SERVER = https://your-server:443`

10. Se placer dans le dossier de l'environnement dev pour lancer le serveur local via la commande : `gulp run --view <VIEW_CODE>`

```
> gulp run --view <VIEW_CODE>
[11:30:35] Starting 'connect:primo_explore'...
[11:30:35] Finished 'connect:primo_explore' after 111 ms
[11:30:35] Starting 'reinstall-primo-node-modules'...
[11:30:35] Finished 'reinstall-primo-node-modules' after 78 μs
[11:30:35] Starting 'watch-js'...
[11:30:35] Finished 'watch-js' after 21 ms
[11:30:35] Starting 'watch-custom-scss'...
[11:30:35] Finished 'watch-custom-scss' after 50 μs
[11:30:35] Starting 'watch-css'...
[11:30:35] Finished 'watch-css' after 5.32 ms
[11:30:35] Starting 'setup_watchers'...
[11:30:35] Finished 'setup_watchers' after 2.13 ms
[11:30:35] Starting 'custom-html-templates'...
[11:30:35] Finished 'custom-html-templates' after 17 ms
[11:30:35] Starting 'custom-js'...
[11:30:35] Finished 'custom-js' after 14 ms
[11:30:35] Starting 'custom-scss'...
[11:30:35] Finished 'custom-scss' after 5.86 μs
[11:30:35] Starting 'custom-css'...
[BS] Access URLs:
 -------------------------------------
       Local: http://localhost:8003
 -------------------------------------
          UI: http://localhost:3001
 -------------------------------------
 ```

	- **VIEW_CODE** = Identifiant de la vue et nom du customization package.
	- **Astuce** : pour connaître l'ensemble des commandes disponibles avec Gulp : `gulp -T`

11. Ouvrir votre navigateur à l'adresse : `localhost:8003/primo-explore/?vid=<VIEW_CODE>`, un frontend primo est visible. Tout est OK.

## Exemples de personnalisation

### Structure du customization package


```
├── css
│   ├── custom1.css
│   ├── README.md
├── html
│   ├── home_en_US.html
│   └── README.md
├── img
│   └── README.md
├── js
│   ├── custom.js
│   └── README.md
├── README.md
└── showDirectives.txt
```

### Personnalisation des CSS

#### Changer les couleurs

1. Copier le fichier colors.json disponible à l'emplacement `/path/to/your/project/folder/primo-explore-devenv/colors.json` dans `/path/to/your/project/folder/primo-explore-devenv/primo-explore/custom/<VIEW_CODE>`
2. Éditer ce fichier. Exemple :

```json
{
  "primary": "#53738C",
  "secondary" : "#A9CDD6",
  "backgroundColor" : "white",
  "links": "#5C92BD",
  "warning": "tomato",
  "positive": "#0f7d00",
  "negative": "gray",
  "notice": "#e08303"
}
```
3. Lancer la commande : `gulp app-css --view <VIEW_CODE>` 
	- génère un thème pour votre instance avec les couleurs définies
	- un fichier `app-colors.css` est créé dans votre customization package à l'emplacement : `/path/to/your/project/folder/primo-explore-devenv/primo-explore/custom/<VIEW_CODE>/css/app-colors.css`
	
#### Autres exemples

**Astuce** utiliser la console web pour identifier les sélecteurs css que vous souhaitez outrepasser/personnaliser.
**Précaution** lorsqu'on joue avec les css : ne pas casser le côté responsive de l'interface.

##### Exemple : inverser le main menu et la search bar

- Éditer le custom1.css

```css
.header.topbar-wrapper {
    flex-direction: column-reverse;
}
```
Primo Explore utilise beaucoup [le flex display](https://css-tricks.com/snippets/css/a-guide-to-flexbox/), ce qui permet de faire beaucoup de choses pour modifier l'affichage avec de simples déclarations css


## Astuces

Ne pas modifier directement le `custom1.css`.

L'ensemble des fichiers **css** présents dans le dossier `primo-explore/custom/<VIEW_CODE>/css` seront agrégés dans `custom1.css`.

Il est également possible d'utiliser un preprocesseur CSS de type [Sass](https://sass-lang.com/install) afin de mieux organiser ses développements sur les css.

Possibilité d'extraire les fichier .scss natifs de primo avec la ligne de commande suivante :

`gulp extract-scss-files`

[Pour en savoir plus](https://youtu.be/kOXJQl84K_E)


### Personnalisation via Javascript

#### Création du Package.json

`Npm init -y`

Le package.json va permettre de renseigner à npm les métadonnées de notre projet ainsi que des dépendances utilisées.

#### Identifier les directives disponibles

Déboguage des directives/components : utilisation de la console web de Chrome.

La console web permet d'avoir accès à une partie du code source = **documentation principale**

```js
angular.reloadWithDebugInfo(); // important !! pour lancer primo en mode debug. A exécuter à chaque utilisation.
angular.element($0).scope().$ctrl

```

L'ensemble des directives en **<prm-xxx-after>** permettent de créer un nouveau component.

Utiliser le **bookmarklet** fourni dans le customisation package : `showDirectives.txt` pour afficher l'ensemble des directives disponibles sur une page données.

```js
javascript:(function(){var%20script=document.createElement(%22SCRIPT%22);script.src='https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js';script.type='text/javascript';document.getElementsByTagName(%22head%22)[0].appendChild(script);var%20checkReady=function(callback){if(window.jQuery){callback(jQuery)}else{window.setTimeout(function(){checkReady(callback)},100)}};checkReady(function($){$('primo-explore').find('[parent-ctrl=%22$ctrl%22]').each(function(){$(this).append('<a%20href=%22#%22%20title=%22'+$(this)[0].outerHTML.replace(/</g,'').replace(/>/g,'').replace(/\//g,'').replace(/%22/g,'').replace(/parent-ctrl./g,'').replace(/-([a-z])/g,function(m,w){return%20w.toUpperCase()}).replace(/\$ctrl(.*)/g,'')+'%22%20style=%22display:block;height:auto;color:black;%22>Hover%20for%20id</a>')})})})();
```

##### Exemple : récupérer l'élément puis le controleur de **prm-search-bar**

```js
e = angular.element(document.querySelector('prm-search-bar'));
c = e.controller('prm-search-bar');
```

##### Fonctions utiles ([source](https://docs.google.com/document/d/1pfhN1LZSuV6ZOZ7REldKYH7TR1Cc4BUzTMdNHwH5Bkc/edit#heading=h.5jv2vx23tkuk))

###### Lister tous les components

```js
function getComponents() {
let tags = document.getElementsByTagName('*');
let components = [];
for (let tag of tags) {
  let tagName = tag.localName;  
  if (/^prm-/.test(tagName)){
    let component = {name: tagName, obj:angular.element(tag)};
    components.push(component);
  }
}
    return components;
}
```

###### Retourner l'objet scope d'un component donné

```js
function getComponentScope(componentName) {
let app = getComponents().filter((f)=>f.name===componentName)
.map((m)=>angular.element(m.obj[0]).scope())

return app;
}
```

###### Retourner l'objet controller d'un component donné

```js
function getComponentCtrl(componentName) {
    return getComponentScope(componentName).map((m)=> (m.$ctrl || m.$$childHead.$ctrl))
}
```

###### Récupérer un ensemble de résultats depuis la console web

```js
var prmSearchEl = angular.element(document.querySelector('prm-search'));
var prmSearchScope = prmSearchEl.scope();
var resultSet = prmSearchScope.$$childTail.$ctrl.searchResults;
console.log(resultSet); // Tous les résultat
console.log(resultSet[0]["@id"]); // URI du premier résultat
console.log(resultSet[0].pnx.display.title); // Titre du premier résultat
```

#### Installer un module Npm

De nombreux modules ont déjà été réalisés/partagés par la communauté : https://www.npmjs.com/search?q=primo-explore

Pour faciliter le déploiement de modules, il est conseillé d'utiliser **Browserify**.

[Browserify](http://browserify.org/) : simplifie l'écriture du code et l'integration des packages npm. 

Même conseil que pour les css, ne pas éditer directement le `custom.js`
Créer un fichier **main.js** (en copiant le contenu du custom.js) dans le dossier `primo-explore/custom/<VIEW_CODE>/js`.

Lancer le serveur local avec **Browserify** : `gulp run --view <VIEW_CODE> --browserify`

Cela permet d'utiliser l'environnement de développement avec la méthode ES6. 
Le main.js et tout code javascript est automatiquement transpilé dans custom.js avec rechargement navigateur pour voir les modifications en live.

##### Exemple : installation du module [Unpaywall](https://www.npmjs.com/package/primo-explore-oadoi-link)

```sh
cd primo-explore/custom/<VIEW_CODE>
npm install primo-explore-oadoi-link --save-dev
```
###### Éditer le fichier main.js

```js
//Ajouter la ligne suivante en haut du fichier
import 'primo-explore-oadoi-link';
```
```js
//Ajouter oaidoi dans les modules angulars appelée au niveau de l'application
    var app = angular.module('viewCustom', [
    										'angularLoad',
											'oadoi'
    										]);
```
```js
 //Ajouter les variables nécessaires au fonctionnement du module
    app
	  .constant('oadoiOptions', {
	  	"imagePath": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIAAAACACAMAAAD04JH5AAAAk1BMVEX///81vfYqufWy7eNUwus3vvZ92uWp6+IuvPcoufYxvfjZ8PlUx/XQ9urV7vn6//3I6fVgxeNGwvYxtu1Yv92E3eVay/Hq+/SI3+Nzy+Ch6OJ01uiw4O1Mxfjy/fjE8+e95fGT1eRnxuCk3Oljz+1Fu+x7ytpSu9+J0OBLuedYvt+s4OuS2eaU4+LZ+O3J9Oht1OtlyPIDAAADeklEQVR4nO2aa3fiIBCGBY0OWV3XEOttTdN2Y2/W9v//uo0b04uGzEDgcE6X92PCME9gYIDQ6wUFBQUFBX0SexcMCJrNVvu7/JcTAAZEsahY7Z9tQTBTAefJbO8RoGK4ff7hEaAU58WDV4BjM6w6hUNngCODiH56BSgRiju/AGVH3Bp2hCWAMhyLG78AZSMYBYI9gBKBGTSCTYCyEXZ+AcpI0O4GywBspktgG4CJJz0E6wBMzDwDMKGVIB0AMK2h4AIA5G+/AGVuoicGcp28EpBK8xk5Dqjek/m6fz162WwZCYGT10kkgGjTX5zKTydjzgnI0h4Av5qc2WQvBARqXkI/hc+nl1YJTkCNQ/T7101WizFKIFZ2ABr9kwhYbgGAv32UzA6TxafeeEVHAydNR61VQFIHfy97SyIWjecfAYk2ASdlpfYqRnWx/vY4BQFwGNaP8E7gXQFgXDf58mPsi7oN+u4B3jtAfKl2e3qMzwaU6bDNfnMqc/gab+LUCxM0DAtCRmizr4fg8PzF4d/jbIsRUMZBm/1rVWQRnde7rF68YX1AmYxazKH60Mtog3H1YokBxAW+QG0DOI2B+aWf6sUaHwf46owAsFEBjFAAGKBh2GZexcAiuYw1KgCTaE5ss95eZ1l2+NPghgzA0YOLdvvjqWCTyADw1A1AJTJAXHgGqIv6A0AT0rcHgACATYVqS66UOHXsWhAmAiwdqQw3C8SwUj9C1gSmALxhO9RMgDQCYMlABUD035uO25vAFACdwN7VkKxtAERkgCECYBgD9gAMh+H3ATDNBQHg2wAAWpFrgIFnAI6e1jkGwI+t3QIQdqduAeAWtXcKEONbQ7cAQDi1dwqAjwHHAIQecAtAOat1CYCuBVwDdDoptQCAnw20AJCX5b0rJYAg/bhSWS9pO5NJwwlW/Q20H2dK86uXPq6RemcGj7S/6Cp7pt6bfpZ6W4SfjyEAXZUS/5268k+OYkf+8fNBtwCxzP0CUNKgQwBINe6xuAB41LnX5sA/5Br+HQDE5KsDbgBiqXe30bZ/TffWAUD7aqdl/6Q1iDsAcZ/7BACjS6XW3Mfi3sS/NQCQO7PLzZb881Tj/pp1ACH177JaBIjlrsvt9q7egWvlPtsAINMb84v1HQEAuDSYeLoDlI65LNJOHW8OEEk5SFcPecd2DwoKCgr63/UXnxY8Wl1A45AAAAAASUVORK5CYII=",
	  	"email": "yourmail@home.fr"
	  });
```


#### Créer un component simplement : exemple d'un menu

Éditer le `main.js`, ajouter :


```js
	app.component('prmTopBarBefore', {
	     templateUrl: 'custom/<VIEW_CODE>/html/customnav.html'
	});
```
Dans le dossier html du customization package, créer un nouveau fichier customnav.html avec le contenu suivant :
```html
<prm-customnav>
<div layout="row" layout-padding layout-align="space-between center">
<div>
    <md-button>Accueil</md-button>
    <md-button>Bibliothèques</md-button>
    <md-button>Services</md-button>
    <md-button class="hide-xs">Collections</md-button>
     <md-button class="hide-xs">Ressources</md-button>
     <md-button class="hide-xs">Actualités</md-button>
    <md-menu>
        <md-button md-menu-origin ng-click="$mdOpenMenu()">Aide et Formation</md-button>
        <md-menu-content width="2">
            <md-menu-item>
                <md-button>Ateliers de la BU</md-button>
            </md-menu-item>
            <md-menu-item>
                <md-button>Guides en ligne</md-button>
            </md-menu-item>
              <md-menu-item>
                <md-button>RDV avec un bibliothécaire</md-button>
            </md-menu-item>
        </md-menu-content>
    </md-menu>
</div>
<div class="nav-buttons">
    <md-button class="md-raised md-accent">Mon compte lecteur</md-button>
</div></prm-customnav>

```
Enfin, au niveau des css ajouter : 
```css
prm-topbar {
    height: 100%;
}
prm-topbar .top-nav-bar {
    height: 60px;
}
prm-customnav .layout-padding {
    background: #333;
    color: #FFF;
}
prm-logo .logo-image, prm-logo img {
    max-height: 40px;
}
```

#### Création d'un module avec appel d'un webservice externe

Créer un fichier intitulé `sfxHoldings.module.js` dans `primo-explore/custom/<VIEW_CODE>/js` avec le code ci-dessous :

```js
angular.module('sfxHoldings', []).component('prmViewOnlineAfter', {
  bindings: { parentCtrl: '<' },
  controller: function controller($scope, $http, $element, sfxholdingsService) {
    this.$onInit = function () {
      var obj = $scope.$ctrl.parentCtrl.item.linkElement.links[0];
      if (obj.hasOwnProperty("getItTabText") && obj.hasOwnProperty("displayText") && obj.hasOwnProperty("isLinktoOnline") && obj.hasOwnProperty("link")) {
        if (obj['displayText'] == "openurlfulltext") {
	      console.log(obj);
	      console.log(obj['link']);
          var openurl = obj['link'];
          var openurlSvc = openurl.replace("http://acceder.bu.univ-rennes2.fr/sfx_33puedb","https://catalogue.bu.univ-rennes2.fr/r2microws/getSfx.php");
          var response = sfxholdingsService.getSfxData(openurlSvc).then(function (response) {
            var holdings = response.data;
            if (holdings === null) {
	            
            } else {
	          angular.element(document.querySelector('prm-view-online div a.arrow-link.md-primoExplore-theme'))[0].style.display = "none"; 
// 	          console.log(holdings);
              $scope.sfxholdings = holdings;
            }
          });
        } 
      } 
    };
  },
  template: `<prm-spinner class="inline-loader display-inline dark-on-light half-transparent" ng-if="sfxloading"></prm-spinner>

<div ng-if="sfxholdings" id="sfxholdings">
	<h3 class="section-title">En Ligne :</h3>
    <md-list class="separate-list-items margin-bottom-medium padding-bottom-zero">
        <md-list-item class="md-2-line _md-no-proxy _md" ng-repeat="(index, holding) in sfxholdings">
        <a class="neutralized-button layout-full-width layout-display-flex md-button md-ink-ripple layout-row" tabindex="0" layout="flex" href="{{holding.href}}" target="_blank" md-ink-ripple="red" role="button">
                <div layout="row" flex="100" layout-align="space-between center" class="layout-align-space-between-center layout-row flex-100">
                    <div class="md-list-item-text layout-wrap layout-row flex" layout="row" layout-wrap="" flex="">
                        <div flex="" flex-xs="100" class="flex-xs-100 flex">
                        <h3>{{holding.title}}</h3>
                            <p><span class="availability-status available">Accès</span>
                            	<span ng-if="holding.coverage">, </span>
								<span>{{holding.coverage}}</span></p>
						</div>
                        <div layout-align="end center" layout="row" layout-wrap="" flex-xs="100" flex-sm="30" flex="" class="list-item-actions layout-wrap layout-align-end-center layout-row flex-xs-100 flex-sm-30 flex"></div>
                    </div>
                    <prm-icon ng-if="!$ctrl.isOvp()" class="padding-right-small" icon-type="svg" svg-icon-set="action" icon-definition="ic_open_in_new_24px">
                        <md-icon md-svg-icon='action:ic_open_in_new_24px'></md-icon>
                        <prm-icon-after parent-ctrl="$ctrl"></prm-icon-after>
                    </prm-icon>
                </div>
                <div class="md-ripple-container" style=""></div>
            </div>
        </md-list-item>
    </md-list>
</div>
`
}).factory('sfxholdingsService', ['$http', function ($http) {
  return {
    getSfxData: function getSfxData(url) {
      return $http({
        method: 'JSONP',
        url: url
      });
    }
  };
}]).run(function ($http) {
  // Necessary for requests to succeed...not sure why
  $http.defaults.headers.common = { 'X-From-ExL-API-Gateway': undefined };
});

```

Éditer ensuite le `main.js` pour ajouter :


```js
import { sfxHoldings } from './sfxHoldings.module';
```

**Important** : il faut nécessaire de mettre le web service dans une liste blanche (utilisation de `$sceDelegateProvider.resourceUrlWhitelist()` ou `$sce.trustAsResourceUrl()`) pour autoriser les requêtes http externes.  

```js
	app.config(['$sceDelegateProvider', function ($sceDelegateProvider) {
	  var urlWhitelist = $sceDelegateProvider.resourceUrlWhitelist();
	  urlWhitelist.push('https://catalogue.bu.univ-rennes2**');
	  $sceDelegateProvider.resourceUrlWhitelist(urlWhitelist);
	}]);
```

### Personnalisation du HTML

Suit une convention de nommage. Exemples pour modifier la page d'accueil :

`home_en_US.html` > page d'accueil pour l'anglais
`home_fr_FR.html` > page d'accueil pour le français 


**Astuce** : les templates de primo sont accessibles depuis la **console web > sources > primo-explore > lib > templates.js**


### Personnalisation des images (logo, images pour les types de document, favicon)

Simplement déposer les images dans le dossier `img`.
Exemple pour les images des types de document  : icon_<resource-type>.png (se référer aux **code tables** dans le backend Primo).

**Astuce** : les icônes utilisées dans l'UI Primo sont définies dans le fichier `webpack:///www/components/appConfig/iconConfig.ts` (accès via console web)


### Générer l'archive de son customization package pour l'uploader dans le backend Primo

- `gulp create-package`

Choisir le numéro correspondant au nom de votre vue et cliquer sur entrée.
Le fichier zip est localisé dans `/path/to/your/project/folder/primo-explore-devenv/packages`


## [Primo Studio](https://github.com/ExLibrisGroup/Primo-Studio)

Proposer un éditeur de vue avec une IHM, le tout adossé à un "app store" pour étendre les fonctionnalités de Primo à l'aide de modules installable en un clic.
Un service qui sera probablement hébergé directement par ExLibris.

[Démonstrateur](http://ec2-18-217-175-187.us-east-2.compute.amazonaws.com:8004/)



## Sources

- [Google doc : New Primo UI cookbook](https://docs.google.com/document/d/1z1D5II6rhRd2Q01Uqpb_1v6OEFv_OksujEZ-htNJ0rw/edit#heading=h.xtcb9acz0ly2)
- [Google doc : Thoughts, ideas, tricks on the new Primo UI](https://docs.google.com/document/d/1pfhN1LZSuV6ZOZ7REldKYH7TR1Cc4BUzTMdNHwH5Bkc/edit#heading=h.5jv2vx23tkuk)
- [Dépôts sur Github](https://github.com/search?utf8=%E2%9C%93&q=primo-explore&ref=simplesearch)
- [Packages NPM](https://www.npmjs.com/search?q=primo-explore)
- [IGeLU 2017 Developers Day - EXPLORING THE NEW UI WITH PRIMO-EXPLORE-DOM](https://youtu.be/dsRmHblEn_Y)
- ELUNA/IGeLU Primo New UI Hackathon :
	- [Primo New UI: Day 1 - HTML and CSS](https://www.youtube.com/watch?v=ICvM8Xa_gkE)
	- [Primo New UI Day 2 - Basic Javascript](https://www.youtube.com/watch?v=kcWOlxs7VKI)
	- [Primo New UI Day 3 - Service Pages](https://www.youtube.com/watch?v=B9eR9jaC5lc)
	- [Primo Hackathon Day 4 - Primo Roadmap and Lightning Lalk](https://www.youtube.com/watch?v=dQR_LOleeHI)


## Exemples d'institutions utilisant la NUI + dépôts Github

- [REX - Royal Danish Library](https://rex.kb.dk/primo-explore/search?sortby=rank&vid=NUI&lang=en_US)
	- dépôt Github : https://github.com/Det-Kongelige-Bibliotek/primo-explore-rex
- [Brandeis University Library](https://search.library.brandeis.edu/primo-explore/search?sortby=rank&vid=BRAND)
	- dépôt Github : https://github.com/richshea/Brandeis-Primo-Customizations-Package
- [Ithaca College Library](https://ithaca-primo.hosted.exlibrisgroup.com/primo-explore/search?vid=01ITHACACOL_V1&lang=en_US)
	- dépôt Github : https://github.com/rgilmour70/primo-new-ui-custom
- [New-York University Library](http://bobcat.library.nyu.edu/primo-explore/search?vid=NYU-NUI&sortby=rank&lang=en_US)
	- dépôt Github : https://github.com/NYULibraries/primo-explore-nyu
- [University of Washington Libraries](https://alliance-primo.hosted.exlibrisgroup.com/primo-explore/search?vid=UW&tab=default_tab&sortby=rank&lang=en_US)
	- dépôt Github : https://github.com/UW-Libraries/uwlib-primo-nui
- [KTH Biblioteket](https://kth-primo.hosted.exlibrisgroup.com/primo-explore/search?vid=46KTH_VU1_L&lang=sv_SE)
	- dépôt Github : https://github.com/thompa21/kthb-primo-explore
- [Consortium Novanet (Canada)](https://novanet-primo.hosted.exlibrisgroup.com/primo-explore/search?vid=ACAD&sortby=rank&lang=en_US)
	- dépôt Github : https://github.com/novanet-libraries/new-ui-packages
- [Oregon State University Library](https://search.library.oregonstate.edu/primo-explore/search?vid=OSU&sortby=rank)
	- dépôt Github : https://github.com/osulp/osulp-primo-newui
- [Consortim Libis (Belgique)](http://limo.libis.be/index.html)
	- [KU Leuven](https://limo.libis.be/primo-explore/search?vid=Lirias)
	- dépôt Github :
		- https://github.com/libis/primoUI-custom-view-packages
		- https://github.com/libis/primoUI-central-package
- [Swinburne University of Technology Library](https://librarysearch.swinburne.edu.au/primo-explore/search?dscnt=0&vid=SWIN2&sortby=rank&lang=en_US)
	- dépôt Github : https://github.com/justinkelly/swinburne_primo_new_ui
- [Willamette University Library](https://alliance-primo.hosted.exlibrisgroup.com/primo-explore/search?vid=WU&tab=default_tab&mode=advanced&sortby=rank)
- [University of Queensland Library](https://search.library.uq.edu.au/primo-explore/search?vid=61UQ&sortby=rank)
	- dépôt Github : https://github.com/uqlibrary/uqlibrary-reusable-components/tree/master/applications/primo2/view_package
- [University of Sussex Library](https://sussex-primo.hosted.exlibrisgroup.com/primo-explore/search?vid=44SUS_VU1&sortby=rank&lang=en_US)
- [Charles Sturt University Library](https://primo.csu.edu.au/discovery/search?vid=61CSU_INST:61CSU&lang=en)
- [Harvard Libraries](https://hollis.harvard.edu/primo-explore/search?vid=HVD2)
	- dépôt Github : https://github.com/cbaksik/HVD2
- Alliance Primo Customization Standing Group :
	Github : https://github.com/alliance-pcsg
- [University of Otago Library](https://otago.hosted.exlibrisgroup.com/primo-explore/search?&vid=DUNEDIN)	
	- https://github.com/Brewstmerr/DUNEDIN-view


- **Voir aussi** : https://docs.google.com/document/d/1JqSNx6eDe_sNPz9K8sZtDRhQWbzyaQz0mpLWqmqOhk0/edit#
- [ELUNA : List of Primo Sites with New UI](https://el-una.org/working-groups/primo/primo-sites/)
