# proyecto MongoDB
### 1. Debes seleccionar un fichero json que incluya todos los tipos de datos soportados en MongoDB
El fichero .json es [prankkids.json](prankkids.json). se trata de una consulta a la api [https://db.ygoprodeck.com/api-guide/](https://db.ygoprodeck.com/api-guide/) solicitando todas las cartas que pertenecen al arquetipo [Brominiños](https://yugioh.fandom.com/es/wiki/Bromini%C3%B1os)
### 2. Con la utilidad mongoimport introduce los documentos correspondientes a esa colección.
Para ello, se debe ejecutar el siguiente comando en la terminal:
```
mongoimport --db=yugioh --collection=prankkids --jsonArray --type json --file=prankkids.json
```
![](capturas/captura1.png)