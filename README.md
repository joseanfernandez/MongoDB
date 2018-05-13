# MongoDB  - Práctica para Bases de Datos (Windows)


## Crear una base de datos.

```console
> use tiendaOnline
switched to db tiendaOnline
```

## Tener una colección.
```console
> db.createCollection('cursos')
{ "ok" : 1 }
```

# Insertar, modificar y borrar documentos en la colección.

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
