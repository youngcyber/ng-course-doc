chapter02 - ng
==============

### CDN Library ของ Google

	https://developers.google.com/speed/libraries/

### เรียกใช้ Library AngularJS

	<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>

### การใช้ `ng-app`

**เพิ่ม**ไฟล์ *chapter02.html*

	<html ng-app>
		<body>

			{{ 'Hello World' }}
			<br>
			{{ 10 + 20 }}

			<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
		</body>
	</html>

### การใช้ Directive `ng-init`

	<body ng-init="price=500;qty=40">

		Amount: {{ price * qty }}

	</body>

> ### การเรียกใช้ Directive ใน AngularJS
- `ng-init`
- `ng:init`
- `ng_init`
- `x-ng-init`
- `data-ng-init`

### การใช้ Expression `{{ }}` และ `ng-bind`

ใช้ Expression และ Basic Filter

	{{ 1500 | currency }}

ใช้ `ng-bind`

	<span ng-bind="price | currency:'THB '"></span>
	<br>
	<span ng-bind="qty"></span>

### การใช้ Directive `ng-model`

ใช้ `ng-model` กับ `<input type="text">`

	<input type="text" ng-model="name">
	<h3>Hello, {{ name }}</h3>

ใช้ `ng-model` กับ `<input type="radio">`

	Do you like this ?
	<br>
	<input type="radio" value="Yes" ng-model="like"> Yes
	<br>
	<input type="radio" value="No" ng-model="like"> No
	<br>
	You answer: {{ like }}

ใช้ `ng-model` กับ `<select>`

	<select ng-model="age">
		<option value="ละอ่อน">น้อยกว่า 18</option>
		<option value="หนุ่ม-สาว">18 - 25</option>
		<option value="ผู้ใหญ่เต็มตัว">26 - 30</option>
		<option value="แก่แล้วนะ">มากกว่า 30</option>
	</select>
	<br>
	You are: {{ age }}

### การใช้ Directive `ng-change`

	<input type="text" ng-change="counter=counter+1" ng-model="text">

	{{ counter }}

### การใช้ Directive `ng-show`, `ng-hide`

	<body ng-init="show=true">

		<h3>Value of <i>show</i>: {{ show }}</h3>

		<h3 ng-show="show" style="background-color: red;">Show</h3>
		<h3 ng-hide="show" style="background-color: green;">Hidden</h3>

	</body>

### การใช้ Directive `ng-click`

ใช้ทำการ Toggle

	<button ng-click="show=!show">Toggle</button>

ใช้ทำการ Increment

	<button ng-click="counter=counter+1">Counter</button>

	<h3>{{ counter }}</h3>

### การใช้ Directive `ng-if`

	<h3 ng-if="show" style="background-color: red;">Show</h3>
	<h3 ng-if="!show" style="background-color: green;">Hidden</h3>

### การใช้ Directive `ng-switch`

	<input type="radio" ng-model="color" value="red"> Red
	<input type="radio" ng-model="color" value="blue"> Blue
	<input type="radio" ng-model="color" value="green"> Green
	<input type="radio" ng-model="color" value="pink"> Pink

	<div ng-switch="color">
		<span ng-switch-when="red" style="color: {{color}};">Red</span>
		<span ng-switch-when="blue" style="color: {{color}};">Blue</span>
		<span ng-switch-when="green" style="color: {{color}};">Green</span>
		<span ng-switch-default>Others</span>
	</div>

> ### ข้อแตกต่างระหว่าง `ng-show`/`ng-hide` กับ `ng-if`/`ng-switch`
- `ng-show` และ `ng-hide` ทำการ **แสดง** และ **ซ่อน** โดย**ไม่มี**การ **เพิ่ม** หรือ **ลบ** Element ออกจาก *DOM*
- `ng-if` และ `ng-switch` จะทำการ **เพิ่ม** และ **ลบ** Element ออกจาก *DOM*

### การใช้ Directive `ng-class`

กำหนด Style

	<style>
		.italic {
			font-style: italic
		}

		.bold {
			font-weight: bold;
		}
	</style>

ใช้งาน `ng-class`

	<input type="checkbox" ng-model="style1" ng-true-value="'bold'"> Bold
	<input type="checkbox" ng-model="style2" ng-true-value="'italic'"> Italic

	<p ng-class="[style1, style2]">Hello, World</p>

