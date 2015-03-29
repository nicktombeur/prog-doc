#Angular

##Module

[Developer Guide](https://docs.angularjs.org/guide/module)

*Example:*

```javascript
var app = angular.module('app', []);
```

```html
<!DOCTYPE html>
<html ng-app="app">
	<head>
		<script type="text/javascript" src="angular.min.js" defer>
		<script type="text/javascript" src="app.js" defer>
	</head>
	<body>
	</body>
</html>
```

##Controller

[Developer Guide](https://docs.angularjs.org/guide/controller)

*Example:*

```javascript
(function() {
	var app = angular.module('app',  []);

	app.controller('ExampleController', function() {
		this.hello = 'Hello World!';
	});
})();
```

```html
<body>
	<div ng-controller="ExampleController as exampleCtrl">
		<p>{{exampleCtrl.hello}}</p>
	</div>
```

Name of the controller should always:
- Be in capital case
- End with the word 'Controller'

##Built-in Directives

[Developer Guide](https://docs.angularjs.org/api/ng/directive)

*Example:*

```html
<p ng-show="exampleCtrl.message.visible">{{exampleCtrl.message.text}}</p>
```

```javascript
var message = {
	text: 'Hello world!',
	visible: true
}
```

##Filters

[Developer Guide](https://docs.angularjs.org/guide/filter)

*Example:*

Format into currency.
```html
<p>{{product.price | currency}}</p>
```

##Forms

[Developer Guide](https://docs.angularjs.org/guide/forms)

*Example:*

```html
<form name="userForm" ng-submit="userForm.$valid && exampleCtrl.add(user)" novalidate>
	<input type="text" ng-model="exampleCtrl.user.name" required />
	<input type="submit" value="Submit" />
</form>
```

```javascript
app.controller('ExampleController', function() {
	this.user = {};

	this.add = function(user) {
		// add to DB
		this.user = {};
	}
})
```

Styling form validation:
https://docs.angularjs.org/guide/css-styling

##Directives

[Developer Guide](https://docs.angularjs.org/guide/directive)

To prevent code duplication you can use ng-include.
But it's better to use a custom Directive.

Dash in HTML translates to camelCase in JavaScript.

Examples:
- An attribute directive
	- ```html <h3 example-title></h3>```
- An element directive
	- ```html <h3><example-title></example-title></h3>```

##Dependencies

[Developer Guide](https://docs.angularjs.org/guide/di)

Always use the array syntax for DI!

*Example:*

```javascript
(function() {
	var app = angular.module('example', ['example-store']);
})();
```

```javascript
(function() {
	var app = angular.module('example-store', []);
})();
```

##Built-in Services

[Developer Guide](https://docs.angularjs.org/api/ng/service)

All built-in Services start with a $ sign.

$http Service makes an async request to a server.

Examples:
- $http({ method: 'GET', url: '/examples'});
- $http.get('/examples');

Both return a Promise object with .succes() and .error()

More soon...
