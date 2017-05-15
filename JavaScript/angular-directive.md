```
<html ng-app='app'>
    <body>
        <hello>
        	<br/>
            <span>原始的内容，</span><br/>
            <span>还会在这里。</span>
        </hello>
    </body>

    <script src="angular-1.5.5/angular.min.js"></script>
    <script src="HelloDirective.js"></script>
</html>

//HelloDirective.js
var appModule = angular.module('app', []);
appModule.directive('hello', function() {
    return {
        restrict: 'E',
        template: '<div>Hi there<span ng-transclude></span></div>',
        transclude: true, // keep original content of <hello> tag and wrap it in ng-transclude
        replace: true // replace <hello> tag with its content
    };
});
 
```

***
```
<html ng-app='app'>
	<body ng-controller='MyController'>
        <div ng-repeat='thing in things'>
            {{thing}}.<hello></hello>
        </div>
    </body>

    <script src="angular-1.5.5/angular.min.js"></script>
    <script src="HelloDirective.js"></script>
</html>

// HelloDirective.js
var appModule = angular.module('app', []);
appModule.directive('hello', function() {
    return {
        restrict: 'E',
        template: '<span>Hi there</span>',
        replace: true
    };
});
appModule.controller('MyController',function($scope) {
    $scope.things = [1,2,3,4,5,6];
});
 
//webpage
1.Hi there
2.Hi there
3.Hi there
4.Hi there
5.Hi there
6.Hi there

```


## '<expander class='expander' expander-title='title' expander-text='text' expander-count='10'>'
