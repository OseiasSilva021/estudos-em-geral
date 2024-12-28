
# 🌐 Arquitetura para Criação de APIs

A criação de uma **API** (Interface de Programação de Aplicações) bem estruturada é essencial para garantir que seu sistema seja escalável, eficiente e fácil de manter. Neste guia, vamos explorar uma arquitetura moderna e limpa para a construção de APIs RESTful, com exemplos práticos! 📚

## 📦 Estrutura do Projeto

Uma boa organização do projeto é a chave para uma API bem estruturada. Aqui está um exemplo de como você pode organizar seus arquivos e pastas:

```
/project
  /controllers   📂   - Controladores que lidam com as requisições
  /models        🧩   - Modelos de dados e interações com o banco
  /routes        🛤️   - Definição das rotas da API
  /services      🔧   - Lógica de negócios e regras específicas
  /middlewares   🔒   - Validações, autenticação, etc.
  /config        ⚙️   - Configurações do projeto (banco de dados, variáveis, etc.)
  /utils         ⚡   - Funções utilitárias e helpers
  /public        🌐   - Arquivos públicos (se necessário)
  /tests         ✅   - Testes automatizados
```

## 🧩 Camadas da Arquitetura

### 1. **Models** (Modelos) 🏗️
Os **Models** são responsáveis pela representação dos dados e interações com o banco de dados. Eles geralmente definem a estrutura dos dados e os métodos para manipulação dessas informações.

#### Exemplo:
```javascript
// models/User.js

const db = require('../config/db'); // Conexão com o banco de dados

class User {
  static async findAll() {
    const users = await db.query('SELECT * FROM users');
    return users;
  }

  static async findById(id) {
    const user = await db.query('SELECT * FROM users WHERE id = ?', [id]);
    return user;
  }

  static async create(name, email) {
    const newUser = await db.query('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);
    return newUser;
  }
}

module.exports = User;
```

### 2. **Controllers** (Controladores) 🎮
Os **Controllers** lidam com as requisições HTTP recebidas pela API. Eles recebem os dados da requisição, chamam os **Models** para interagir com os dados e enviam a resposta para o cliente.

#### Exemplo:
```javascript
// controllers/UserController.js

const User = require('../models/User');

class UserController {
  static async getUsers(req, res) {
    try {
      const users = await User.findAll(); // Busca todos os usuários
      res.status(200).json(users);         // Envia a resposta em JSON
    } catch (error) {
      res.status(500).json({ error: 'Erro ao obter usuários' });
    }
  }

  static async createUser(req, res) {
    const { name, email } = req.body;
    try {
      const newUser = await User.create(name, email); // Criação de um novo usuário
      res.status(201).json(newUser);                   // Retorna o usuário criado
    } catch (error) {
      res.status(500).json({ error: 'Erro ao criar usuário' });
    }
  }
}

module.exports = UserController;
```

### 3. **Routes** (Rotas) 🛤️
As **Routes** definem os endpoints da API e as ações que cada rota realiza. Elas fazem a conexão entre a requisição e o **Controller** adequado.

#### Exemplo:
```javascript
// routes/userRoutes.js

const express = require('express');
const UserController = require('../controllers/UserController');

const router = express.Router();

router.get('/users', UserController.getUsers);     // Rota para obter todos os usuários
router.post('/users', UserController.createUser);  // Rota para criar um novo usuário

module.exports = router;
```

### 4. **Services** (Serviços) ⚙️
Os **Services** contêm a lógica de negócios mais complexa. Eles podem ser usados para organizar regras de validação, manipulação de dados ou chamadas externas à API.

#### Exemplo:
```javascript
// services/UserService.js

class UserService {
  static validateUserData(name, email) {
    if (!name || !email) {
      throw new Error('Nome e e-mail são obrigatórios');
    }
    // Adicione outras validações conforme necessário
  }
}

module.exports = UserService;
```

### 5. **Middlewares** (Middleware) 🔒
Os **Middlewares** são funções que têm acesso à requisição, resposta e próximo middleware. Eles são úteis para autenticação, validação de dados, log de requisições, etc.

#### Exemplo:
```javascript
// middlewares/authMiddleware.js

const jwt = require('jsonwebtoken');

function authenticate(req, res, next) {
  const token = req.header('Authorization');
  if (!token) {
    return res.status(401).json({ error: 'Acesso negado. Token não fornecido.' });
  }
  try {
    const verified = jwt.verify(token, process.env.JWT_SECRET);
    req.user = verified;
    next(); // Passa para o próximo middleware ou rota
  } catch (error) {
    res.status(400).json({ error: 'Token inválido.' });
  }
}

module.exports = authenticate;
```

## 🔄 Fluxo de Requisição

1. O **Cliente** faz uma requisição para um endpoint da **API** (por exemplo, `GET /users`).
2. A **Rota** direciona a requisição para o **Controller** apropriado.
3. O **Controller** chama o **Model** para manipular ou buscar os dados.
4. O **Service** pode ser chamado para validar ou processar dados.
5. O **Controller** envia a resposta para o **Cliente**.

## 💻 Como Rodar o Exemplo?

### 1. Instale as dependências
```bash
npm install
```

### 2. Inicie o servidor
```bash
npm start
```

### 3. Acesse no seu navegador
- **GET**: Acesse `http://localhost:3000/users` para obter todos os usuários.
- **POST**: Use uma ferramenta como Postman para enviar uma requisição **POST** para `http://localhost:3000/users` com um corpo JSON contendo `{ "name": "João", "email": "joao@example.com" }` para criar um novo usuário.

## 🔧 Dicas e Recomendações

- **Organize bem seu código**: Mantenha a separação clara entre as camadas (Controllers, Models, Services) para facilitar a manutenção. 🧹
- **Autenticação e Autorização**: Use **JWT** ou **OAuth** para proteger seus endpoints sensíveis. 🔒
- **Valide sempre os dados**: Nunca confie nas entradas dos usuários. Use validações adequadas no **Controller** ou **Middleware**. ✅
- **Documente sua API**: Utilize ferramentas como o **Swagger** para criar uma documentação interativa da sua API. 📖

## 📚 Conclusão

A criação de uma API bem estruturada envolve separar a lógica da aplicação em camadas, garantindo que o código seja modular, escalável e fácil de manter. O uso de boas práticas, como a separação de responsabilidades entre Models, Controllers e Services, ajudará a tornar sua API mais robusta e organizada! 🚀

---
### 📝 Feito com ❤️ e muito código!


Este `README.md` fornece uma explicação clara sobre a arquitetura para criação de APIs RESTful, com exemplos práticos e emojis para tornar o conteúdo mais envolvente e fácil de entender.
