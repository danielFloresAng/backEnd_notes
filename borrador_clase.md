// CLASE 14 - Mongoose //

- 01:13:00 -> Objeto de conexión
  <!-- ---------------------------------------------------------- -->
  <!-- ---------------------------------------------------------- -->

// CLASE 16 - Mongo avanzado I //

PUNTOS CLAVES DE VIDEO:

- 00:43:00 -> Crear un índice
- 00:47:53 -> habilitar un índice
- 01:13:40 -> Populate
- 01:27:40 -> Explicación de populate

NOTAS:

- Siempre que hacemos consultas a la base de datos de Mongo DB por mongoose en nuestra app, debe de ser a travez de un módelo.

- Usear índices sólo dónde sea necesario

- Populate sirve para cruzar datos entre colecciones, en una única consulta puedo tener todos los datos completos, sirve para sintetizar el número de consultas individuales resumiéndoslos en una sola.
  <!-- ---------------------------------------------------------- -->
  <!-- ---------------------------------------------------------- -->

// CLASE 17 - Mongo avanzado II //

PUNTOS CLAVES DE VIDEO:

- 00:31:00 -> agregate
- 01:42:00 -> paginado (mongoose-paginate-v2)
  <!-- ---------------------------------------------------------- -->
  <!-- ---------------------------------------------------------- -->

// CLASE 18 - Cookies, Sessions & Storages //

<!-- PUNTOS CLAVES DE VIDEO:
-->

- 00:16:00 -> Termina repaso
- 00:17:00 -> Empieza introducción de tema
- 00:35:00 -> Importar y configurar 'cookie-parser' en app.js
- 00:38:00 -> Método para generar cookies
- 00:38:00 -> Método para generar cookies
- 00:39:00 -> Parámetros de una cookie
- 00:47:00 -> Generando, recuperando y eliminando cookies.
- 00:57:00 -> Firmar cookies
- 01:27:00 -> Instalación y configuración de express-sessions
- 01:40:00 -> Uso de req.sessions con un counter usando endpoint '/api/sessions'
- 01:50:00 -> Ejemplo de login y logout

<!-- NOTAS:
-->

- Cookies son pequeños paquetes de datos para almacenar preferencias.
  <Nota: El backend no tiene control sobre las cookies ya que se almacenan en el navegador del lado del cliente, por lo que no es recomendable manejar datos sensibles dentro de las cookies.

* Método para generar cookies --> .cookie()
  Ej: res.cookie() <!-- Si la cookie es generada dentro de un método de rutas como GET, podemos usar el método en la respuesta de la petición(res)  -->
* Una cookie tiene 3 parámetros:

  - Nombre
  - Playload o carga útil
  - Opciones de configuración (caducidad de la cookie)

  Ej. res.cookie('Nombre de la cookie', {playload:'Contenido de la cookie', {maxAge: 10000}})<!-- maxAge es el tiempo de vida de la cookie, se mide en milisegundos -->

<Nota: para ver cookies en el navegador necesitamos ir a las herramientas de desarrollador, ir a la pestaña 'application' y en la columna izquierda aparecen las cookies

