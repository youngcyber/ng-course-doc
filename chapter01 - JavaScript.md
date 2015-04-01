chapter01 - JavaScript
======================

### เขียน JavaScript

**เพิ่ม**ไฟล์ *chapter01.html*

	<!DOCTYPE html>
	<html>
	<head>
		<title>AngularJS - Course</title>
	</head>
	<body>

		<script>
			console.log('Hello World');
		</script>

	</body>
	</html>

### Chrome's Developer Tool

![](http://i.cubeupload.com/ikYxC6.png)

- Windows -> Ctrl + Shift + I
- OSX -> Ctrl + Opt + I 

### การประกาศตัวแปร

	<script>

		var v1;

		var v2 = 'Hello, World';
		var v3 = 50;

		var v4 = new Date();
		v4.setDate(v4.getDate() - 365);

		console.log(v4);

	</script>

### Function

ตัวอย่างการเขียน Function

	function hello() {
		console.log('Hello');
	}

ตัวอย่างการเขียน Function แบบมี Parameter

	function hello(name) {
		console.log('Hello ' + name);
	}

	hello('World);

### Operator

Operator ต่างๆ `==`, `!=`, `>`, `<`, `>=`, `<=`, `&&`, `||`

ตัวอย่างการเขียน Code

	var v1 = 10;

	if (v1 == 10) {
		console.log('เท่ากับ 10');
	} else {
		console.log('ไม่เท่ากับ 10')
	}

### Array

	var a1 = [1, 2, 3, 4];
	var a2 = ['A', 'B', 'C'];

	console.log(a1);
	console.log(a1[0]);

### Object

	var o1 = {};

ตัวอย่างการเขียน Code

	var o2 = { 
		name: 'Chai', 
		age: 35, 
		birthdate: new Date() 
	};

	console.log(o2);
	console.log(o2.name);
	console.log(JSON.stringify(o2));

ตัวอย่างการเขียน Code, Object แบบมี Function

	var o3 = {
		name: 'Chai',
		greet: function() {
			console.log('Hello');
		}
	}

	o3.greet();
	console.log(JSON.stringify(o3));

### Array of Object

	var ao1 = [ {} ];

ตัวอย่างการเขียน Code

	var ao2 = [
		{ 
			name: 'Chai', 
			age: 35
		},
		{ 
			name: 'Sak', 
			age: 28
		},
		{ 
			name: 'Peter', 
			age: 42
		}
	];

	console.log(ao2);
	console.log(JSON.stringify(ao2));

### JSON

แปลงจาก Object เป็น JSON String

	var o = { 
		name: 'Chai', 
		age: 35, 
		birthdate: new Date() 
	};

	console.log(o);
	console.log(JSON.stringify(o));

แปลงจาก Array of Object เป็น JSON String

	var ao = [
		{ 
			name: 'Chai', 
			age: 35
		},
		{ 
			name: 'Sak', 
			age: 28
		},
		{ 
			name: 'Peter', 
			age: 42
		}
	];

	console.log(ao);
	console.log(JSON.stringify(ao));

แปลงจาก JSON String เป็น Object

	var j = '{"name":"Chai","age":35,"birthdate":"2015-03-23"}';

	console.log(j);
	console.log(JSON.parse(j));