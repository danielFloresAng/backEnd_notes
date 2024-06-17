// CRUD //

<!--
C -> Create
R -> Read
U -> Update
D -> Delete
-->

// MONGO DB //

<!-- CRUD in Mongo -->

- db.collection_name.insertOne(doc)
  -> add a new documment to the collection

- db.collection_name.insertMany(docs)
  ->Adds severals documents to the collection(an array of documents)

- db.collection_name.findOne(opt)
  -> Return the first found document that contains the search criteria(opt)

- db.collection_name.find(opt)
  -> Return all the documents that contains the search criteria

- db.collection_name.find(opt).pretty()
  -> Shows the results of find() method more readables

<!-- ---- Methods ----  -->

- use data_base_name
  --> select de DB that we want to use

- db.collection_name.find({query})
  --> finds the documents we want in the collection

- db.createCollection('collection_name')
  --> creates new collection

- show dbs
  --> shows all the databases

- db.collection_name.insertOne({'property': "value"})
  --> adds an object

- db.collection_name.insertMany([{array_with_two_or_more_objects}])
  --> adds an array with severals objects

- db.collection_name.deleteOne({"property":"value"})
  --> delete one document in the selected collection

- db.collection_name.estimateDocumentCount()
  -> Makes an aproximate count of the documets by its metadata

- db.collection_name.countDocuments(opt)
  -> Makes a count of the documets that contains the options(opt)

- db.collection_name.updateOne({"unique_property": "value"}, {"property_to_update": "new_value"})
  --> Updates one property of the selected collection, usually we are going to use the collection ID to select the object to update.

<!-- Operators in Mongo DB -->

- $and
    syntax -> {$and:[{},{}]}

- $or
    syntax -> {$or:[{},{}]}

- $lt (les than)
    syntax -> {'propery':{$lt: "value_condition"}}

- $lte (les than or equal)
    syntax -> {'propery':{$lte: "value_condition"}}

- $gt (greater than)
    syntax -> {'propery':{$gt: "value_condition"}}

- $gte (greater than or equal)
    syntax -> {'propery':{$gte: "value_condition"}}

- $ne (not equal)
    syntax -> {'propery':{$ne: "value_condition"}}

- $eq (equal)
    syntax -> {'propery':{$eq: "value_condition"}}

<!--
//// Note:
We cand write one or more conditions to filter elements, just need to separate them with a come ",".

Ej.:
db.students.find({"gender": "Male", "age": {$lt:40}})
 -->

<!-- Limit, Skip and Sort -->

- .sort("name": -1)  
   -> Orders the documents in descendant or ascendent, depends of the properties selected.

- .skip(offset)
  -> Omit the numbers of the indicated documents with the offset

- .limit(num)
  -> Limits the number of the returned documents

<!-- Index -->

- An index makes the access to a content more agile and easy. We can search some subject in the index an once we find it we can go to that 'page'.

- We have a default 'index' by id in mongo DB

- To able an inedex inside the mongoose schema we need to put 'index: true' inside the object property that we want to able the index on.
Ej.:
<!--
const schema = new mongoose.Schema({
lastName: { type: String, required: true, index: true },
});
 -->

<!--
//// Note:
Just use the 'index' only on the fields that could be useful because use the 'index' property use system resources.
-->

- mongooseModel.explain('executionStats') -> return an array request statistic.

  // POPULATE //

* Works to access to all the collections inside our data base that we want and makes queries between them in just one request.

to use the .populate() method we need to put a reference (ref) in the model schema property that we want to use in the query.
Then , in the query we use .pupulate() with the the 'path' property (where we are going to type the property) and the model that we want to use(model)

Ej.:

File: cart.model.js

const schema = new mongoose.Schema({
\_user: type: mongoose.Schema.Types.ObjectId,
ref:'user_index',<!-- Here we put the reference that we are going to use in the 'path' propertie inside the .populate() on the query, that value makes reference to the collection, in this case is 'user_index' -->
required: true,

})

File: cart.routes.js

router.get('/', async (req,res)=>{

const carts = await cartsModel.find().populate({path: '\_user'<!-- Here we use the reference of the model, 'path' makes reference to the schema propertie that we want to use, in this case is the user of propertie of the 'user_index' collection, '_user' -->, model: userModel<!-- Here we vinculate the model that we want to acces to make queries on it data -->})

res.send({origin:'local', playload: carts})
})

// COOKIES //

- Pequeños paquetes de datos, estos datos son normalmente, información del usuario en base a los 'rastros' que el cliente va dejando en el navegador.
  Las cookies no se almacenan en el servidor, se almacenan del lado del cliente.

- Cookies -> Navegador/cliente. No datos sencibles, no es seguro.

- Sessions -> Almacenamiento del lado del servidor

// SOCKET.IO //

- 1:
Instanciar servidor de express para usar ese servidor dentro de la instancia de socket.io
<!-- 
Ej.:

const httpServer = app.listen(8080, ()={
console.log('Servidor funcionando en puerto 8080')
})

const socketInstance = new Server(httpServer)

app.set('socketInstance', socketInstance)
-->

- 2:
  Se suscribe el servidor a los tópicos de socket.io

Ej.:
/// Este proceso se hizo en un archivo separado (sockets.js), no dentro de app.js, para ordenar el proyecto. ///

import { Server } from "socket.io";

const socketInit = (httpServer) => {
let messages = [];

const io = new Server(httpServer);
io.on("connection", (user) => { <!-- .on() sirve para encender el servidor de socket.io -->
user.emit("chat", messages);

<!--
    El .emit() necesita cómo parámetros el nombre del evento y el contenido de éste, en éste caso el nombre es 'chat' y el contenido es 'messages', qué es el array vacío de clarado al principio de la función.
     -->

    console.log(
      `Cliente conectado desde ${user.handshake.address}. ID de usuario: ${user.id}`
    );

    io.on("newMessage", (data) => {
      messages.push(data);
      console.log(`Mensaje de ${user.id}: ${data.message}`);

      io.emit("messageArrived", data);
    });

});

return io;
};

// MONGOOSE-PAGINATE //

- Install -> npm i mongoose-paginate-v2

- Import -> import mongoosePaginate from 'mongoose-paginate-v2'

- Use -> mongooseSchema.plugin(mongoosePaginate)
 <!-- 'schema' is the mongoose schema that we declared in the mongoose model. Ej.: 'productsSchema' or 'userSchema' -->

- Params on the paginate -> mongooseModel.paginate({role:'admin'<!-- filter -->},{page:1, limit:5})
<!-- The .paginate() method recieves two parameters, the first is an object with the filters and the second an object with the limit of items that we want to show and the page of that items. -->

