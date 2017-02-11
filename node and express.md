#### The concept of middleware:  
a middleware is function to deal with request and response of a path. It can grab data from resources or add attributes to response such as status code, headers, cookies or other properties.  

use() method maps path with middleware by app.use(PATH, middleware).  It makes middlewares works as assebly pipeline.

next function is only usefull when both url and same method are same. It is used to pass the request and response object to next middleware.  

#### The conecpt of routing:  
There are two types router in the tinyUrl project, the express.Router and angularjs $routeProvider. 
example of express.Router
```JavaScript
var express = require('express');
var app = express();
var useragent = require('useragent')

var indexRouter = express.Router();
var apiRouter = express.Router();
var redirectRouter = express.Router();

// indexRouter
indexRouter.get('/', function(req, res) {
	res.end('this is the idnex.html');
});

// apiRouter
apiRouter.post('/urls', function(req, res) {
	console.log('received your post request');
});

apiRouter.get('/urls/:shortUrl', function(req, res) {
	res.end('this is the information for ' + req.params.shortUrl);
});

apiRouter.get('/urls/:shortUrl/:info', function(req, res) {
	res.end('this is the information for ' + req.params.shortUrl + ' of ' + req.params.info);
});

// redirectRouter
redirectRouter.get('/', function(req, res) {
	var shortUrl = req.originalUrl.slice(1);
	res.end('you will be redirected to the longUrl of ' +  shortUrl);
});

// mont indexRouter to '/'
app.use('/', indexRouter);
// mont apiRouter to '/api/v1'
app.use('/api/v1', apiRouter);
// mont redirectRouter to '/:shortUrl'
app.use('/:shortUrl', redirectRouter);

// catch all invalid url
app.use('*', function(req, res) {
	res.end('404 NOT FOUND');
});

app.listen(3000, function() {
	console.log("listen on port 3000");
});
```
the example of angular $routeProvider  
```javascript
var app = angular.module('tinyurlApp',['ngRoute', 'ngResource', 'chart.js']);
app.config(function($routeProvider) {
	//dependencies injection, call for routeProvider object
	$routeProvider.when('/', {
		// set template and controller
		templateUrl: '/public/views/get_tinyUrl.html',
		controller: 'homeController'
	}).when('/urls/:shortUrl', {
        templateUrl: '/public/views/url.html',
        controller: 'urlController'
    })
});
```  
I was confused by those two routers. The difference of two routers:  
1. express.Router is backend on server, angular $routeProvider is on frontend webpage.
2. express.Router is to map paths to request handlers, while angular $routeProvider is to render templates and controllers.  
3. to get data model from resources, controllers will make $http request in single webpage.    

**Note:** the very reason that why we use angular js is to make single webpage. We set several specific vies in single page and fill the view with templates and controllers and pull data from resources via in-page  $http request.

