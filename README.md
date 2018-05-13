# MongoDB  - Práctica para Bases de Datos (Windows)


## Crear una base de datos

```console
> use tiendaOnline
switched to db tiendaOnline
```


## Tener una colección
```console
> db.createCollection('cursos')
{ "ok" : 1 }
```


## Insertar, modificar y borrar documentos en la colección

### Insertar
```console
> db.cursos.insert({nombre: "Angular 5", horas: 30, profesor: "Elena Nito"})
WriteResult({ "nInserted" : 1 })
> db.cursos.insert({nombre: "Bootstrap 4", horas: 5, profesor: "Elena Nito"})
WriteResult({ "nInserted" : 1 })
> db.cursos.insert({nombre: "Python", horas: 60, profesor: "Aquiles Bailo"})
WriteResult({ "nInserted" : 1 })
> db.cursos.insert({nombre: "MongoDB", horas: 6, profesor: "Armando Bronca"})
WriteResult({ "nInserted" : 1 })
> db.cursos.insert({nombre: "SQL Server", horas: 10, profesor: "Armando Bronca"})
WriteResult({ "nInserted" : 1 })
> db.cursos.insert({nombre: "Java", horas: 20, profesor: "Elsa Capunta"})
WriteResult({ "nInserted" : 1 })
```

### Modificar
```console
> p = db.cursos.findOne({nombre: "MongoDB"})
{
        "_id" : ObjectId("5af6870983377b3b7eeff2e3"),
        "nombre" : "MongoDB",
        "horas" : 6,
        "profesor" : "Armando Bronca"
}
> p.horas = 8
8
> db.cursos.update({nombre: "MongoDB"}, p)
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

### Borrar
```console
> db.cursos.remove({nombre: "SQL Server"})
WriteResult({ "nRemoved" : 1 })
````



## Crear un índice sobre un campo de la colección

En este apartado vamos a crear un índice único para que no pueda repetirse el campo "nombre" del curso.

### Antes de crear el índice
```console
> db.cursos.insert({nombre: "Java", horas: 200, profesor: "Elsa Capunta"})
WriteResult({ "nInserted" : 1 })
> db.cursos.find()
{ "_id" : ObjectId("5af6868783377b3b7eeff2e0"), "nombre" : "Angular 6", "horas" : 30, "profesor" : "Elena Nito" }
{ "_id" : ObjectId("5af686a783377b3b7eeff2e1"), "nombre" : "Bootstrap 4", "horas" : 5, "profesor" : "Elena Nito" }
{ "_id" : ObjectId("5af686dc83377b3b7eeff2e2"), "nombre" : "Python", "horas" : 60, "profesor" : "Aquiles Bailo" }
{ "_id" : ObjectId("5af6870983377b3b7eeff2e3"), "nombre" : "MongoDB", "horas" : 8, "profesor" : "Armando Bronca" }
{ "_id" : ObjectId("5af6885f83377b3b7eeff2e5"), "nombre" : "Java", "horas" : 20, "profesor" : "Elsa Capunta" }
{ "_id" : ObjectId("5af68cd783377b3b7eeff2e6"), "nombre" : "Java", "horas" : 200, "profesor" : "Elsa Capunta" }
```
Nos ha permitido añadir un segundo documento con nombre "Java" que ya existía en la colección.

### Creamos el índice
```console
> db.cursos.createIndex({"nombre": 1}, {"unique":true})
{
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```

### Después de crear el índice
```console
> db.cursos.insert({nombre: "Java", horas: 200, profesor: "Elsa Capunta"})
WriteResult({
        "nInserted" : 0,
        "writeError" : {
                "code" : 11000,
                "errmsg" : "E11000 duplicate key error collection: tiendaOnline.cursos index: nombre_1 dup key: { : \"Java\" }"
        }
})
```
No lo inserta y además nos muestra el mensaje de error.



## Realizar consultas en las que utilices, igual, mayor y menor que

Para mostrar los documentos de una manera más clara, hemos usado la función pretty().

### Igual
Cursos que tengan 20 horas.
```console
> db.cursos.find({horas: 20}).pretty()
{
        "_id" : ObjectId("5af6885f83377b3b7eeff2e5"),
        "nombre" : "Java",
        "horas" : 20,
        "profesor" : "Elsa Capunta"
}
```

### Mayor que (Mayor o igual que)
Cursos que tengan más de 20 horas.
```console
> db.cursos.find({horas: {$gt:20}}).pretty()
{
        "_id" : ObjectId("5af6868783377b3b7eeff2e0"),
        "nombre" : "Angular 6",
        "horas" : 30,
        "profesor" : "Elena Nito"
}
{
        "_id" : ObjectId("5af686dc83377b3b7eeff2e2"),
        "nombre" : "Python",
        "horas" : 60,
        "profesor" : "Aquiles Bailo"
}
```

Cursos que tengan 20 horas o más.
```console
> db.cursos.find({horas: {$gte:20}}).pretty()
{
        "_id" : ObjectId("5af6868783377b3b7eeff2e0"),
        "nombre" : "Angular 6",
        "horas" : 30,
        "profesor" : "Elena Nito"
}
{
        "_id" : ObjectId("5af686dc83377b3b7eeff2e2"),
        "nombre" : "Python",
        "horas" : 60,
        "profesor" : "Aquiles Bailo"
}
{
        "_id" : ObjectId("5af6885f83377b3b7eeff2e5"),
        "nombre" : "Java",
        "horas" : 20,
        "profesor" : "Elsa Capunta"
}
```


### Menor que (Menor o igual que)
Cursos que tengan menos de 8 horas.
``` console
> db.cursos.find({horas: {$lt:8}}).pretty()
{
        "_id" : ObjectId("5af686a783377b3b7eeff2e1"),
        "nombre" : "Bootstrap 4",
        "horas" : 5,
        "profesor" : "Elena Nito"
}
```

Cursos que tengan 8 horas o menos.
```console
> db.cursos.find({horas: {$lte:8}}).pretty()
{
        "_id" : ObjectId("5af686a783377b3b7eeff2e1"),
        "nombre" : "Bootstrap 4",
        "horas" : 5,
        "profesor" : "Elena Nito"
}
{
        "_id" : ObjectId("5af6870983377b3b7eeff2e3"),
        "nombre" : "MongoDB",
        "horas" : 8,
        "profesor" : "Armando Bronca"
}
```

<span style="color:blue">Tip</span>



