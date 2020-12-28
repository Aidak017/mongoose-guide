# ¿Qué es Mongoose?
> Mongoose es un NPM basado en modelos para la base de datos MongoDB.
> En esta guía te enseñaré como usarlo, al final te parecerá fácil :D.

## ¿Qué es MongoDB?
> Es una base de datos NoSQL creada en 2009 en Estados Unidos.
> Es considerada una de las bases de datos más modernas, ya que guarda sus datos en documentos JSON, los cuales son muy flexibles.
> Ahora que ya sabes qué es MongoDB, vamos al lío...

### Empezando
Vamos a crear un Atlas. Para crear un atlas, pincha [aquí](https://mongodb.com/cloud/atlas).
Dale al botón que pone "Start free". Te pedirá que pongas varios datos, si no sabes hacer un login ya no es mi culpa lol.
(puedes hacerlo con google)

Una vez nos hayamos registrado, nos aparecerá esto:
<br>
<br>
<img src="https://i.imgur.com/vXsLGI3.png" width="500">
<br>
Dale al botón verde en el que pone CONNECT y elige la segunda opción: Connect your application.
Crea unas credenciales, después, en Driver pones Node.js y en versión, pues, pon la última.

En la sección 2, pega la URI que te da la ventana, reemplaza <dbname> por algo (ejemplo: tutorial)
y <password> por la contraseña que previamente creaste.

### Creando nuestro proyecto
Ahora crea una app node.js y simplemente escribe estas dos líneas:
y también instala mongoose
```js
const mongoose = require('mongoose')

mongoose.connect('')
```
Okey, donde he puedo el string vacío, quiero que pongáis vuestra uri, tal que así:
```js
mongoose.connect('mongodb+srv://usuario:<password>@cluster0.gresm.gcp.mongodb.net/<dbname>?retryWrites=true&w=majority')
```
pero reemplazando lo que dije por vuestras credenciales.

### Creando mi primer Schema
Ahora, haz una carpeta llamada "models" y crea un archivo llamado Tutorial.js,
en el siguiente escribe esto:
```js
const mongoose = require('mongoose')

const Esquema = new mongoose.Schema({
    Nombre: String,
    Apellido: String,
    Edad: Number
})

const modelo = module.exports = mongoose.model('usuarios', Esquema)
```
Bien, ahora te explico lo que has hecho:
- En el constructor Schema, has puesto que Nombre y Apellido sea un String y Edad sea un número,
por lo que al insertar datos en nuestra colección, se formateará de un modo u otro.
- Al poner const modelo, y exportarlo, y después asignarle la función model, estamos modelando nuestro
schema para adaptarlo a JSON y después, al poner el string 'usuarios', estamos dando nombre a nuestra colección,
que se llamará usuarios.

### Insertando documentos en el Schema
Bien, ahora después de hacer esto, volvemos a nuestro archivo principal y escribimos esto:
```js
const modelo = require('./models/Tutorial.js')
```
Aquí requererimos el modelo, y después para insertar sería:
```js
const nuevo = new modelo({
    Nombre: 'Fulanito',
    Apellido: 'De tal',
    Edad: 14
})
nuevo.save()
```

### Obteniendo documentos del Schema
Ahora, queremos ver si hemos hecho todos estos pasos correctamente.
Vamos a probar:
```js
const data = await modelo.findOne({
    Nombre: 'Fulatino'
})

if (!data) return console.log('No existe shit')

else if (data){
    console.log(data.Nombre + data.Apellido)
}
```
Si nos retorna Fulanito Detal, es que todo va perfecto. :D

### Actualizando documentos del Schema
¿Pero qué pasa si quiero actualizar en vez de crear más documentos?
ez: 
```js
await modelo.findOneAndUpdate({
    Nombre: 'Fulanito',
    Edad: 15
})
```
Poneos en la situación de que Fulanito haya cumplido años y por eso haya que actualizar nuestra base de datos.
Bueno, hasta aquí esta guía de 100 líneas xD, dejadme un star, así sé que me apoyáis, y recordad hacer todos estos pasos
dentro de una funcion asíncrona.