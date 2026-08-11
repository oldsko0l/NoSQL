# 🍃 Introdução ao NoSQL e MongoDB

Enquanto o SQL trabalha com tabelas e relacionamentos rígidos, o **NoSQL** representa um paradigma diferente — projetado para cenários onde flexibilidade, escala e velocidade são prioridades.

---

## 🤔 O que é NoSQL?

**NoSQL** ("Not Only SQL") é um paradigma de banco de dados que engloba diversos tipos de bancos de dados **não relacionais**, projetados para oferecer:

* **Flexibilidade** — estrutura de dados adaptável, sem schema fixo.
* **Escalabilidade** — preparados para crescer horizontalmente (mais máquinas, não máquinas maiores).
* **Alto desempenho** — otimizados para leitura e escrita em grande volume.

---

## 🗂️ Os Quatro Paradigmas NoSQL

| Paradigma | Exemplo | Forma de Armazenamento |
| :--- | :--- | :--- |
| **Orientado a Documentos** | MongoDB | Documentos JSON/BSON |
| **Chave-Valor** | Redis | Pares simples de chave → valor |
| **Famílias de Colunas** | Cassandra | Colunas agrupadas por família |
| **Orientado a Grafos** | Neo4j | Nós e arestas (relações) |

---

## 🌱 O que é MongoDB?

> **"Mongo"** vem de **Humongous** (gigantesco) — o banco foi projetado desde o início para armazenar e gerenciar **grandes volumes de dados** de forma eficiente.

MongoDB é um banco de dados NoSQL de **código aberto**, **orientado a documentos**. Diferente de bancos relacionais como MySQL ou PostgreSQL, o MongoDB armazena dados em **documentos**, em vez de linhas em tabelas.

---

## 🏗️ Como o MongoDB se Organiza?

A hierarquia de dados no MongoDB segue três níveis:

```
Servidor MongoDB
└── Banco de Dados (Database)
    └── Coleção (Collection)   ← equivale a uma "tabela"
        └── Documento (Document) ← equivale a uma "linha"
```

* Um servidor pode hospedar **múltiplos bancos de dados**.
* Cada banco contém **coleções**, e cada coleção armazena **documentos**.

---

## 📄 Formato BSON (Binary JSON)

Todo registro no MongoDB é um **documento**. Os dados são armazenados em **BSON** (Binary JSON) — uma versão binária do JSON, otimizada para eficiência.

Cada documento é composto por **campos (fields)**, onde cada campo tem um **nome** e um **valor**:

```json
{
  "_id": "ObjectId('abc123')",
  "nome": "Ana Silva",
  "idade": 28,
  "ativo": true,
  "endereco": {
    "cidade": "Salvador",
    "estado": "BA"
  },
  "interesses": ["tecnologia", "música"]
}
```

| Elemento | Descrição |
| :--- | :--- |
| **Field Name** | A chave/nome do campo (ex: `"nome"`). |
| **Value** | O valor do campo — pode ser string, número, booleano, array ou outro documento. |

---

## 🔗 Relacionamentos no MongoDB

> **⚠️ Diferença fundamental:** ao contrário do SQL, o MongoDB **minimiza o uso de JOINs**.

Em vez de dividir dados relacionados em várias tabelas e uni-los depois, o MongoDB armazena esses dados **juntos no mesmo documento** por meio de **documentos incorporados (embedded documents)**:

| Abordagem SQL | Abordagem MongoDB |
| :--- | :--- |
| Dados distribuídos em tabelas separadas. | Dados agrupados dentro do mesmo documento. |
| Unidos via `JOIN` na consulta. | Acessados diretamente, sem `JOIN`. |
| Schema rígido e predefinido. | Schema flexível e adaptável. |

---

## 💻 Primeiros Comandos (mongosh)

```js
mongosh                                         // Abre o shell do MongoDB

show databases                                  // Lista todos os bancos
use shop                                        // Seleciona (ou cria) um banco
show collections                                // Lista as coleções do banco atual

db.createCollection("produtos")                 // Cria uma coleção manualmente
db.produtos.insertOne({ nome: "Notebook" })     // Insere um documento
db.produtos.find()                              // Consulta todos os documentos
```

---

[🏠 Início do Repositório NoSQL](01-introducao-nosql.md)
