# Introduction
[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)
[![JavaScript Style Guide](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

Folder structure and task implementation of a modular development environment for [Herman-Scheer](http://www.herman-scheer.com/)

Provides fast, reliable and extensible starter for the development of **Modern** microservice based projects.

`hs-microservices` provides the following features:

- Ready to go, build system using gulp and webpack for working with Typescript.
- Production and development builds.
- Development server with Browsersync, and Webpack Dev Middleware.
- Hot Module Reloading for client side applications
- Following the best practices
  - [standard](https://github.com/feross/standard)
  - [stylelint](https://github.com/stylelint/stylelint-config-standard)

Table of Contents
-----------------
- [Prerequisites](#prerequisites)
- [Features](#features)
  - [Client Side](#client-side)
  - [Server Side](#server-side)
- [Start](#start)
- [Installing Dependencies](#installing-dependencies)
- [Project Structure](#project-structure)
  - [Client Directory](#client-directory)
  - [Server Directory](#server-directory)
- [Deployment](#deployment)
- [Troubleshoot](#troubleshoot)
- [Contributors](#contributors)

Prerequisites
--------

**Note** that this project requires 
- node v6.9.x or higher (install nvm if you need node version control)
  - [nvm](https://github.com/creationix/nvm)
- npm 3.10.x or higher (should come installed with node if you used nvm)
- yarn 0.21.x (install through npm with npm install --global yarn)

Features
--------

#### Client Side
- Gulp and Webpack Build

- [Pug templating](https://pugjs.org/api/getting-started.html)

```pug
.block
  .block__element
    h1 hello world
```

- SASS stylesheets [(indented syntax)](http://sass-lang.com/documentation/file.INDENTED_SYNTAX.html)

```sass
.block
  .block__element
    h1
     color: $c1
```

- [Image Handling](https://github.com/tcoopman/image-webpack-loader)

```sass
// sass
.element
  background: url('~images/profile.jpg')
```

```pug
// pug
img(src=require('images/profile.jpg'))
```

- [Responsive Images](https://github.com/herrstucki/responsive-loader)

```sass
// sass
.element
  background: url('~responsive-loader?size=400!images/profile.jpg')
```

```pug
// pug
- var image = require('responsive-loader?placeholder=true&sizes[]=100,sizes[]=200,sizes[]=900!images/profile.jpg')

div(style={
  'background-image': `url(${image.placeholder})`,
  height: image.height,
  width: image.width,
  'background-size': 'cover'
})
  img(src=image.src, srcset=image.srcSet, sizes='100w,200w,300w')
```

- [SVG Icon Sprites](https://github.com/mrsum/webpack-svgstore-plugin)

```pug
// pug
.element
  svg: use(xlink:href='#icon-name-from-global-icons-folder')
```
#### Server Side
- Gulp and Webpack Build

- [ApiDoc File Generation](http://apidocjs.com/)

```typescript
/**
* @api {get} /user/:id Request User information
* @apiName GetUser
* @apiGroup User
*
* @apiParam {Number} id Users unique ID.
*
* @apiSuccess {String} firstname Firstname of the User.
* @apiSuccess {String} lastname  Lastname of the User.
*/
```

- [Nodemon Change Monitoring](https://nodemon.io/)

- [Server Side Typescript](http://jlongster.com/Backend-Apps-with-Webpack--Part-I)

Start
--------
In order to start using the boilerplate:

```bash
### move into the assigned directory
### whether your application will be client side
cd client

### whether your application will be server side
cd server

### make sure you are using the correct node version by running
node -v // 6.9.x

### or if you are using nvm
nvm use

### install the project's dependencies
yarn install

### runs initial development asset build and watches your files by default
npm run gulp build

### watches your files by default
npm run gulp

### runs production build
npm run deploy
```

Installing Dependencies
--------
We will use yarn in order to install all dependencies

```bash
// installing @angular/core
yarn add @angular/core
```

Inside `client/modules/app/app.ts`

```typescript
import { Component } from '@angular/core'

@Component({
  selector: 'app',
  template: `<h1>Hello World</h1>`
})

export class App {}
```

Make sure all dependencies are added to the dependencies field in `client/package.json`

```json
"dependencies": {
  "@angular/core": "^4.1.0"
}
```

Project Structure
-----------------

The project is separated into multiple directories, client and server. If you are only making client side changes then you will be working on the client side directory same if you are making server side changes.

#### Client Directory

| Name                                   | Description                                                                              |
|----------------------------------------|------------------------------------------------------------------------------------------|
| client/**modules**/main.sass           | The main sass file                                                                       |
| client/**modules**/main.ts             | The main application file.                                                               |
| client/**modules**/app/app.ts          | Main application folder, YOUR CODE WILL GO HERE!                                         |
| client/**modules**/polyfills.ts        | Webpack development polyfills                                                            |
| client/**modules**/global              | Global files such as icons, images, sass libraries, and global pug templates             |
| client/**public**/                     | Bundled assets (fonts, css, js, img).                                                    |
| client/.babelrc                        | Local configuration for gulp code in your project                                        |
| client/.env                            | API keys, tokens, passwords and database URI.                                            |
| client/.nvmrc                          | File containing version number in the project root directory                             |
| client/.stylelintrc                    | Configuration file for stylelint                                                         |
| client/gulpfile.babel.js               | Configuration file for gulp and all its tasks																						|
| client/package.json                    | NPM dependencies.                                                                        |
| client/yarn.lock                       | Contains exact versions of NPM dependencies in package.json.                             |
| client/postcss.config.js               | Configuration file for Post CSS, installed plugins will be added here										|

#### Server Directory

| Name                                   | Description                                                                              |
|----------------------------------------|------------------------------------------------------------------------------------------|
| server/**modules**/main.ts             | The main application file.                                                               |
| server/**modules**/app/app.ts          | Main application folder, YOUR CODE WILL GO HERE!                                         |
| server/**modules**/app/api/apidoc.json | API Configuration file                                																		|
| server/**modules**/polyfills.ts        | Webpack development polyfills                                                            |
| server/**modules**/global              | Global files such as icons, images, sass libraries, and global pug templates             |
| server/**public**/                     | Bundled assets (fonts, css, js, img).                                                    |
| server/.babelrc                        | Local configuration for gulp code in your project                                        |
| server/.env                            | API keys, tokens, passwords and database URI.                                            |
| server/.nvmrc                          | File containing version number in the project root directory                             |
| server/.stylelintrc                    | Configuration file for stylelint                                                         |
| server/gulpfile.babel.js               | Configuration file for gulp and all its tasks																						|
| server/package.json                    | NPM dependencies	                                                                        |
| server/pm2.json                    		 | PM2 Configuration file                                                                   |
| server/server.js                    	 | Main run file                                                                        		|
| server/yarn.lock                       | Contains exact versions of NPM dependencies in package.json.                             |

Deployment
--------

In order to deploy either client or server side application, there are some prerequisites.

**Note** that this project requires:
- Docker version 17.x or higher (you can install it with either docker for [mac](https://docs.docker.com/docker-for-mac/) or [windows](https://docs.docker.com/docker-for-windows/))
- A Docker Account
	- You must provide lead developer with your docker account id so that you can push and pull to the project docker hub repository

To deploy an application, please follow these steps:
1. cd into the ***server*** or ***client*** folder
2. Make sure you have commited all your changes to git and you have a clean git
3. Run command ```npm run deploy```
4. Wait for docker and gulp binary to compile.
	- If you experience any errors please screenshot your terminal and send and email to Giuseppe at [g@herman-scheer.com](g@herman-scheer.com)
5. Website should be up in 5-10 mins after final binary is done.

Troubleshoot
-----------------
If you experience any errors please contact Giuseppe at [g@herman-scheer.com](g@herman-scheer.com)

Contributors
-----------------
![giusepperj](https://avatars2.githubusercontent.com/u/5714678?v=3&s=150)
