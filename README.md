# ng-mercury-solr
Solr wrapper for Angular
Mercury is an AngularJS module, that enables simple querying and faceting/filtering of Solr indexes.
Provides a search service and a companion directive that can be used in any Angularjs project.

Mercury is inspired by Solstice and Restangular - Service for Rest API.

##Requisites:
* Solr 4.7.0+ - http://lucene.apache.org/solr/
* Angular 1.0.8+ - https://angularjs.org/

##How to use:
* Install apache solr in your server
* Install angular in your client
* call mercury.js or mercury.min.js after angular
```html
<script type="text/javascript" src="js/angular.min.js"></script>
<script type="text/javascript" src="js/mercury.min.js"></script>
```
###Inyect dependencies in module
```javascript
var yourApp = angular.module('yourApp', ['mercury']);
```
###Set end-point in your config:
```javascript
yourApp.config(function(MercuryProvider) {
    MercuryProvider.setEndpoint('http://url-your-solr/solr/core/');
});
```
###In your controller insert (is a example):
```javascript
yourApp.controller('searchCtrl', ['Mercury',
	function(Mercury) {
	// your code here...
	}
]);
```
#### In "//your code here" inside the method, insert, for example:
```javascript
    Mercury.search({
	    'q.op': 'AND',
	    rows: $scope.pageSize,
	    start : ((pag) ? pag : 0) * $scope.pageSize,
	    q: ($scope.search) ? $scope.search :  "*" ,
	    facet: true,
	    'facet.limit' : 4,
	    'facet.mincount' : 1,
	    'f.topics.facet.limit' : 50
        })
        .then(function (callback){
            $scope.totalResults = callback.data.response.numFound;
            $scope.searchOfferResult = callback.data.response.docs;
            $scope.totalPages = Math.ceil($scope.totalResults / $scope.pageSize);

        }, function(err){
            console.log(err);
        });
};
```

is easy! :D

##TODO:
* Parse to Angular 2
* Caching with $cacheFactory for history calls or others features
* Insert PUT and DELETE and more features for Solr files
* Add multiple end-points to cores
* Make and documented manual for the directive in HTML

###Licence:
Open source
 * @license MIT License, http://www.opensource.org/licenses/MIT
