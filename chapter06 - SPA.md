chapter06 - SPA
===============

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter06.html
	app/
		06/
			app.js
			views/
				home.html
				about.html
				employee.html
				employee_detail.html

### Single Page Application

**เพิ่ม**ไฟล์ *chapter06.html*

	<body>
		<a href="#/">Home</a> | <a href="#/about">About</a>

		<hr>

		<div ng-view></div>

		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-route.min.js"></script>

		<script src="app/06/app.js"></script>
	</body>

**เพิ่ม**ไฟล์ *app/06/views/home.html*

	<h3>Home</h3>

	<p>{{ controllerName }}</p>

**เพิ่ม**ไฟล์ *app/06/views/about.html*

	<h3>About</h3>

	<p>{{ controllerName }}</p>

**เพิ่ม**ไฟล์ *app/06/app.js*

	var app = angular.module('app', ['ngRoute']);

**แก้ไข**ไฟล์ *app/06/app.js* โดย**เพิ่ม** `HomeController` และ `AboutController`

	app.controller('HomeController', function($scope) {
		$scope.controllerName = 'This is HomeController';
	});

	app.controller('AboutController', function($scope) {
		$scope.controllerName = 'This is AboutController';
	});

**แก้ไข**ไฟล์ *app/06/app.js* โดย**เพิ่ม** `config()`

	app.config(function($routeProvider) {
		$routeProvider
			.when('/', {
				controller: 'HomeController',
				templateUrl: 'app/06/views/home.html'
			})
			.when('/about', {
				controller: 'AboutController',
				templateUrl: 'app/06/views/about.html'
			})
			.otherwise({
				redirectTo: '/'
			})
	});

### Quiz 06-1

ทำการเพิ่ม

1. Route สำหรับ `/employee`
2. `EmployeeController` เพื่อใช้ `$http` ดึงข้อมูลจากไฟล์ *http://api-slim.tutor4dev.com/employees.json* และ นำมาเก็บไว้ที่ตัวแปร `$scope.employees`
2. ไฟล์ *app/06/views/employee.html* โดยทำการแสดงข้อมูลของ Employee จาก `$scope.employees`

### Route แบบมี Parameter

**แก้ไข**ไฟล์ *app/06/app.js* โดย**เพิ่ม** Route สำหรับ `/employee/:id`

	.when('/employee/:id', {
		controller: 'EmployeeDetailController',
		templateUrl: 'app/06/views/employee_detail.html'
	})

**แก้ไข**ไฟล์ *app/06/app.js* โดย**เพิ่ม** `EmployeeDetailController`

	app.controller('EmployeeDetailController', function($scope, $routeParams, $http) {

		$scope.id = $routeParams.id;

		$scope.query = {
			emp_no: $scope.id
		};

		$http.get('employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

**เพิ่ม**ไฟล์ *app/06/views/employee_detail.html*

	<h3>Employee Detail</h3>

	Employee ID: {{ id }}

	{{ query }}

	<p ng-repeat="e in employees | filter: query">
		Name: {{ e.first_name + ' ' + e.last_name }}
		<br>
		Gender: {{ e.gender }}
	</p>

### Quiz 06-2

ทำการแก้ไข App ส่วนที่เหลือเพื่อให้รองรับหน้า Employee Detail โดยการกด Link จากหน้า Employee