
# 🚀 Node.js: Autenticação com JWT

Bem-vindo! Neste guia, você aprenderá a criar uma API simples com autenticação usando JSON Web Tokens (JWT). 🌐

---

## 📝 Sobre o JWT
O JWT (JSON Web Token) é um padrão (RFC 7519) para comunicação segura entre duas partes. Ele é composto por:
- **Cabeçalho**
- **Carga útil**
- **Assinatura**

Um exemplo de token:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoxLCJpYXQiOjE2NDk1MzI4ODMsImV4cCI6MTY0OTUzNjQ4M30.o2AyCJiUkK3iCdbXto0xP6MF97KlyeNHPXw_mMdIQcg
```

---

## ⚙️ Pré-requisitos
Antes de começar, certifique-se de que você tem conhecimentos básicos sobre:
- **Node.js**
- **Express**

Se necessário, confira este artigo sobre APIs com Node.js e Sequelize.

---

## 📂 Estrutura do Projeto
Criamos uma API simples com três endpoints:
1. `/` - Rota pública, acessível a todos.
2. `/login` - Endpoint para autenticação de usuários.
3. `/private` - Rota protegida, acessível apenas com um token válido.

### 🗂️ Estrutura de Arquivos
```
/src
  ├── server.js
  ├── auth.js
```

---

## 📦 Dependências
As bibliotecas utilizadas neste projeto são:
- **express**: Criação de APIs robustas com métodos HTTP e middlewares.
- **jsonwebtoken**: Gerenciamento de tokens JWT.
- **nodemon**: Ferramenta para desenvolvimento com live-reload.

Certifique-se de configurar o `type` como `"module"` no `package.json` para usar `import` e `export` no JavaScript.

---

## 🚧 Implementação

### 🛠️ Configuração do Servidor (`src/server.js`)
- **Rota pública**: Para todos os usuários.
- **Rota de login**: Gera um token usando `jsonwebtoken.sign`.
- **Middleware de validação**: Valida o token antes de acessar rotas protegidas.

Fluxo do login:
1. Dados de autenticação (email e senha) são enviados no header.
2. Validamos os dados recebidos.
3. Geramos o token com:
   - Informações do usuário.
   - Chave secreta (armazenada em `.env`).
   - Configurações adicionais, como tempo de expiração.
4. Retornamos ao cliente o token e as informações do usuário.

### 🔒 Middleware de Autenticação (`src/auth.js`)
O middleware `tokenValidated` realiza:
1. Recuperação do token no header.
2. Validação do token com `jsonwebtoken.verify` usando a chave secreta.
3. Decodificação do token, extraindo informações do usuário.
4. Encaminhamento do fluxo para a rota protegida.

---

## 🛡️ Considerações Finais
- JWT é amplamente utilizado para autenticação em diferentes linguagens.
- Bibliotecas como `jsonwebtoken` facilitam a criação e verificação de tokens.
- Sempre mantenha sua chave secreta protegida (use `.env`).

Explore, experimente e aproveite a segurança e flexibilidade do JWT! ✨
