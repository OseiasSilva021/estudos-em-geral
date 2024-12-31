# ✨ Criando uma App CRUD com Node.js + MongoDB ✨

**Autor:** Pedro Pinto  
**Data:** Março 28, 2019  

## 🚀 Introdução

Node.js é um interpretador de código JavaScript que opera no lado do servidor. Essa plataforma permite criar aplicações de alta escalabilidade de forma simples e rápida. Ele é baseado no interpretador V8 da Google.

Neste tutorial, vamos criar uma aplicação CRUD (Create, Read, Update e Delete) para registro de smartphones usando Node.js e MongoDB.

---

## 🔬 Estrutura do Tutorial

1. ✅ O que é CRUD
2. 🔮 Arquitetura REST
3. 📊 MongoDB — O que é?
4. ⚡ Vamos Começar:
   - Instalar o Node.js
   - Criar um diretório para o projeto
   - Iniciar o projeto
   - Instalar pacotes necessários
5. 🎨 Organização MVC
6. 📝 Criação dos Endpoints

---

## 🔢 O que significa CRUD?

CRUD é um acrônimo que representa:

- **Create**: Inserir dados (INSERT)
- **Read**: Ler dados (SELECT)
- **Update**: Atualizar dados (UPDATE)
- **Delete**: Excluir dados (DELETE)

---

## 🔄 Arquitetura REST

**REST (REpresentational State Transfer)** é uma arquitetura que utiliza o protocolo HTTP para comunicação. A representação de recursos geralmente é feita em JSON. 

Para mais informações, consulte a [documentação REST](https://restfulapi.net/).

---

## 📂 O que é MongoDB?

MongoDB é um banco de dados NoSQL que armazena informações em documentos JSON, sem esquemas fixos, permitindo maior flexibilidade e escalabilidade.

---

## ⚡ Vamos Começar!

### 1. 🛠️ Instalar o Node.js

Execute os comandos abaixo no terminal:

```bash
sudo apt-get update
sudo apt-get install nodejs
```

### 2. 🔨 Criar Diretório para o Projeto

```bash
mkdir smartphones_app
cd smartphones_app
```

### 3. 📚 Iniciar o Projeto

Inicie o projeto com o comando:

```bash
npm init
```

Isso gerará um arquivo `package.json` com as informações do projeto.

### 4. 🔹 Instalar Pacotes Necessários

Instale os seguintes pacotes:

```bash
npm install --save express body-parser mongoose
```

---

## 🎨 Organização da Aplicação (MVC)

A estrutura da aplicação seguirá o padrão MVC (Model, View, Controller):

```
smartphones_app/
├── controllers
├── models
├── routes
├── views
```

Crie essas pastas com o comando:

```bash
mkdir -p controllers models routes views
```

### Criando o Model

No diretório `models`, crie o arquivo `smartphones.model.js` com o seguinte código:

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

let SmartphoneSchema = new Schema({
    nome: { type: String, required: true, max: 100 },
    marca: { type: String, required: true },
});

module.exports = mongoose.model('Smartphone', SmartphoneSchema);
```

### Criando as Rotas

No diretório `routes`, crie o arquivo `smartphones.route.js` com o seguinte código:

```javascript
const express = require('express');
const router = express.Router();

const smartphone_controller = require('../controllers/smartphone.controller');

router.get('/testar', smartphone_controller.test);
module.exports = router;
```

### Criando o Controller

No diretório `controllers`, crie o arquivo `smartphones.controller.js`:

```javascript
var Smartphone = require('../models/smartphones.model');

exports.test = function (req, res) {
    res.send('Olá! Teste ao Controller');
};
```

### Integrando com o Servidor

No arquivo principal `index.js`, configure as rotas e o servidor:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const smartphones = require('./routes/smartphones.route');

const app = express();
let porto = 8000;

// Configuração da Base de Dados
let mongoDB = 'mongodb://bd_user:abcd1234@ds111234.mlab.com:123213/smartphones';
mongoose.connect(mongoDB, { useNewUrlParser: true });
mongoose.Promise = global.Promise;

// Middleware
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
app.use('/smartphones', smartphones);

// Inicialização do Servidor
app.listen(porto, () => {
    console.log('Servidor em execução no porto ' + porto);
});
```

---

## 🔧 Testando a App

Para testar, inicie o servidor com:

```bash
node index.js
```

Acesse no navegador ou Postman:

```
http://localhost:8000/smartphones/testar
```

Se você visualizar a mensagem "Olá! Teste ao Controller", sua rota está funcionando! ✨

---

## 🌐 Conclusão

Você configurou um projeto Node.js, conectou-o ao MongoDB e implementou a estrutura MVC. Agora você pode expandir sua aplicação criando endpoints para Create, Read, Update e Delete! 🎉

