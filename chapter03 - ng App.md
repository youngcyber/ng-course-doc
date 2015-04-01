chapter03 - ng App
==================

### โครงสร้างการจัดเก็บไฟล์ใน Chapter นี้

	chapter03.html
	app/
		03/
			app.js

### ใช้งาน AngularJS Application

**เพิ่ม**ไฟล์ *app/03/app.js*

	var app = angular.module('app', []);

**เพิ่ม**ไฟล์ *chapter03.html*

	<!DOCTYPE html>
	<html ng-app="app">
	<head>
		<title>AngularJS - Course</title>
	</head>

	<body>

		<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
		<script src="app/03/app.js"></script>

	</body>
	</html>

### ใช้งาน Controller

**แก้ไข**ไฟล์ *app/03/app.js* โดย**เพิ่ม**

	app.controller('BasicController', function() {

		console.log('Hello, World');

	});

**แก้ไข**ไฟล์ *chapter03.html* โดย**เพิ่ม**

	<div ng-controller="BasicController">
	</div>

### ใช้งาน `$scope`

**แก้ไข**ไฟล์ *app/03/app.js* โดย**แก้ไข**

	app.controller('BasicController', function($scope) {

		$scope.name = 'AngularJS';

		$scope.hello = function() {
			console.log('Hello, ' + $scope.name);
		}

	});

**แก้ไข**ไฟล์ *chapter03.html* โดย**แก้ไข**

	<div ng-controller="BasicController">

		{{ name }}
		<br>
		<button ng-click="hello()">Hello</button>

	</div>

### Quiz 03-1

เขียน Code เพื่อคำนวนผล *Price x Quantity* เมื่อกดปุ่ม *Calculate*

	Price: <input type="text"><br>
	Quantity: <input type="text"><br>
	
	<button>Calculate</button><br>
	
	<p>Result:</p>

### ใช้งาน `ng-repeat`

**แก้ไข**ไฟล์ *app/03/app.js* โดย**เพิ่ม**

	app.controller('EmployeeController', function($scope) {
	});

**แก้ไข**ไฟล์ *app/03/app.js* โดย**แทรก** `$scope.employees` ให้กับ `EmployeeController`

	$scope.employees = [
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
		},
		{
			"emp_no":"10003",
			"birth_date":"1959-12-03",
			"first_name":"Parto",
			"last_name":"Bamford",
			"gender":"M",
			"hire_date":"1986-08-28"
		},
		{
			"emp_no":"10004",
			"birth_date":"1954-05-01",
			"first_name":"Chirstian",
			"last_name":"Koblick",
			"gender":"M",
			"hire_date":"1986-12-01"
		},
		{
			"emp_no":"10005",
			"birth_date":"1955-01-21",
			"first_name":"Kyoichi",
			"last_name":"Maliniak",
			"gender":"M",
			"hire_date":"1989-09-12"
		},
		{
			"emp_no":"10006",
			"birth_date":"1953-04-20",
			"first_name":"Anneke",
			"last_name":"Preusig",
			"gender":"F",
			"hire_date":"1989-06-02"
		},
		{
			"emp_no":"10007",
			"birth_date":"1957-05-23",
			"first_name":"Tzvetan",
			"last_name":"Zielinski",
			"gender":"F",
			"hire_date":"1989-02-10"
		},
		{
			"emp_no":"10008",
			"birth_date":"1958-02-19",
			"first_name":"Saniya",
			"last_name":"Kalloufi",
			"gender":"M",
			"hire_date":"1994-09-15"
		},
		{
			"emp_no":"10009",
			"birth_date":"1952-04-19",
			"first_name":"Sumant",
			"last_name":"Peac",
			"gender":"F",
			"hire_date":"1985-02-18"
		},
		{
			"emp_no":"10010",
			"birth_date":"1963-06-01",
			"first_name":"Duangkaew",
			"last_name":"Piveteau",
			"gender":"F",
			"hire_date":"1989-08-24"
		}
	];

**แก้ไข**ไฟล์ *chapter03.html* โดย**เพิ่ม**

	<div ng-controller="EmployeeController">

		{{ employees }}

	</div>

**แก้ไข**ไฟล์ *chapter03.html* โดย**แก้ไข**

	<div ng-controller="EmployeeController">

		<p ng-repeat="e in employees">{{ e }}</p>

	</div>

### Quiz 03-2

- เขียน Code เพื่อแสดงข้อมูลในแต่ละ Field (*emp_no*, *birth_date*, *first_name*, *last_name*, *gender*, *hire_date*) โดยใช้ `<table>`
- ใช้ `ng-if` แสดง *gender* เป็น Male และ Female

### การ Filter `ng-repeat`

**แก้ไข**ไฟล์ *chapter03.html* โดย**เพิ่ม**

	<input type="text" ng-model="query" placeholder="Search">
	<p>{{ query }}</p>

**แก้ไข**ไฟล์ *chapter03.html* โดย**แก้ไข**

	ng-repeat="e in employees | filter: query"

### การ Filter `ng-repeat` แบบเจาะจง Field

**แก้ไข**ไฟล์ *chapter03.html* โดย**เพิ่ม**

	<input type="text" ng-model="query.last_name" placeholder="Last Name">

### การ Sort `ng-repeat`

**แก้ไข**ไฟล์ *chapter03.html* โดย**เพิ่ม**

	<input type="radio" ng-model="sort" value="first_name"> Sorted by First Name
	<p></p>
	<input type="radio" ng-model="sort" value="last_name"> Sorted by Last Name

**แก้ไข**ไฟล์ *chapter03.html* โดย**แก้ไข**

	ng-repeat="e in employees | orderBy: sort"

### การ Sort `ng-repeat` แบบ Descending

**แก้ไข**ไฟล์ *chapter03.html* โดย**เพิ่ม**

	<input type="radio" ng-model="sort" value="-first_name"> Sorted by First Name (Descending)