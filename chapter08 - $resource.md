chapter08 $resource
===================

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter08.html
	app/
		08/
			app.js

### ReSTful URI

- GET -> *http://api-slim.tutor4dev/employee*
- GET -> *http://api-slim.tutor4dev/employee/:id*
- POST -> *http://api-slim.tutor4dev/employee*
- PUT -> *http://api-slim.tutor4dev/employee/:id*
- DELETE -> *http://api-slim.tutor4dev/employee/:id*

### ใช้งาน Module `ngResource`

**เพิ่ม**ไฟล์ *app/08/app.js*

	var app = angular.module('app', ['ngResource']);

	app.constant('apiUrl', '//api-slim.tutor4dev.com');

**แก้ไข**ไฟล์ *app/08/app.js* โดย**เพิ่ม** `EmployeeFactory`

	app.factory('EmployeeFactory', function($resource, apiUrl) {

		return $resource(apiUrl + '/employee/:id');

	});

**เพิ่ม**ไฟล์ *chapter08.html*

	<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
	<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-resource.min.js"></script>
	<script src="app/08/app.js"></script>

### ใช้ `$resource` แสดง List ของ Employee

**แก้ไข**ไฟล์ *app/08/app.js* โดย**เพิ่ม** `ListController`

	app.controller('ListController', function($scope, EmployeeFactory) {

		$scope.employees = EmployeeFactory.query();
	});

**แก้ไข**ไฟล์ *chapter08.html* โดย**เพิ่ม**

	<p ng-repeat="e in employees">
		{{ e.emp_no + ': ' + e.first_name + ' ' + e.last_name }}
	</p>

### ใช้ `$resource` แสดง Employee ตามเงื่อนไข

**แก้ไข**ไฟล์ *app/08/app.js* โดย**เพิ่ม** `ShowController`

	app.controller('ShowController', function($scope, EmployeeFactory) {

		$scope.showEmployee = function() {
			$scope.employee = EmployeeFactory.get({ id: $scope.emp_no });
		}
	});

**แก้ไข**ไฟล์ *chapter08.html* โดย**เพิ่ม**

	<hr>

	<div ng-controller="ShowController">
		Employee #: <input type="text" ng-model="emp_no">
		<br>
		<input type="button" ng-click="showEmployee()" value="Show Employee">
		<p>{{ employee.emp_no + ' ' + employee.first_name + ' ' + employee.last_name }}</p>
	</div>

### ใช้ `$resource` เพิ่ม New Employee

**แก้ไข**ไฟล์ *app/08/app.js* โดย**เพิ่ม** `CreateController`

	app.controller('CreateController', function($scope, EmployeeFactory) {

		$scope.createEmployee = function() {
			var postData = { emp_no: $scope.employee.emp_no, first_name: $scope.employee.first_name, last_name: $scope.employee.last_name };

			EmployeeFactory.save(postData);
		}
	});

**แก้ไข**ไฟล์ *chapter08.html* โดย**เพิ่ม**

	<hr>

	<div ng-controller="CreateController">
		Employee:
		<input type="text" ng-model="employee.emp_no" placeholder="Employee #">
		<input type="text" ng-model="employee.first_name" placeholder="First Name">
		<input type="text" ng-model="employee.last_name" placeholder="Last Name">
		<br>
		<input type="button" ng-click="createEmployee()" value="Create">
	</div>

### ใช้ `$resource` ลบ Employee

**แก้ไข**ไฟล์ *app/08/app.js* โดย**แก้ไข** `EmployeeFactory` และ **เพิ่ม** `DeleteController`

	app.factory('EmployeeFactory', function($resource, apiUrl) {

		return $resource(
			apiUrl + '/resource/employee/:id', {}, {
				delete: {
					headers: { 'X-HTTP-Method-Override': 'DELETE' }
				}
			}
		);
	});

	app.controller('DeleteController', function($scope, EmployeeFactory) {
		$scope.deleteEmployee = function() {
			EmployeeFactory.delete({ id: $scope.emp_no });
		}
	});

**แก้ไข**ไฟล์ *chapter08.html* โดย**เพิ่ม**

	<hr>

	<div ng-controller="DeleteController">
		Employee #: <input type="text" ng-model="emp_no">
		<br>
		<input type="button" ng-click="deleteEmployee()" value="Delete">
	</div>

### ใช้ `$resource` แก้ไข Employee

**แก้ไข**ไฟล์ *app/08/app.js* โดย**แก้ไข** `EmployeeFactory` และ **เพิ่ม** `UpdateController`

	app.factory('EmployeeFactory', function($resource, apiUrl) {

		return $resource(
			apiUrl + '/resource/employee/:id', {}, {
				update: {
					method: 'PUT',
					isArray: false,
					params: { id: '@id' },
					headers: { 'X-HTTP-Method-Override': 'PUT' }
				}
			}
		);
	});

	app.controller('UpdateController', function($scope, EmployeeFactory) {
		$scope.updateEmployee = function() {
			var postData = { emp_no: $scope.employee.emp_no, first_name: $scope.employee.first_name, last_name: $scope.employee.last_name };
			EmployeeFactory.update({ id: $scope.old_emp_no	}, postData);
		}
	});

**แก้ไข**ไฟล์ *chapter08.html* โดย**เพิ่ม**

	<div ng-controller="UpdateController">
		Old Employee #: <input type="text" ng-model="old_emp_no">
		<br>
		Employee:
		<input type="text" ng-model="employee.emp_no" placeholder="Employee #">
		<input type="text" ng-model="employee.first_name" placeholder="First Name">
		<input type="text" ng-model="employee.last_name" placeholder="Last Name">
		<br>
		<input type="button" ng-click="updateEmployee()" value="Update">
	</div>
