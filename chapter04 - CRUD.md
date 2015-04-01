chapter04 - CRUD
================

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter04.html
	app/
		04/
			app.js

### พัฒนา CRUD ด้วย AngularJS

**เพิ่ม**ไฟล์ *app/04/app.js*

	var app = angular.module('app', []);

	app.controller('EmployeeController', function($scope, $http) {

		$http.get('http://api-slim.tutor4dev.com/employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

**เพิ่ม**ไฟล์ *chapter04.html*

	<!DOCTYPE html>
	<html ng-app="app">
	<head>
		<title>AngularJS - Course</title>
	</head>

	<body>

		<p ng-repeat="e in employees">
			{{ e.first_name }}
		</p>

		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
		<script src="app/04/app.js"></script>

	</body>
	</html>

### ลบ Employee คนสุดท้ายโดยใช้ JavaScript `pop()` Function

**แก้ไข**ไฟล์ *app/04/app.js* โดย**เพิ่ม** `$scope.deleteEmployee()` ให้กับ `EmployeeController`

	$scope.deleteEmployee = function() {
		$scope.employees.pop();
	}

**แก้ไข**ไฟล์ *chapter04.html* โดย**เพิ่ม**

	<button ng-click="deleteEmployee()">Delete</button>

### ลบ Employee โดยใช้ JavaScript `splice()` Function

**แก้ไข**ไฟล์ *app/04/app.js* โดย**แก้ไข** `$scope.deleteEmployee()`

	$scope.deleteEmployee = function(index) {
		$scope.employees.splice(index, 1);
	}

**แก้ไข**ไฟล์ *chapter04.html* โดย**แก้ไข**

	<p ng-repeat="e in employees">

		{{ e.first_name }}

		<button ng-click="deleteEmployee($index)">Delete</button>

	</p>

### Quiz 04-1

- เขียน Code เพื่อเพิ่ม Employee โดยใช้ JavaScript `push()` Function

Hint

	Employee #: <input type="text" ng-model="employee.first_name">

	$scope.employees.push({
		first_name: $scope.employee.first_name
	});

### แก้ไข Employee

**แก้ไข**ไฟล์ *app/04/app.js* โดย**เพิ่ม** `$scope.toggleEditMode()`

	$scope.toggleEditMode = function() {
		$scope.editMode = !$scope.editMode;
	}

**แก้ไข**ไฟล์ *chapter04.html* โดย**แก้ไข**

	<p ng-repeat="e in employees">
		<span ng-show="!edit">
			{{ $index + 1 + ' ' + e.first_name }}
			<button ng-show="!editMode" ng-click="edit=true;toggleEditMode()">Edit</button>
		</span>

		<span ng-show="edit">
			<input type="text" ng-model="e.first_name">
			<button ng-click="edit=false;toggleEditMode()">Save</button>
		</span>
	</p>
	