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
  - app.js structure
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
