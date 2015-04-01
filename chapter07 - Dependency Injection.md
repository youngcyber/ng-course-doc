chapter07 - Dependency Injection
================================

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter07.html
	app/
		07/
			app.js

### Dependency Injection

	app.controller('HomeController', function($scope, xxx) {
	});

**เพิ่ม**ไฟล์ *chapter07.html*

	<body>
		<h3>ng-course</h3>

		<div ng-controller="HomeController"></div>

		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
		<script src="app/07/app.js"></script>
	</body>

**เพิ่ม**ไฟล์ *app/07/app.js*

	var app = angular.module('app', []);

### ใช้ `value()` Service

**แก้ไข**ไฟล์ *app/07/app.js* โดย**เพิ่ม**

	app.value('accessToken', 'xxx');

	app.value('currentUser', {
		name: 'admin'
	});

	app.value('helloValue', function() {
		return 'Hello, Value';
	});

**แก้ไข**ไฟล์ *app/07/app.js* โดย**เพิ่ม** `HomeController`

	app.controller('HomeController', function(accessToken, currentUser, helloValue) {

		console.log(accessToken);
		accessToken = 'yyy';
		console.log(accessToken);

		currentUser.name = 'kongthap';
		console.log(currentUser.name);

		console.log(helloValue());

	});

### ใช้ `constant()` Service

**แก้ไข**ไฟล์ *app/07/app.js* โดย**เพิ่ม**

	app.constant('apiUrl', '//api-slim.tutor4dev.com');

	app.constant('config', {
		xxx: 'x',
		yyy: 'y'
	});

### Quiz 07-1

เขียน `employeeValue` แบบ Function ที่จะทำการคืนค่ารายชื่อของ Employee

	[
		{
			"emp_no":"10001",
			"birth_date":"1953-09-02",
			"first_name":"Georgi",
			"last_name":"Facello",
			"gender":"M",
			"hire_date":"1986-06-26"
		},
		{
			"emp_no":"10002",
			"birth_date":"1964-06-02",
			"first_name":"Bezalel",
			"last_name":"Simmel",
			"gender":"F",
			"hire_date":"1985-11-21"
		}
	];

Hints

- `$scope.employees = employeeValue()`

### ใช้งาน `service()` และ `factory()` Service

**แก้ไข**ไฟล์ *app/07/app.js* โดย**เพิ่ม**

	app.service('helloService', function() {
		this.hello = function() {
			return 'Hello, Service';
		}
	});

	app.factory('helloFactory', function() {
		return {
			hello: function() {
				return 'Hello, Factory';
			}
		};
	});

**แก้ไข**ไฟล์ *app/07/app.js* โดย**แก้ไข** `HomeController`

	app.controller('HomeController', function(helloService, helloFactory) {

		console.log(helloService.hello());
		console.log(helloFactory.hello());

	});

### Quiz 07-2

เขียน `employeeFactory` โดยมี Function ชื่อ `getEmployees()` ที่จะทำการคืนค่ารายชื่อของ Employee

	[
		{
			"emp_no":"10001",
			"birth_date":"1953-09-02",
			"first_name":"Georgi",
			"last_name":"Facello",
			"gender":"M",
			"hire_date":"1986-06-26"
		},
		{
			"emp_no":"10002",
			"birth_date":"1964-06-02",
			"first_name":"Bezalel",
			"last_name":"Simmel",
			"gender":"F",
			"hire_date":"1985-11-21"
		}
	];

Hints

- `$scope.employees = employeeFactory.getEmployees()`

### `provider()` Service

**แก้ไข**ไฟล์ *app/07/app.js* โดย**เพิ่ม**

	app.provider('hello', function() {
		var text = 'xxx';

		return {
			setText: function(value) {
				text = value;
			},
			$get: function() {
				return {
					hello: function() {
						return 'Hello, Provider: ' + text
					}
				}
			}
		}
	});

**แก้ไข**ไฟล์ *app/07/app.js* โดย**แก้ไข** `HomeController`

	app.controller('HomeController', function(helloProvider) {
		console.log(helloProvider.hello());
	});

ใช้ `config()` เพื่อ Config `helloProvider`

	app.config(function(helloProvider) {
		helloProvider.setText('yyy');
	});

### Quiz 07-3

ทำการแยก Service, Factory และ Provider ไว้ใน Module ของตนเอง

Hints

- `angular.module('app.service', []);`
- `angular.module('app.factory', []);`
- `angular.module('app.provider', []);`
- `angular.module('app', ['app.service', ...]);`

### Quiz 07-4

ทำการแยก Service, Factory และ Provider ไว้ในไฟล์ของตนเอง

Hints

	chapter07.html
	app/
		07/
			app.js
			service.js
			factory.js
			provider.js


	