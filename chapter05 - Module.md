chapter05 - Module
==================

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter05.html
	app/
		05/
			app.js
			employee.js

### ใช้งาน Module `ngAnimate`

**เพิ่ม**ไฟล์ *app/05/app.js*

	var app = angular.module('app', ['ngAnimate']);

	app.controller('EmployeeController', function($scope, $http) {

		$http.get('http://api-slim.tutor4dev.com/employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

**เพิ่ม**ไฟล์ *chapter05.html*

	<!DOCTYPE html>
	<html ng-app="app">
	<head>
		<title>AngularJS - Course</title>
		<style>
			.ng-enter {
				transition:0.75s;
				opacity:0;
			}

			.ng-enter-active {
				opacity:1;
			}

			.ng-leave {
				transition:0.75s;
				opacity:1;
			}

			.ng-leave-active {
				opacity:0;
			}
		</style>
	</head>
	<body>

		<div ng-controller="EmployeeController">
			<input type="text" ng-model="query">
			<p ng-repeat="e in employees | filter: query">
				{{ e.first_name + ' ' + e.last_name }}
			</p>
		</div>

		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-animate.min.js"></script>

		<script src="app/05/app.js"></script>
	</body>
	</html>

### Modularized AngularJS Application

**แก้ไข**ไฟล์ *app/05/app.js*

	var app = angular.module('app', ['employeeModule']);

**เพิ่ม**ไฟล์ *app/05/employee.js* โดย**ย้าย** `EmployeeController` จากไฟล์ *app/05/app.js* มายังไฟล์นี้แทน

	var emp = angular.module('employeeModule', []);

	emp.controller('EmployeeController', function($scope, $http) {

		$http.get('http://api-slim.tutor4dev.com/employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

**แก้ไข**ไฟล์ *chapter05.html* โดย**เพิ่ม**

	<script src="app/05/employee.js"></script>

### Quiz 05-1

ทำการย้าย `EmployeeController` ไปไว้กับ Module ใหม่ชื่อ `employeeControllerModule` โดยจัดเก็บในไฟล์ชื่อ *app/05/employeeController.js*

Hints:

- `angular.module('employeeModule', ['employeeControllerModule'])`




