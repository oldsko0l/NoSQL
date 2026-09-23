# Relações no MongoDB

## _id e Documentos Incorporados

Todo documento precisa ter um `_id`. O MongoDB cria um `ObjectId` automaticamente se você não definir um, mas dá pra colocar um valor customizado também.

Documentos incorporados (embedded) são quando você coloca os dados relacionados dentro do próprio documento. Não precisa de join e é mais rápido pra leitura.

## Projeção

Escolhe quais campos retornar na consulta. Evita trazer o documento inteiro pela rede, economiza largura de banda e memória.

```js
db.customers.find({}, { _id: 0, name: 1, city: 1 })
```

## Schema

O MongoDB não obriga um schema fixo — documentos da mesma coleção podem ter campos diferentes. Mas dá pra usar JSON Schema se quiser validar alguma coisa.

## Tipos de Dados

| Categoria | Tipo | Exemplo |
| :--- | :--- | :--- |
| Texto e Booleano | String, Boolean | "Jefté", true |
| Numéricos | Integer, Long, Decimal | 55, 10000000000, 12.99 |
| Identificadores | ObjectId | ObjectId("5b98d4654d01c52e1637a99b") |
| Datas | ISODate, Timestamp | ISODate("2026-09-15") |
| Estruturas | Embedded Document, Array | { "a": { ... } }, ["item1", "item2"] |

## Perguntas de Arquitetura

Quatro perguntas pra pensar antes de modelar:

- Quais dados são necessários? → define os campos e como eles se relacionam
- Onde o dado é consumido? → define as coleções e agrupamentos
- Qual o tipo de exibição? → determina as consultas mais eficientes
- Qual a frequência de leitura/escrita? → define se o foco é em buscas rápidas ou gravações sem duplicação

## Leitura vs. Escrita

Se o sistema faz muita leitura, melhor usar embedded e guardar o dado já no formato que vai ser exibido.

Se faz muita escrita, melhor usar referências pra não duplicar dado.

---

## Tipos de Relação

### 1:1 (um para um)

**Embedded** — quando os dados pertencem só àquele documento.

```js
db.patients.insertOne({
  name: "Jefté",
  age: 35,
  diseaseSummary: { diseases: ["cold", "broken leg"] }
})
```

**Referência** — quando as duas entidades têm vida própria.

```js
db.persons.insertOne({ name: "Jefté", age: 35, salary: 3000 })

db.cars.insertOne({
  model: "BMW",
  price: 40000,
  owner: ObjectId('6aa9e2cee9c288ce1241317e')
})
```

---

### 1:N (um para muitos)

**Embedded** — quando os filhos sempre são acessados junto com o pai.

```js
db.questionThreads.insertOne({
  creator: "Jefté",
  question: "How does that work?",
  answers: [{ text: "Like that." }, { text: "Thanks!" }]
})
```

**Referência** — quando pode ter muitos filhos e estourar o limite de 16MB.

```js
db.cities.insertOne({ name: "New York City", coordinates: { lat: 21, lng: 55 } })

db.citizens.insertMany([
  { name: "Jefté Goes", cityId: ObjectId("5b98d6b44d01c52e1637a99f") },
  { name: "Brenno Salvador", cityId: ObjectId("5b98d6b44d01c52e1637a99f") }
])
```

---

### N:M (muitos para muitos)

**Embedded** — quando o dado fica "congelado" dentro da entidade.

```js
db.customers.insertOne({ name: "Jefté", age: 35 })

db.customers.updateOne({}, {
  $set: { orders: [{ title: "A Book", price: 12.99, quantity: 2 }] }
})
```

**Referência** — quando as duas entidades existem de forma independente.

```js
db.authors.insertMany([
  { name: "Jorge Amado", age: 78, address: { street: "Bahia" } },
  { name: "Graciliano Ramos", age: 55, address: { street: "Rio de Janeiro" } }
])

db.books.updateOne({}, {
  $set: { authors: [
    ObjectId("5b98d9e44d01c52e1637a9a6"),
    ObjectId("5b98d9e44d01c52e1637a9a7")
  ]}
})
```

---

## Embedded vs. References

Use embedded quando os dados são sempre lidos juntos, têm forte relação de pertencimento e não são compartilhados com outras coleções.

Use referências quando os dados são compartilhados, têm vida independente ou o documento pode crescer muito.
