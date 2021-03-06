# proyecto MongoDB
### 1. Debes seleccionar un fichero json que incluya todos los tipos de datos soportados en MongoDB
El fichero .json es [prankkids.json](prankkids.json). se trata de una consulta a la api [https://db.ygoprodeck.com/api-guide/](https://db.ygoprodeck.com/api-guide/) solicitando todas las cartas que pertenecen al arquetipo [Brominiños](https://yugioh.fandom.com/es/wiki/Bromini%C3%B1os)
### 2. Con la utilidad mongoimport introduce los documentos correspondientes a esa colección.
Para ello, se debe ejecutar el siguiente comando en la terminal:
```
mongoimport --db=yugioh --collection=prankkids --jsonArray --type json --file=prankkids.json
```
![](capturas/captura1.png)
### 3. Insertar varios documentos utilizando los dos métodos de inserción de MongoDB
Los métodos son `insertOne` y `insertMany`. Se utilizan de la siguiente manera:
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
### 4. Elimina varios documentos utilizando los dos métodos de eliminación de MongoDB
Los métodos son `deleteOne` y `deleteMany`. Se utilizan de la siguiente manera:
```
db.prankkids.deleteOne({ attribute : "WATER" })
```
![](capturas/captura4.png)
```
db.prankkids.deleteMany({ attribute : "WATER" })
```
![](capturas/captura5.png)
Donde deleteOne borra la primera coincidencia, y deleteMany borra todas las coincidencias.
### 5. Actualiza varios documentos utilizando los tres métodos de actualización de MongoDB
Los métodos son `updateOne`, `updateMany` y `replaceOne`. Se utilizan de la siguiente manera:
```
db.prankkids.updateOne(
   { "attribute" : "FIRE" },
   { $set : { "atk" : 2000 } }
)
```
![](capturas/captura6.png)
```
db.prankkids.updateMany(
   { attribute : "FIRE" },
   { $set : { atk : 2000 } }
)
```
![](capturas/captura7.png)
```
db.prankkids.replaceOne(
   { "name": "Prank-Kids Rocket Ride"},
   { "name": "carta reemplazada"}
)
```
![](capturas/captura8.png)

### 6. Consultas
**5 consultas de datos simples**
* Consulta los documentos cuyo valor "name" es igual a "Prank-Kids Battle Butler", mostrándolo de manera legible
```
db.prankkids.find({ "name" : "Prank-Kids Battle Butler" }).pretty()
```
![](capturas/captura9.png)
* Consulta el primer documento cuyo atributo sea "WIND"
```
db.prankkids.find({ "attribute" : "WIND" }).limit(1)
```
![](capturas/captura10.png)
* Consulta los documentos cuyo valor "linkval" sea mayor que menor o igual a 2
```
db.prankkids.find({ "linkval" : { $lte : 2 } })
``` 
![](capturas/captura11.png)
* Consulta Los documentos cuyo tipo empiece por "Lin"
```
db.prankkids.find({ "type" : {$regex: /^Lin/ } })
```
![](capturas/captura12.png)
* Consulta los documentos cuyo ataque sea superior a 2500, ordenándolo por ataque de forma descendente
```
db.prankkids.find({ "atk" : { $gt : 2500 } }).sort({"atk":1})
```
![](capturas/captura13.png)
**3 consultas con arrays**
* Consulta los documentos que contengan en el array linkmarkers el valor "Bottom" como uno de sus elementos
```
db.prankkids.find( { "linkmarkers": "Bottom" } )
```
![](capturas/captura14.png)
* Consulta los documentos que contengan en el array linkmarkers los valores "Right" y "Bottom" en cualquier orden
```
db.prankkids.find( { "linkmarkers": { $all: ["Right", "Bottom"] } } )
```
![](capturas/captura15.png)
* Consulta los documentos cuyo array linkmarkers tenga exactamente 1 elemento
```
db.prankkids.find( { "linkmarkers": { $size: 1 } } )
```
![](capturas/captura16.png)
**3 consultas con documentos embebidos**
* Consulta los documentos cuyo precio de amazon es igual a 0.40
```
db.prankkids.find( { "card_prices.amazon_price":  "0.40" } )
```
![](capturas/captura17.png)
* Consulta cuántos documentos pertenecen al set de nombre Hidden Summoners
```
db.prankkids.find({"card_sets.set_name":"Hidden Summoners"}).count()
```
![](capturas/captura18.png)
* Consulta los documentos cuya rareza de uno de sus sets es Rare
```
db.prankkids.find({"card_sets.set_rarity":"Rare"})
```
![](capturas/captura19.png)
**Consulta de agrupación**
* lista todos los tipos de carta de hay, así como el número de cartas que hay de cada uno
```
db.prankkids.aggregate([
   {
      $group: {
         _id: "$type",
         count: { $count: { } }
      }
   }
])
```
![](capturas/captura20.png)