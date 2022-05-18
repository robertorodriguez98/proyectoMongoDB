# proyecto MongoDB
### 1. Debes seleccionar un fichero json que incluya todos los tipos de datos soportados en MongoDB
El fichero .json es [prankkids.json](prankkids.json). se trata de una consulta a la api [https://db.ygoprodeck.com/api-guide/](https://db.ygoprodeck.com/api-guide/) solicitando todas las cartas que pertenecen al arquetipo [Brominiños](https://yugioh.fandom.com/es/wiki/Bromini%C3%B1os)
### 2. Con la utilidad mongoimport introduce los documentos correspondientes a esa colección.
Para ello, se debe ejecutar el siguiente comando en la terminal:
```
mongoimport --db=yugioh --collection=prankkids --jsonArray --type json --file=prankkids.json
```
![](capturas/captura1.png)
### Insertar varios documentos utilizando los dos métodos de inserción de MongoDB
```
db.prankkids.insertOne(
   {
      "archetype" : "Prank-Kids",
      "atk" : 150,
      "attribute" : "FIRE",
      "desc" : "Carta de pruebas.",
      "id" : 1,
      "linkval" : 2,
      "name" : "carta 1",
      "race" : "Pyro",
      "type" : "Link Monster"
   }
)
```
![](capturas/captura2.png)
```
db.inventory.insertMany([
    {
        "archetype" : "Prank-Kids",
        "atk" : 3000,
        "attribute" : "WATER",
        "desc" : "Carta de pruebas 2.",
        "id" : 1,
        "linkval" : 2,
        "name" : "carta 2",
        "race" : "Pyro",
        "type" : "Link Monster"
     },
     {
        "archetype" : "Prank-Kids",
        "atk" : 150,
        "attribute" : "AIR",
        "desc" : "Carta de pruebas 3.",
        "id" : 1,
        "linkval" : 3,
        "name" : "carta 3",
        "race" : "Pyro",
        "type" : "Link Monster"
     }
 ])
```
![](capturas/captura3.png)
