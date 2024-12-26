# Banco de Dados 📊

Este guia aborda como conectar e trabalhar com bancos de dados relacionais (**MySQL**/**PostgreSQL**) e não relacionais (MongoDB) em Node.js, utilizando ORMs como Sequelize e TypeORM, além de explorar operações CRUD e conceitos de modelagem de banco de dados.

## Conectando com Bancos de Dados Relacionais (**MySQL**/**PostgreSQL**) 🗄️

### **MySQL** / **PostgreSQL** 💻

Os bancos de dados relacionais como **MySQL** e **PostgreSQL** são amplamente utilizados no desenvolvimento de aplicações web 🌐. Para interagir com esses bancos de dados no Node.js, utilizamos bibliotecas como `mysql2` (para **MySQL**) ou `pg` (para **PostgreSQL**) 🔌.

#### Exemplo de conexão com MySQL:

```javascript
const mysql = require('mysql2');

// Criar conexão com o banco de dados
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'meu_banco'
});

// Conectar ao banco
connection.connect((err) => {
  if (err) {
    console.error('Erro de conexão: ' + err.stack);
    return;
  }
  console.log('Conectado como id ' + connection.threadId);
});
```

### Usando ORMs (Sequelize / TypeORM) 🔧

#### Sequelize 🔄

O **Sequelize** é um ORM para Node.js que facilita a interação com bancos de dados relacionais, permitindo que você trabalhe com modelos de dados e abstraia a sintaxe SQL em código JavaScript ✨.

**Instalar Sequelize e mysql2:** 🛠️

```bash
npm install sequelize mysql2
```

#### Exemplo com Sequelize:

```javascript
const { Sequelize, DataTypes } = require('sequelize');

// Conexão com o banco de dados
const sequelize = new Sequelize('meu_banco', 'root', 'password', {
  host: 'localhost',
  dialect: 'mysql',
});

// Definir um modelo
const Usuario = sequelize.define('Usuario', {
  nome: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  email: {
    type: DataTypes.STRING,
    unique: true,
  },
});

// Sincronizar o modelo com o banco
sequelize.sync();
```

### Operações CRUD com Sequelize 🔄

- **Create (Criar):** 🆕

```javascript
Usuario.create({ nome: 'João', email: 'joao@example.com' });
```

- **Read (Ler):** 👀

```javascript
Usuario.findAll().then(users => console.log(users));
```

- **Update (Atualizar):** 🔄

```javascript
Usuario.update({ nome: 'João Atualizado' }, {
  where: { id: 1 }
});
```

- **Delete (Deletar):** 🗑️

```javascript
Usuario.destroy({
  where: { id: 1 }
});
```

## Banco de Dados NoSQL (MongoDB) 🌳

O **MongoDB** é um banco de dados NoSQL, onde os dados são armazenados em documentos JSON (chave-valor), sem a necessidade de tabelas e relações 📑.

### Instalando e Usando o Mongoose 🛠️

O **Mongoose** é uma biblioteca para trabalhar com MongoDB em Node.js, proporcionando uma camada de abstração para interagir com o banco de dados de maneira estruturada 🔐.

**Instalar Mongoose:** 🛠️

```bash
npm install mongoose
```

#### Exemplo de Conexão com MongoDB:

```javascript
const mongoose = require('mongoose');

// Conectar ao MongoDB
mongoose.connect('mongodb://localhost:27017/meu_banco', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('Conectado ao MongoDB'))
  .catch(err => console.error('Erro de conexão', err));

// Definir um modelo
const usuarioSchema = new mongoose.Schema({
  nome: String,
  email: { type: String, unique: true }
});

const Usuario = mongoose.model('Usuario', usuarioSchema);
```

### Operações CRUD com MongoDB 🔄

- **Create (Criar):** 🆕

```javascript
const novoUsuario = new Usuario({ nome: 'Maria', email: 'maria@example.com' });
novoUsuario.save();
```

- **Read (Ler):** 👀

```javascript
Usuario.find().then(users => console.log(users));
```

- **Update (Atualizar):** 🔄

```javascript
Usuario.updateOne({ _id: 'id_do_usuario' }, { nome: 'Maria Atualizada' });
```

- **Delete (Deletar):** 🗑️

```javascript
Usuario.deleteOne({ _id: 'id_do_usuario' });
```

## Conceitos de Modelagem de Banco de Dados 🧠

A modelagem de banco de dados envolve definir como os dados serão estruturados e como as diferentes entidades se relacionam entre si 🔄. Aqui estão os principais conceitos:

### 1. Relacionamentos entre Tabelas 🔗

- **1:1 (Um para Um):** Quando um registro de uma tabela está relacionado com um único registro de outra tabela. Exemplo: uma pessoa tem um único passaporte 👤📜.
- **1:N (Um para Muitos):** Quando um registro de uma tabela pode estar relacionado com múltiplos registros de outra tabela. Exemplo: um autor pode ter vários livros 📚✍️.
- **N:N (Muitos para Muitos):** Quando múltiplos registros de uma tabela podem estar relacionados com múltiplos registros de outra tabela. Exemplo: alunos podem se matricular em várias disciplinas e cada disciplina pode ter vários alunos 🎓📚.

### 2. Indexação e Consultas Eficientes 🚀

A indexação é o processo de criar índices para facilitar a busca rápida por dados específicos em uma tabela 🔍. Sem índices, o banco de dados precisa fazer uma busca linear por todas as entradas, o que pode ser muito lento em tabelas grandes 🐢.

#### Exemplo de criação de índice em MySQL:

```sql
CREATE INDEX idx_email ON usuarios (email);
```

#### Exemplo de criação de índice em MongoDB:

```javascript
Usuario.createIndex({ email: 1 });
```

Ao usar índices, é importante considerar o impacto no desempenho das operações de inserção e atualização, pois os índices precisam ser atualizados cada vez que um novo registro é adicionado ou modificado ⚡.

## Conclusão 🎯

- **Bancos de Dados Relacionais (MySQL/**PostgreSQL**)** são ideais quando a estrutura dos dados é bem definida e as relações entre as entidades são claras 🔑.
- **Bancos de Dados NoSQL (MongoDB)** são úteis quando a estrutura dos dados é flexível e o volume de dados é grande 📈.
- **ORMs** como `Sequelize` e `TypeORM` tornam o trabalho com bancos relacionais mais fácil e abstrato 🔧, enquanto o `mongoose` facilita a interação com o MongoDB 🌱.
- **Modelagem de Banco de Dados** é crucial para garantir que seus dados sejam organizados de forma eficiente, permitindo escalabilidade e otimização de consultas ⚙️.