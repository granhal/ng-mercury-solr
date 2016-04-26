# mercury
Solr wrapper for Angular

##Requisites:
⋅⋅⋅ Solr 4.7.0 - http://lucene.apache.org/solr/
⋅⋅⋅ Angular 1.0.8+ - https://angularjs.org/

##How to use:
    1. Install apache solr in your server
    2. Install angular in your client

##Set in your config:

    ```javascript
    yourApp.config(function(MercuryProvider) {
        MercuryProvider.setEndpoint('http://url-your-solr/solr/core/');
    });
    ```
##In your search method insert (is a example):

    ```javascript
        Mercury.search({ // in this object, insert your solr query!!
                'q.op': 'AND',
                rows: $scope.pageSize,
                start : (($scope.currentPage)? ($scope.currentPage-1) : 0) * $scope.pageSize,
                fq: 'speStateId:1 OR speStateId:4',
                fl: '*, score',
                q: $scope.searchCarrousel ? $scope.searchCarrousel : ($scope.search) ? $scope.search: '*',
                pt: (UserLocalService.getLocation()) ? UserLocalService.getLocation().lat + "," + UserLocalService.getLocation().lon : ''
            })
            .then(function (callback){ // resolve promise and set variable for view!!
                console.log("resolve mercury:");
                console.log(callback);
                $scope.totalResults = callback.data.response.numFound;
                $scope.searchOfferResult = callback.data.response.docs;
                $scope.totalPages = Math.ceil($scope.totalResults / $scope.pageSize);

            }, function(err){ // error for promise!!
                console.log(err);
            });

    ```

is easy! :D

##TODO:
    - Parse to Angular 2
    - Insert PUT and DELETE method for Solr files


###Licence:
Open source
 * @license MIT License, http://www.opensource.org/licenses/MIT
