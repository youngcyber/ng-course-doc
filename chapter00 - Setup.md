chapter00 - Setup
=================

### ติดตั้งโปรแกรม

- [Sublime Text 3](http://www.sublimetext.com/3)
- [Chrome's LiveReload Extension](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei?hl=EN)
- [Chrome's Postman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm)
- [Firefox's LiveReload Add-On](https://addons.mozilla.org/en-us/firefox/addon/livereload/)
- [Firefox's RESTClient](https://addons.mozilla.org/en-US/firefox/addon/restclient/)
- [Node.js](https://nodejs.org/download/)

### สร้าง Project Folder

1. สร้าง Folder สำหรับเก็บ Project สามารถสร้างไว้ที่ใดก็ได้เช่น *C:\ng-course*
2. เปิดโปรแกรม Command Prompt และ พิมพ์ `cd c:\ng-course`

### ติดตั้ง `gulp-connect` เพื่อใช้เป็น HTTP Server

สร้างไฟล์ *package.json* ไว้ใน Project Folder

	{
		"dependencies": {},
		"devDependencies": {
			"gulp": "latest",
			"gulp-connect": "latest"
		}
	}

สร้างไฟล์ *gulpfile.js* ไว้ใน Project Folder

	var
		gulp = require('gulp'),
		connect = require('gulp-connect');

	var
		src = [
			'*.html',
			'*.js',
			'app/**/*.html',
			'app/**/*.js'
		];

	gulp.task('connect', function() {
		connect.server({
			root: __dirname,
			livereload: true,
			port: 8000
		});
	});

	gulp.task('watch', function() {
		gulp.watch(src, ['reload']);
	});

	gulp.task('reload', function() {
		gulp.src(src)
			.pipe(connect.reload());
	});

	gulp.task('default', ['connect', 'watch']);

พิมพ์คำสั่งที่ Command Prompt เพื่อติดตั้ง *gulp* และ packages

	npm install -g gulp

	npm install

สร้างไฟล์ *index.html* ไว้ใน Project Folder

	<!DOCTYPE html>
	<html>
	<head>
		<title>AngularJS - Course</title>
	</head>

	<body>
		<h3>AngularJS - Course</h3>
	</body>
	</html>

พิมพ์คำสั่งที่ Command Prompt เพื่อ Start HTTP Server

	gulp

ใช้ Chrome เปิด URL

	http://localhost:8000