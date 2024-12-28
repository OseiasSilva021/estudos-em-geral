
# 🚀 MVC - Model-View-Controller (Padrão de Arquitetura)

O **MVC** é um padrão de arquitetura de software que separa a aplicação em três camadas principais: **Model**, **View** e **Controller**. Esse padrão ajuda a manter o código organizado, reutilizável e de fácil manutenção. Vamos explorar cada uma dessas camadas com exemplos! 📚

## 📦 Estrutura do Projeto

Uma aplicação MVC típica tem a seguinte estrutura:

```
/project
  /models    👩‍💻   - Contém a lógica de dados e interação com o banco de dados
  /views     🖥️   - Exibe a interface do usuário
  /controllers 📂 - Controla a interação entre o modelo e a visão
  /public      🌐 - Arquivos públicos (CSS, JS, imagens)
```

## 🏗️ Camadas do MVC

### 1. **Model** (Modelo) 🧩
O **Model** é responsável por gerenciar os dados da aplicação. Ele pode interagir com o banco de dados, fazer validações e fornecer dados para a **View**.

#### Exemplo:
```javascript
// models/User.js

const db = require('../db'); // Conexão com o banco de dados

class User {
  static async findAll() {
    const users = await db.query('SELECT * FROM users');
    return users;
  }

  static async create(name, email) {
    const newUser = await db.query('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);
    return newUser;
  }
}

module.exports = User;
```

### 2. **View** (Visão) 🖼️
A **View** é responsável por exibir os dados para o usuário. Pode ser composta por HTML, CSS e JavaScript. A **View** recebe dados do **Controller** e os apresenta de forma interativa.

#### Exemplo:
```html
<!-- views/users.ejs -->

<h1>Lista de Usuários</h1>
<ul>
  <% users.forEach(function(user) { %>
    <li><%= user.name %> - <%= user.email %></li>
  <% }); %>
</ul>
```

### 3. **Controller** (Controlador) 🕹️
O **Controller** atua como um intermediário entre o **Model** e a **View**. Ele processa a entrada do usuário, chama os métodos do **Model** e escolhe qual **View** será exibida.

#### Exemplo:
```javascript
// controllers/UserController.js

const User = require('../models/User');
const path = require('path');

class UserController {
  static async list(req, res) {
    const users = await User.findAll(); // Obtendo os dados do Model
    res.render('users', { users });     // Enviando os dados para a View
  }

  static async create(req, res) {
    const { name, email } = req.body;
    await User.create(name, email); // Criando um novo usuário
    res.redirect('/users');         // Redirecionando para a lista de usuários
  }
}

module.exports = UserController;
```

## 🔄 Fluxo de Dados no MVC

1. O **usuário** faz uma **requisição** para o **Controller**.
2. O **Controller** consulta ou manipula o **Model** para obter ou alterar os dados.
3. O **Controller** envia os dados para a **View** exibir.
4. A **View** apresenta os dados ao **usuário**.

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
Abra o navegador e acesse `http://localhost:3000/users` para ver a lista de usuários.

## 🔧 Dicas e Recomendações

- Use o **MVC** para organizar seu código de forma modular e escalável. 📈
- Mantenha **Models** simples e focados na manipulação de dados. 🧑‍💻
- A **View** deve ser o mais simples possível, apenas exibindo os dados. 💡
- O **Controller** deve ser responsável apenas pela lógica de controle. Evite lógica de negócios diretamente nele. ⚙️

## 📚 Conclusão

O padrão **MVC** ajuda a separar a lógica de uma aplicação em três partes independentes, facilitando a manutenção e escalabilidade. Quando implementado corretamente, ele melhora a organização e a clareza do código! 🚀

---
### 📝 Feito com ❤️ e muito código!

Esse `README.md` explica o básico sobre o padrão MVC, mostrando como as camadas se interagem e fornecendo exemplos de código para cada uma delas. Ele também inclui emojis para tornar o conteúdo mais dinâmico e fácil de entender.
