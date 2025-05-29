# S2.04.MongoDBQueriesExercise

## 🍽️ S2.MongoDB.Restaurants

Explorant Restaurants a Nova York amb MongoDB

Aquest projecte fa servir una col·lecció de dades reals i representatives de restaurants a la ciutat de Nova York. Utilitza MongoDB per explorar, filtrar i analitzar informació dels establiments, la seva ubicació, cuina, puntuacions i altres característiques.

📚 Project Overview
L’objectiu d’aquest projecte és practicar consultes MongoDB utilitzant la col·lecció Restaurants, aplicant filtres, projeccions, ordenacions, condicions complexes i operadors d’arrays.

🧱 Col·lecció Restaurants
Cada document representa un restaurant i inclou camps com:

restaurant_id

name

borough

cuisine

address (amb camps: street, zipcode, coord)

grades (array amb informació de puntuacions, dates i notes)

🔍 Consultes destacades
### ✅ Consultes bàsiques
Mostrar tots els documents:

```
db.restaurants.find()
```
Mostrar restaurant_id, name, borough, cuisine:

```
db.restaurants.find({}, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })
```
Mateixa consulta però excloent _id:

```
db.restaurants.find({}, { _id: 0, restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })
```
Mostrar zipcode en comptes de cuisine:

```
db.restaurants.find({}, { _id: 0, restaurant_id: 1, name: 1, borough: 1, "address.zipcode": 1 })
```
### 🌆 Consultes per localització
```
Restaurants del Bronx:

```
db.restaurants.find({ borough: "Bronx" })
```
Primers 5 restaurants del Bronx:

```
db.restaurants.find({ borough: "Bronx" }).limit(5)
```
Següents 5 després dels primers:

```
db.restaurants.find({ borough: "Bronx" }).skip(5).limit(5)
### 📊 Consultes per puntuació i criteris
Restaurants amb score > 90:

```
db.restaurants.find({ "grades.score": { $gt: 90 } })
```
Score entre 80 i 100:

```
db.restaurants.find({ "grades.score": { $gt: 80, $lt: 100 } })
Latitud < -95.754168:

```
db.restaurants.find({ "address.coord.1": { $lt: -95.754168 } })
### 🧠 Consultes amb condicions avançades
Excloure cuina 'American', score > 70, longitud < -65.754168:

```
db.restaurants.find({
  cuisine: { $ne: "American" },
  "grades.score": { $gt: 70 },
  "address.coord.0": { $lt: -65.754168 }
})
Mateixa consulta sense $and:

```
db.restaurants.find({
  cuisine: { $ne: "American" },
  "grades.score": { $gt: 70 },
  "address.coord.0": { $lt: -65.754168 }
})
No 'American', grau 'A', no a Brooklyn, ordenat descendent per cuina:

```
db.restaurants.find({
  cuisine: { $ne: "American" },
  "grades.grade": "A",
  borough: { $ne: "Brooklyn" }
}).sort({ cuisine: -1 })
```

🔤 Consultes amb expressions regulars
Nom comença amb 'Wil':

```
db.restaurants.find({ name: /^Wil/ }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })
Nom acaba amb 'ces':

```
db.restaurants.find({ name: /ces$/ }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })
Nom conté 'Reg':

```
db.restaurants.find({ name: /Reg/ }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })
```
### 🗂️ Operadors in i not in
Bronx amb cuina americana o xinesa:

```
db.restaurants.find({
  borough: "Bronx",
  cuisine: { $in: ["American", "Chinese"] }
})
Restaurants en Staten Island, Queens, Bronx o Brooklyn:

```
db.restaurants.find({
  borough: { $in: ["Staten Island", "Queens", "Bronx", "Brooklyn"] }
})
```
Excloure els anteriors:

```
db.restaurants.find({
  borough: { $nin: ["Staten Island", "Queens", "Bronx", "Brooklyn"] }
})
```
### 🧮 Altres consultes
Restaurants amb marcador divisible per 7:

```
db.restaurants.find({ "grades.score": { $mod: [7, 0] } }, { restaurant_id: 1, name: 1, "grades.score": 1 })
```
Restaurants amb coordenades amb latitud entre 42 i 52:

```
db.restaurants.find({
  "address.coord.1": { $gt: 42, $lte: 52 }
}, { restaurant_id: 1, name: 1, address: 1 })
```

Ordenació per nom ascendent:

```
db.restaurants.find().sort({ name: 1 })
```

Ordenació per cuina ascendent i barri descendent:

```
db.restaurants.find().sort({ cuisine: 1, borough: -1 })
```

### 🧪 Nivells de certificació
### 🎯 Nivell 1 – Bàsic
### ✔️ 17 consultes correctes
Apte per assolir competències bàsiques de MongoDB

### 🏅 Nivell 2 – Avançat
### ✔️ Entre 17 i 25 consultes correctes
Amb execució de consultes a MongoDB Compass

### 🛠️ Tools Used
MongoDB

MongoDB Compass

VS Code

Shell MongoDB

JSON Viewer / Extensions

### 🔗 GitHub Repository (opcional)
📂 https://github.com/UsuariRepositori/S2.MongoDB.Restaurants.git
