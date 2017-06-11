# Getting Started

## Prerequiaite
Make sure you have `node` and `npm` installed on your computer. 
If not, for OS X or Windows, the best way to install Node.js is to use one of the installers from the [Node.js download page](https://nodejs.org/en/download/). If you're using Linux, you can use the installer, or you can check [NodeSource's binary distributions](https://github.com/nodesource/distributions) to see whether or not there's a more recent version that works with your system.

!> Test: Run `node -v`. Ensure you're running the latest versions Node v4.x.x+ (or v5.x.x) and NPM 3.x.x+


Clone the repostitory. 
Open a terminal, change directory to the folder under which the project is saved. 

## Install dependencies

Install these dependencies with `npm install`. Use `sudo` in front the command when necessary.
````javascript
npm install
````
## Setup the Intellisense in VisualStudio Code
```javascript
typings install
```

## Prepare MongoDB 
Clone API repository. 
Under `/util`, run `bash create_db.sh`. 
This imports all forecast data and creates necessary indexes.


## Run the API
In another terminal tab, run the app.
```javascript
npm start 
```
Go to http://0.0.0.0:4000 or http://localhost:4000 in your browser


### Start  MongoDB
Under root directory, run `mongod`.