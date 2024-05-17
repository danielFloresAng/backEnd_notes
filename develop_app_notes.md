///// APP STRUCTURE /////
* project foler
  - src folder
    / app.js
    / config.js
    / sockets.js
    - view
      viewHandlebarsFiles.handlebars
    - routes
      user.routes.js
    - public
      index.html
      staticFiles
    - models
      models.js

  - node_modules folder
  - package.json -> set the "type":"module"
  - package-lock.json -> this file will contain all de dependencies


// SRC //
- //--// app.js structure //--//
    * Imports in app.js:

      - From dependencies:
        * express
        * handlebars
        * mongoose

      - From internal files
        * sockets
        * config.js
        * routes (views, users, products, etc...)

    * Set express => const app = express()
    * Set httpServer with express (app.listen)
    * Set socket:
      - import socket instance from the correct js file where was setted the socket server.
      - set the app.set with the socket server (app.set('socket', socket))
    * Set the app.use parse JSON and urlencode code lines:
    - app.use(express.json());
    -  app.use(express.urlencoded({ extended: true }));


- //--// config.js //--//
  * Is a js file where we can set all the general configurations of the app.
  All these configurations are inside an object comonly call "config". 
  
  * Here are the common properties of the config object:

  const config = {
    SERVER: 'name_of_the_server_to_use',
    PORT: number of the port that we are going to use in our app,
    MONGO_URI: 'direction_of_our_database',
    DIRNAME: 'direction of our src folder'
  }

  * the common value of the DIRNAME config property is going to be the follow: 

  DIRNAME: path.dirname(new URL(import.meta.url).pathname.replace(/^\/([A-Za-z]:\/)/, '$1')), // Win
    get UPLOAD_DIR() { return `${this.DIRNAME}/public/img` },

  to use the URL feature we need to import the path feauter to our js config file:

  import path from 'path';