- Podemos generar, recuperar y eliminar cookies desde cada endpoint

  - Generar cookies: cómo se había explicado antes, se usa la respuesta 'res' con el método .cookie() y ésta cookie se generará en el navegador. Ej.:
      <!-- Ej.:
      router.get("/setCookies", async (req, res)=>
      {res.cookie('mi_cookie_','contenido o playload, {maxAge:10000})}
      -->

  - Recuperar cookies: Se pueden recuperar las cookies atravez de la solicitud 'req', el navegador devolverá las cookies a la app.

      <!-- Ej.:
      router.get("/getCookies", async (req, res)=>{
      res.send(req.cookie)
      }
      -->

- Eliminar cookies: Para eliminar cookies necesitamos usar el método .clearCookie() en la respuesta 'res', de la app, debemos utilizar el nombre de la cookie que queremos eliminr.
    <!-- Ej.:router.get("/getCookies", async (req, res)=>{
      res.send(req.clearCookie('mi_cookie'))
      }
      -->

* Firmar cookies: Firmar una cookie da un extra de seguridad en los datos que se manejan, sin embargo, recordemos que las cookies siguen estando en el lado del cliente por lo que aún siguen sin se la opción más segura.

- Antes de firmar una cookie necesitamos agregar el SECRET dentro de la habilitación de app.use(cookieParser())
     <!-- Ej.:
    app.use(cookieParser(config.SECRET)) 
      -->
- Después activamos la opción 'signed: true' dentro del objeto de configuración de la cookie
<!-- Ej.:
  res.cookie("mi_cookie", "ésta es la primer cookie", { maxAge: 100000, signed: true });
 -->

- Ahora en la petición para recuperar cookies se usa .signedCookies
  <!-- Ej.:
  res.status(200).send({ origin: config.SERVER, playload: req.signedCookies });
   -->

* Para activar el uso de sesiones en la app, necesitamos instalar express-session, importarlo en el archivo principal de la app y usar .use() para el uso de sesiones.
  En el app.use(session()) se pondrá un objeto con el 'secret' y dos propiedades más:

<!-- Ej.:
  app.use(
  session({
    secret: config.SECRET,
    resave: true,
    saveUninitialized: true,
  })
);
 -->

- - - > En el objeto req.session podemos almacenar cualquier dato.
    <!-- Ej.:
      req.session.userName = 'Rei'
      req.session.counter = 1
      req.session.user = {
          email: "clair@gmail.com",
          password: "claire123",
          name: "Claire La Fout",}
     -->

<Nota: Después de haber completado el proceso anterior, tendremos el objeto 'req.session' disponible para trabajar en nuestra app.

<Nota: Las sesiones están del lado del servidor, por lo que es más seguro que las cookies, ya que el back-end tiene control absoluto de los datos.

<!-- ---------------------------------------------------------- -->
<!-- ---------------------------------------------------------- -->

// CLASE 19 - Cookies, Sessions & Storages II //

<!-- PUNTOS CLAVES DE VIDEO:
-->

- 00:26:00 -> Instalar y configurar session-file-store en la app
- 00:40:00 -> Instalar y configurar connect-mong-
<!-- NOTAS:
-->

<Nota: Recordar que las cookies están del lado del cliente(navegador) y las sesiones del lado del servidor(back-end), por lo que no es recomendable manejar datos sencibles en las cookies ya que no es tan seguro.

- Pasos para usar session-file-store en app

  - Instalar ----------------> npm i session-file-store
  - Importar en app ---------> import FileStore from 'session-file-store' y almacenar en una variable: <!-- const fileStorage = FileStore(session) -->
  - Configurar uso de persistencia con .use()
  <!--
  app.use(
  session({
    store: new fileStorage({ path: "./sessions", ttl: 100, retries: 0 }),
    secret: config.SECRET,
    resave: true,
    saveUninitialized: true,
  })
   -->

- Usar connect-mongo en app, persistencia en base de datos
  - Instalar ----------------> npm i connect-mongo
  - Importar en app ----------> import MongoStore from "connect-mongo";
  - Configurar uso de persistencia con .use()
      <!-- 
      app.use(
      session({
        store:MongoStore.create({
          mongoUrl: config.MONGO_URI,
          TTL: 15
        })
        secret: config.SECRET,
        resave: true,
        saveUninitialized: true,
      })
       -->

  * Para hacer un login es necesario que la plantilla renderice el req.session para que ésta muestre la información del usuario una vez que éste acceda. 
  Desde la ruta de '/login' se debe redireccionar al usario a su perfil si es qué el usuario y contraseña son correctos, se usa el método .redirect() en la respuesta. 
  <!-- Ej.:

  router.post('.login', (req, res)=> {
    savedUser.email === email && savedUser.password === password
      ? res.redirect("/profile")
  })
   -->

<!-- ---------------------------------------------------------- -->
<!-- ---------------------------------------------------------- -->
    // CLASE 20 - Autenticación y autorización //

<!-- PUNTOS CLAVES DE VIDEO:
-->

- 00:29:00 -> Métodos de autenticación
- 00:40:00 -> Mención: manera de sintetizar el if con ? (no es ternario)
- 00:44:00 -> bcrypt, passport y passport-local (instalar con npm)
- 00:50:00 -> Explicación hash (no usar clave plana, usar hash)
- 00:54:00 -> Usar bcrypt
- 01:07:00 -> Probando autenticación
- 01:26:00 -> Resolviendo autenticación

<!-- NOTAS:
-->

- AUTENTICACION: Identificar usuarios
- AUTORIZACION: Verificar nivel de usuario (user, admin, premium, etc...)

- 200 -> Sin error
- 500 -> Error general al procesar
- 401 -> Error de autenticación(fallo en datos de usuario)
- 403 -> Error de autorización(fallo en el nivel de usuario(admin, user, etc...))

<!-- ---------------------------------------------------------- -->
<!-- ---------------------------------------------------------- -->

// CLASE 21 - Estrategia de autenticación por terceros + JWT //

<!-- PUNTOS CLAVES DE VIDEO:
retraso de 4 minutos
-->

- 00:06:00 -> Spread operator
- 00:55:00 -> Autenticación por terceros: xonfiguración en git hub
- 01:06:00 -> Configurar estrategia passport con git hub en el código
- 01:13:00 -> Confiurar view para logear con git hub
- 01:15:00 -> Clinet_id, secret y callback en config(provisionalmente, son datos sensibles)
- 01:28:00 -> Explicación de autenticación
- 01:39:00 -> Tipos de login (local, passport, externos)

<!-- NOTAS:
-->

- Midlewars son funciones que tienen acceso a los enpoints en todos los modos de peticiones
- No mostrar secret: Se quitaría de config.js

<!-- ---------------------------------------------------------- -->
<!-- ---------------------------------------------------------- -->

// CLASE 24 - Práctica integradora //
<!-- PUNTOS CLAVES DE VIDEO:
retraso de 4 minutos
-->

- 00:03:00 -> Resumen de rutas


<!-- NOTAS:
-->


<!-- ---------------------------------------------------------- -->
<!-- ---------------------------------------------------------- -->
