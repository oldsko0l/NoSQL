# Atividade MongoDB: Antes e Depois

## Setup

```js
use store

db.customers.insertMany([
  { name: "Ana", age: 25, city: "Salvador", active: true, points: 120 },
  { name: "Bruno", age: 32, city: "Feira de Santana", active: true, points: 300 },
  { name: "Carlos", age: 28, city: "Salvador", active: false, points: 80 },
  { name: "Daniela", age: 40, city: "São Paulo", active: true, points: 500 },
  { name: "Eduarda", age: 22, city: "Rio de Janeiro", active: false, points: 50 }
])
```

## Exercício 1

```js
db.customers.find({ city: "Salvador" }, { _id: 0, name: 1, city: 1 })
```

## Exercício 2

```js
db.customers.updateOne({ name: "Carlos" }, { $set: { active: true } })
```

## Exercício 3

```js
db.customers.updateMany({ city: "Salvador" }, { $set: { state: "BA" } })
```

## Exercício 4

```js
db.customers.updateOne({ name: "Ana" }, { $inc: { points: 50 } })
```

## Exercício 5

```js
db.customers.insertOne({
  name: "Fernando",
  age: 29,
  city: "Recife",
  active: true,
  points: 90
})
```

## Exercício 6

```js
db.customers.deleteOne({ name: "Eduarda" })
```

## Exercício 7

```js
db.customers.updateOne({ name: "Daniela" }, { $set: { vip: true } })
```

## Exercício 8

```js
db.customers.updateOne({ name: "Bruno" }, { $unset: { points: "" } })
```

## Exercício 9

```js
db.customers.find().sort({ age: -1 })
```

## Exercício 10

```js
db.customers.find({ active: true, age: { $gt: 30 } }, { _id: 0, name: 1 })
```

## Desafio

```js
// 1
db.customers.find({}, { _id: 0, name: 1 })

// 2
db.customers.countDocuments()

// 3
db.customers.countDocuments({ active: true })

// 4
db.customers.find().sort({ points: -1 }).limit(1)

// 5
db.customers.find().sort({ age: 1 }).limit(1)

// 6
db.customers.find({ points: { $gte: 100, $lte: 400 } })

// 7
db.customers.find({ city: { $in: ["Salvador", "São Paulo"] } })

// 8
db.customers.find().sort({ name: 1 })

// 9
db.customers.find().limit(3)

// 10
db.customers.find({ active: false })
```
