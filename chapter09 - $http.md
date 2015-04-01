chapter09 - $http
=================

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter09.html
	app/
		09/
			app.js
			views/
				employee.html
				employee_detail.html
				employee_create.html
				home.html

### `$http` API

	$http({
		method: 'GET',
		url: 'http://api-php.tutor4dev.com/select.php',
		params: { 'emp_no': 101 }
	});

	$http({
		method: 'POST',
		url: 'http://api-php.tutor4dev.com/insert.php',
		data: {
			'emp_no': 101,
			'first_name': 'James',
			'last_name': 'Bond'
		}
	});

### `$http` Shorthand

	$http.get('http://api-php.tutor4dev.com/select.php?emp_no=101');

	$http.post('http://api-php.tutor4dev.com/select.php?emp_no=101', {
		'emp_no': 101,
		'first_name': 'James',
		'last_name': 'Bond'
	});
				
### ใช้งาน Promise ด้วย `$q`

	app.factory('employeeFactory', function($http, $q) {
		var defer = $q.defer();

		$http.get(url)
			.success(function(data) {
				defer.resolve(data);
			});

		return defer.promise;
	});

### URI

- *GET* -> *http://api-php.tutor4dev.com/select.php*
- *GET* -> *http://api-php.tutor4dev.com/select.php?emp_no=101*
- *POST* -> *http://api-php.tutor4dev.com/insert.php*
- *POST* -> *http://api-php.tutor4dev.com/update.php*
- *POST* -> *http://api-php.tutor4dev.com/delete.php*

### Project Setup

**เพิ่ม**ไฟล์ *app/09/app.js*

	var app = angular.module('app', ['ngRoute']);

	app.constant('apiUrl', '//api-php.tutor4dev.com')

	app.config(function($routeProvider) {
		$routeProvider
			.otherwise({
				redirectTo: '/'
			})
	});

**เพิ่ม**ไฟล์ *chapter09.html*

	<a href="#/">Home</a> | <a href="#/employee">Employee</a> | <a href="#/create">Create</a>

	<div ng-view></div>

	<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
	<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-route.min.js"></script>
	<script src="app/09/app.js"></script>

### หน้า Home Page

**แก้ไข**ไฟล์ *app/09/app.js*

	.when('/', {
		controller: 'HomeController',
		templateUrl: 'app/09/views/home.html'
	})

	app.controller('HomeController', function() {});

**เพิ่ม**ไฟล์ *app/09/views/home.html*

	<h3>Home</h3>

### หน้า Employee

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `employeeFactory`

	app.factory('employeeFactory', function($http, $q, apiUrl) {
		return {

			listEmployees: function() {
				var defer = $q.defer();

				$http.get(apiUrl + '/select.php')
					.success(function(data) {
						defer.resolve(data);
					})
					.error(function() {
						defer.reject('Error ...');
					});

				return defer.promise;
			}
		};
	});

	app.controller('EmployeeController', function($scope, employeeFactory) {

		$scope.employees = [];

		employeeFactory.listEmployees()
			.then(function(data) {
				$scope.employees = data;
			}, function() {
				console.log('Error ...');
			});
	});

**เพิ่ม**ไฟล์ *app/views/employee.html*

	<h3>Employee</h3>

	<div ng-controller="EmployeeController">
		<p ng-repeat="e in employees">
			<a href="#/employee/{{e.emp_no}}">{{ e.emp_no }}</a>
			{{ e.first_name + ' ' + e.last_name }}
		</p>
	</div>

### Delete Employee

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `deleteEmployee` ให้กับ `EmployeeFactory`

	deleteEmployee: function(id) {
		var defer = $q.defer();

		$http.post(apiUrl + '/delete.php', { 'emp_no': id })
			.success(function(data) {
				defer.resolve(data);
			})
			.error(function() {
				defer.reject('Error ...');
			});

		return defer.promise;
	}

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `deleteEmployee` ให้กับ `EmployeeController`

	$scope.deleteEmployee = function(id) {
		employeeFactory.deleteEmployee(id)
			.then(function() {
				console.log('Success');
			});
	}

### หน้า Employee Detail

**แก้ไข**ไฟล์ *app/09/app.js* โดยเพิ่ม `$routeProvider`

	.when('/employee/:id', {
		controller: 'EmployeeDetailController',
		templateUrl: 'app/09/views/employee_detail.html'
	})

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `showEmployee` ให้กับ `EmployeeFactory`

	showEmployee: function(id) {

		var defer = $q.defer();

		$http.get(apiUrl + '/select.php?emp_no=' + id, { 'emp_no': id })
			.success(function(data) {
				defer.resolve(data);
			})
			.error(function() {
				defer.reject('Error ...');
			});

		return defer.promise;
	}

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `EmployeeDetailController`

	app.controller('EmployeeDetailController', function($scope, $routeParams, employeeFactory) {
		$scope.employee = {};

		employeeFactory.showEmployee($routeParams.id)
			.then(function(data) {
				$scope.employee = data;
				$scope.employee.old_emp_no = $scope.employee.emp_no;
			});
	});

**เพิ่ม**ไฟล์ *app/views/employee_detail.html*

	<h3>Employee Detail</h3>

	<p>Employee #<input type="text" ng-model="employee.emp_no"></p>
	<p>First Name<input type="text" ng-model="employee.first_name"></p>
	<p>Last Name<input type="text" ng-model="employee.last_name"></p>

### Update Employee

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `updateEmployee` ให้กับ `EmployeeFactory`

	updateEmployee: function(employee) {

		var defer = $q.defer();

		$http.post(apiUrl + '/update.php', employee)
			.success(function(data) {
				defer.resolve(data);
			})
			.error(function() {
				defer.reject('Error ...');
			});

		return defer.promise;
	}

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `updateEmployee` ให้กับ `EmployeeDetailController`

	app.controller('EmployeeDetailController',
		function($scope, $routeParams, employeeFactory) {

		$scope.updateEmployee = function() {
			employeeFactory.updateEmployee($scope.employee);
		}
	});

**แก้ไข**ไฟล์ *app/views/employee_detail.html*

	<p><input type="button" value="Update" ng-click="updateEmployee()"></p>

### หน้า Create Employee

**แก้ไข**ไฟล์ *app/09/app.js* โดยเพิ่ม `$routeProvider`

	.when('/create', {
		controller: 'EmployeeCreateController',
		templateUrl: 'app/09/views/employee_create.html'
	})

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `createEmployee` ให้กับ `EmployeeFactory`

	createEmployee: function(employee) {

		var defer = $q.defer();

		$http.post(apiUrl + '/insert.php', employee)
			.success(function(data) {
				defer.resolve(data);
			})
			.error(function() {
				defer.reject('Error ...');
			});

		return defer.promise;
	}

**แก้ไข**ไฟล์ *app/09/app.js* โดย**เพิ่ม** `EmployeeCreateController`

	app.controller('EmployeeCreateController', function($scope, $location, employeeFactory) {
		$scope.createEmployee = function() {
			employeeFactory.createEmployee($scope.employee)
				.then(function() {
					$location.path('/employee');
				});
		}
	});

**เพิ่ม**ไฟล์ *app/views/employee_create.html*

	<h3>New Employee</h3>

	<p>Employee #<input type="text" ng-model="employee.emp_no"></p>
	<p>First Name<input type="text" ng-model="employee.first_name"></p>
	<p>Last Name<input type="text" ng-model="employee.last_name"></p>

	<p><input type="button" value="Save" ng-click="createEmployee()"></p>