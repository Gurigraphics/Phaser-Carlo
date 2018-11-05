# Phaser-Carlo Tutorial
Create a desktop game with javascript that zipped is only +/-7Mb

### Advantages
Applications created with NW.js and Electron have about +/-100Mb - because they include other Chromium in files.

Carlo open your app in Google Chrome that is already installed locally

Then, you can bundle your application into a single executable (without Chromium) that zipped is only +/-7Mb

### What's Carlo
Carlo is a web rendering surface for Node applications created by Google Chrome team.
https://github.com/GoogleChromeLabs/carlo

### How this work
1- Carlo checks whether Google Chrome is installed locally or not

2- Run a browser instance of Google Chrome

3- Run node as server and your app

## How use

### 1- Create a folder and inside the file: *package.json*
```Javascript
{
  "name": "Game",
  "version": "0.0.1",
  "description": "Game example",
  "main": "main.js",
  "scripts": {
    "pack": "pkg package.json", 
    "run": "node main.js"
  },
  "bin": {
    "game": "./main.js"
  },
  "keywords": [],
  "author": "Gurigraphics",
  "license": "Apache-2.0",
  "dependencies": {
    "carlo": "^0.9.0"
  },
  "pkg": {
    "assets": [
      "www/**/*"
    ],
    "targets": [
      "node8-win"
    ]
  }
}
```

### 2- Open prompt and install dependences
```Javascript
npm i
```
### 3- Create a file: *main.js*
```Javascript
'use strict';

const carlo = require('carlo');

(async () => {

  const app = await carlo.launch(
    {
      bgcolor: '#2b2e3b',
      width: 808,
      height: 628,
      center: true
    });

  app.on('exit', () => process.exit());

  app.serveFolder(__dirname + '/www');
  app.serveFolder(__dirname + '/node_modules', 'node_modules');

  await app.load('index.html');
})();
```
### 4- Create a folder "www"

### 5- Put your files (app.js, index.html, etc) inside this folder

### 6- To start game
```Javascript
 npm run run 
 or 
 node main.js
```

### 7- to install pkg globally
```Javascript
npm install pkg -g
```

### 8- to export win desktop game
```Javascript
npm run pack 
or
pkg package.json
or
pkg .
or
pkg node8-win-x64
```

### 9- to export mac and linux

Change package.json targets "node8-win", etc.

Examples:
```Javascript
pkg node6-macos-x64
pkg node4-linux-armv6
```
Others:

platform freebsd, linux, macos, win

arch x64, x86, armv6, armv7

Check: https://github.com/zeit/pkg

### 10- Bonus: to disable Chrome dev tools
 ```
		document.addEventListener('contextmenu', function(e) {
		   e.preventDefault();
		});

		document.onkeydown = function(e) {
			if(event.keyCode == 123) {
			 return false;
			}
			if(e.ctrlKey && e.shiftKey && e.keyCode == 'I'.charCodeAt(0)) {
			 return false;
			}
			if(e.ctrlKey && e.shiftKey && e.keyCode == 'C'.charCodeAt(0)) {
			 return false;
			}
			if(e.ctrlKey && e.shiftKey && e.keyCode == 'J'.charCodeAt(0)) {
			 return false;
			}
			if(e.ctrlKey && e.keyCode == 'U'.charCodeAt(0)) {
			 return false;
			}
		}
```
  
  


