# prolibu-cli
Prolibu command line interface

# Creating an executable NPM package and using it

This short guide explains how to create an NPM package that can be called as a script from another project.
For clarity:
The package to execute will be called: Module
The place where you use it: Application

# 1. Build your module

Create a standard module **ignore command line parsing**
*Your entry point index.html should be callable using require()*

### Paths
If your module is split in multiple files make sure to use full paths to include them.
For example:
```js
/* Files at lib:
- a.js
- b.js

In a.js:
*/
const b = require('b'); // Won't work
const b = require('./b'); // Works
```

## 1.1 Create a command line entry point

Create another entry point, a node file. Add in here:
*for example: cli.js*
- First line must be: #!/usr/bin/env node
- Command line parsing
- Help
- Validation 
- Require your index.js (or main entry point) and run it
  
## 1.2 Modify your package.json

We'll add a line so npm knows it has to copy the cli.js into .bin 
```json
"bin": {
  "name_of_your_app": "./cli.js"
 }
 //or 
 "bin": "./cli.js"
```
## 1.3 Publish

Check a guide on publishing to npm, when you're ready: 
```sh
npm publish
```
Now your package is readily available to be used anywhere.

# 2. Use your module as script in another application

Say you build a parser, a file processor or any other cool thing. Now you want a new node application to use it when building.

## 2.1 Install as any other NPM module

```sh
npm install your-package --save-dev
```

## 2.2 Using it as a script
Open your package.json
```json
  "scripts": {
    "name_to_call": "your_module_name param1 param2 param3"
  },
```
## 2.3 Run it
```sh
npm run name_to_call 
```

And that's it! Enjoy

## References
- https://docs.npmjs.com/files/package.json