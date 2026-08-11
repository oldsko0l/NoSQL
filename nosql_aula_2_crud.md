# ✏️ CRUD no MongoDB

O **CRUD** representa as quatro operações fundamentais de qualquer banco de dados. No MongoDB, elas são realizadas sobre **documentos** dentro de **coleções**.

---

## 🏗️ Revisão da Estrutura

Antes de operar dados, é importante fixar a hierarquia:

```
Database  →  Collection  →  Document
(Banco)       (Coleção)      (Documento JSON/BSON)
```

---

## 📄 Anatomia de um Documento JSON

Todo documento é formado por **campos (fields)** — cada campo é um par **chave : valor**:

```json
{
  "name": "Jefté",
  "age": 35,
  "active": true,
  "scores": [9, 8, 10],
  "address": {
    "city": "Feira de Santana",
    "state": "BA"
  }
}
```

| Tipo de Valor | Exemplo | Descrição |
| :--- | :--- | :--- |
| **String** | `"Jefté"` | Texto entre aspas. |
| **Número** | `35` | Inteiro ou decimal. |
| **Booleano** | `true` | Verdadeiro ou falso. |
| **Array** | `[9, 8, 10]` | Lista de valores. |
| **Documento** | `{ "city": "..." }` | Objeto aninhado (embedded). |

> Múltiplos campos são separados por **vírgulas**. A chave e o valor são separados por **dois-pontos (`:`)**.

---

## 🧰 As Quatro Operações CRUD

| Operação | Significado | Comando MongoDB |
| :--- | :--- | :--- |
| **C**reate | Criar | `insertOne()` / `insertMany()` |
| **R**ead | Ler / Consultar | `find()` / `findOne()` |
| **U**pdate | Atualizar | `updateOne()` / `updateMany()` |
| **D**elete | Deletar | `deleteOne()` / `deleteMany()` |

---

## ➕ Create — Inserindo Documentos

**Inserir um único documento:**

```js
db.produtos.insertOne({
  nome: "Notebook",
  preco: 3500,
  estoque: 10
})
```

**Inserir múltiplos documentos de uma vez:**

```js
db.produtos.insertMany([
  { nome: "Mouse", preco: 80 },
  { nome: "Teclado", preco: 150 },
  { nome: "Monitor", preco: 1200 }
])
```

> **💡 Dica:** O MongoDB cria automaticamente o campo `_id` (ObjectId) como identificador único de cada documento, caso você não forneça um.

---

## 🔍 Read — Consultando Documentos

**Buscar todos os documentos:**

```js
db.produtos.find()
```

**Buscar com filtro (equivalente ao `WHERE`):**

```js
db.produtos.find({ nome: "Mouse" })
```

**Buscar apenas um resultado:**

```js
db.produtos.findOne({ preco: 80 })
```

---

## 🔄 Update — Atualizando Documentos

**Atualizar um único documento:**

```js
db.produtos.updateOne(
  { nome: "Mouse" },          // Filtro: qual documento?
  { $set: { preco: 90 } }    // Operação: o que mudar?
)
```

**Atualizar múltiplos documentos:**

```js
db.produtos.updateMany(
  { estoque: 0 },
  { $set: { ativo: false } }
)
```

> **⚠️ Atenção:** Sempre use `$set` para alterar apenas os campos desejados. Sem ele, o documento inteiro pode ser **substituído**.

---

## 🗑️ Delete — Removendo Documentos

**Remover um único documento:**

```js
db.produtos.deleteOne({ nome: "Teclado" })
```

**Remover múltiplos documentos:**

```js
db.produtos.deleteMany({ ativo: false })
```

> **⚠️ Atenção:** Assim como o `DELETE` no SQL, use sempre um filtro preciso. Sem filtro, `deleteMany({})` remove **todos** os documentos da coleção.

---

[⬅️ Página Anterior](nosql_aula_1_visao_geral.md) | [🏠 Início do Repositório NoSQL](01-introducao-nosql.md)
