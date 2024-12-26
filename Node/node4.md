# Trabalhando com **Express.js** 🌐🚀

**Express.js** é um framework minimalista para **Node.js**, amplamente utilizado para criar aplicações web e **API**s. Ele simplifica o processo de manipulação de rotas, requisições, respostas e muito mais. 💻⚡

## 1. Instalando e Configurando o Express ⚙️🔧

Para começar a usar o **Express.js**, siga os passos abaixo:

### Passos para instalação 📝

1. **Instalar o **Node.js** 🔻 se ainda não tiver:
   - Baixe e instale a versão mais recente do [**Node.js**](https://nodejs.org/).

2. **Criar um novo diretório para o seu projeto** 📂 e inicializar o `package.json`:
   ```bash
   mkdir meu-projeto 🏗️
   cd meu-projeto 🚀
   npm init -y 🧰
   ```

3. **Instalar o Express** ⚡:
   ```bash
   npm install express 💼
   ```

4. **Criar o arquivo `app.js`** 🖥️ para configurar o servidor:
   ```javascript
   const express = require('express');
   const app = express();
   const port = 3000;

   app.get('/', (req, res) => {
       res.send('Olá Mundo! 🌎');
   });

   app.listen(port, () => {
       console.log(`Servidor rodando na porta ${port} 🚀`);
   });
   ```

5. **Executar o servidor** 🎮:
   ```bash
   node app.js 🚀
   ```

Agora, ao acessar `http://localhost:3000`, você verá "Olá Mundo! 🌎". 😎

---

## 2. Criando Rotas e Middleware 🔄

### 2.1. Criando Rotas 🛣️

Express permite criar rotas para diferentes métodos HTTP. Exemplo:

```javascript
app.get('/usuarios', (req, res) => {
    res.send('Lista de usuários 👥');
});

app.post('/usuarios', (req, res) => {
    res.send('Criando usuário 🛠️');
});
```

### 2.2. Middleware 🔧

O middleware é uma função que tem acesso ao objeto de requisição (`req`), objeto de resposta (`res`) e à próxima função de middleware no ciclo de requisição-resposta. Ele pode ser usado para modificar os dados da requisição, validar informações ou até mesmo interromper o fluxo da requisição.

#### Middleware global 🌍:

```javascript
app.use((req, res, next) => {
    console.log('Requisição recebida 📩');
    next();
});
```

#### Middleware específico para uma rota 📍:

```javascript
app.get('/usuarios', (req, res, next) => {
    console.log('Acessando rota de usuários 🔍');
    next();
}, (req, res) => {
    res.send('Lista de usuários 👥');
});
```

---

## 3. Trabalhando com Parâmetros de URL, Query Strings e Corpo das Requisições 🌐📊

### 3.1. Parâmetros de URL 🛣️

Para capturar parâmetros na URL, use o `req.params`:

```javascript
app.get('/usuarios/:id', (req, res) => {
    const usuarioId = req.params.id;
    res.send(`Usuário com ID: ${usuarioId} 👤`);
});
```

### 3.2. Query Strings 🔎

Parâmetros passados na URL após `?` são chamados de query strings. Acesse-os com `req.query`:

```javascript
app.get('/pesquisar', (req, res) => {
    const nome = req.query.nome;
    res.send(`Buscando por: ${nome} 🔍`);
});
```

### 3.3. Corpo das Requisições 💌

Para acessar o corpo da requisição (com dados enviados pelo usuário), use `req.body`. Para isso, você precisa instalar e configurar um middleware como `express.json()` ou `express.urlencoded()`:

- **Configuração para JSON**:
  ```javascript
  app.use(express.json() 🧳);
  ```

- **Exemplo de requisição POST com corpo JSON**:
  ```javascript
  app.post('/usuarios', (req, res) => {
      const usuario = req.body;
      res.send(`Usuário recebido: ${JSON.stringify(usuario)} 👤`);
  });
  ```

---

## 4. Respondendo com JSON, HTML e Arquivos Estáticos 🖼️🎨

### 4.1. Resposta JSON 📦

Para enviar uma resposta JSON, use `res.json()`:

```javascript
app.get('/usuario', (req, res) => {
    res.json({ id: 1, nome: 'João' 📛 });
});
```

### 4.2. Resposta HTML 🖋️

Para enviar HTML como resposta, use `res.send()` com o conteúdo HTML:

```javascript
app.get('/pagina', (req, res) => {
    res.send('<h1>Bem-vindo à página! 🖥️</h1>');
});
```

### 4.3. Servindo Arquivos Estáticos 📁

Para servir arquivos como imagens, CSS ou JavaScript, use o middleware `express.static`:

```javascript
app.use(express.static('public 🏙️'));
```

Isso permitirá acessar arquivos na pasta `public` diretamente pela URL, por exemplo, `http://localhost:3000/imagem.jpg` 🖼️.

---

## 5. Autenticação e Autorização 🔑🔒

### 5.1. Implementando Login com JWT 🔑

Para autenticar usuários com JSON Web Tokens (JWT), você pode usar bibliotecas como `jsonwebtoken`. Instale com:

```bash
npm install jsonwebtoken 🧳
```

#### Exemplo de Login:

```javascript
const jwt = require('jsonwebtoken');

app.post('/login', (req, res) => {
    const usuario = req.body;
    // Valide as credenciais do usuário...
    const token = jwt.sign({ id: usuario.id }, 'secreta_chave 🔐', { expiresIn: '1h' });
    res.json({ token });
});
```

### 5.2. Criando Middleware de Autenticação 🔑

Para proteger rotas, crie um middleware que verifique o token JWT:

```javascript
const autenticar = (req, res, next) => {
    const token = req.headers['authorization'];

    if (!token) {
        return res.status(403).send('Token não fornecido 🚫');
    }

    jwt.verify(token, 'secreta_chave 🔑', (err, decoded) => {
        if (err) {
            return res.status(403).send('Token inválido ❌');
        }
        req.userId = decoded.id;
        next();
    });
};

app.get('/perfil', autenticar, (req, res) => {
    res.send(`Perfil do usuário ${req.userId} 🧑‍💼`);
});
```

---

## 6. Validação de Dados ✅🔍

### 6.1. Usando express-validator 📝

O `express-validator` é uma ferramenta poderosa para validar dados de entrada. Instale com:

```bash
npm install express-validator 🧳
```

#### Exemplo de Validação de Dados:

```javascript
const { body, validationResult } = require('express-validator');

app.post('/usuarios', [
    body('email').isEmail().withMessage('Email inválido ❌'),
    body('nome').notEmpty().withMessage('Nome é obrigatório ⚠️')
], (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }
    res.send('Usuário criado 🆙');
});
```

### 6.2. Usando Joi 📝

O Joi é outra opção popular para validação de dados. Instale com:

```bash
npm install joi 🧳
```

#### Exemplo de Validação com Joi:

```javascript
const Joi = require('joi');

const schema = Joi.object({
    email: Joi.string().email().required(),
    nome: Joi.string().required()
});

app.post('/usuarios', (req, res) => {
    const { error } = schema.validate(req.body);
    if (error) {
        return res.status(400).send(error.details[0].message);
    }
    res.send('Usuário criado 🆙');
});
```

---

## Conclusão 🎉

Com o **Express.js** 🚀, você pode facilmente criar aplicações web e **API**s robustas. Utilizando rotas 🛣️, middleware 🔧, validação de dados 📝 e autenticação 🔑, você garante que sua aplicação seja eficiente, segura e escalável. 🌍👨‍💻
