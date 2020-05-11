```javascript
// Create database
> use monuments

// Create collection
> db.createCollection('locations')

// Create Index in location field
db.locations.createIndex({ location: "2dsphere" });

// Insert data into created collection 'locations'
db.locations.insertMany([
    {name: "Tour Effeil", location: { type: "Point", coordinates: [2.294490337371826,48.858284648396626] } },
    {name: "Arc de Triomphe", location: { type: "Point", coordinates: [2.2950428724288936,48.873776219298364] } }, 
    {name: "Élysées", location: { type: "Point", coordinates: [2.31673926115036,48.870378365042214] } }
])

// Find nearest point location
db.locations.findOne({ 
  location: {
     $near: {
       $geometry: {
          type: "Point",
          coordinates: [2.301807403564453,48.86200447443296]
       },
       $maxDistance: 1000,
       $minDistance: 0
     }
   }
})

// Select 2 of 3 points
db.locations.find({ 
  location: {
    $geoWithin: {
      $geometry: {
        type: "Polygon", 
         coordinates: [
          [ 
            [2.2905635833740234,48.86612631167763],
            [2.3253250122070312,48.86612631167763],
            [2.3253250122070312,48.880578291142996],
            [2.2905635833740234,48.880578291142996],
            [2.2905635833740234,48.86612631167763]
          ]
        ] 
      } 
    } 
  } 
}).pretty()

// Find all points location in 4km radius circle
db.locations.find({ 
  location: {
     $near: {
       $geometry: {
          type: "Point",
          coordinates: [2.301807403564453,48.86200447443296]
       },
       $maxDistance: 4000,
       $minDistance: 0
     }
   }
}).pretty()

```
