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

// CLASE 20 - Autenticación y autorización //

<!-- PUNTOS CLAVES DE VIDEO:
-->

- 00:29:00 -> Métodos de autenticación
- 00:40:00 -> Mención: manera de sintetizar el if con ? (no es ternario)
- 00:44:00 -> bcrypt, passport y passport-local (instalar con npm)

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
