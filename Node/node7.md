# Testes em JavaScript 🧪

Este documento detalha como realizar **Testes Unitários** 🧑‍💻, **Testes de Integração** 🔗 e **Testes E2E** (**End-to-End**) 🌐 em JavaScript, utilizando frameworks populares como **Jest** ⚡, **Mocha** 🕰️ e **Supertest** 🚀.

## 1. Testes Unitários e de Integração 🔍

### Testes Unitários 🧑‍🔬

Os **testes unitários** são fundamentais para garantir que unidades isoladas de código, como funções, métodos ou classes, se comportem como esperado. O objetivo principal é testar o comportamento de uma única unidade de código sem dependências externas.

#### Exemplo de Teste Unitário com Jest

```javascript
// função a ser testada
function somar(a, b) {
  return a + b;
}

// teste unitário
test('soma 1 + 2 para igualar a 3', () => {
  expect(somar(1, 2)).toBe(3);
});
```

O Jest fornece uma API simples de asserções, mocks e spies para testes, tornando-o uma excelente escolha para testar unidades de código.

### Testes de Integração 🔄

**Testes de Integração** verificam se diferentes módulos ou unidades de código interagem corretamente entre si. Eles são úteis para testar como o sistema reage a diferentes interações entre os componentes.

#### Exemplo de Teste de Integração com Jest

```javascript
// Supondo que temos uma função que faz uma chamada para a API
async function pegarUsuarios() {
  const resposta = await fetch('/api/usuarios');
  return resposta.json();
}

test('deve retornar a lista de usuários', async () => {
  const usuarios = await pegarUsuarios();
  expect(usuarios).toHaveLength(3);
});
```

### Testando Rotas, Controladores e Middlewares 🚏

No contexto de APIs, é importante testar as rotas 🚀, controladores 🧑‍💻 e middlewares 🛠️ para garantir que eles funcionem conforme esperado.

#### Exemplo de Teste de Rota com Jest e Supertest

```javascript
const request = require('supertest');
const app = require('../app'); // Supondo que seu app Express está em 'app.js'

describe('GET /usuarios', () => {
  it('deve retornar status 200 e uma lista de usuários', async () => {
    const response = await request(app).get('/usuarios');
    expect(response.status).toBe(200);
    expect(response.body).toBeInstanceOf(Array);
  });
});
```

#### Exemplo de Teste de Middleware

```javascript
// middleware de autenticação
function verificarAutenticacao(req, res, next) {
  if (!req.headers.authorization) {
    return res.status(401).send('Não autorizado');
  }
  next();
}

// teste do middleware
test('deve retornar 401 sem token de autenticação', () => {
  const req = { headers: {} };
  const res = { status: jest.fn().mockReturnThis(), send: jest.fn() };
  const next = jest.fn();

  verificarAutenticacao(req, res, next);
  expect(res.status).toHaveBeenCalledWith(401);
  expect(res.send).toHaveBeenCalledWith('Não autorizado');
});
```

## 2. Testes E2E (**End-to-End**) 🔄🌍

Os testes **E2E** (**End-to-End**) visam garantir que o sistema funcione como um todo, testando a interação completa entre os componentes, incluindo front-end 👨‍💻 e back-end 🖥️.

### Testando APIs Completa com Supertest 🚀

**Supertest** é uma ferramenta poderosa para testar APIs HTTP, permitindo enviar requisições HTTP a servidores e verificar as respostas de maneira simples e eficaz.

#### Exemplo de Teste E2E com Supertest

```javascript
const request = require('supertest');
const app = require('../app'); // Seu aplicativo Express

describe('POST /login', () => {
  it('deve retornar token quando credenciais forem válidas', async () => {
    const response = await request(app)
      .post('/login')
      .send({ usuario: 'usuario_teste', senha: 'senha_teste' });
    expect(response.status).toBe(200);
    expect(response.body.token).toBeDefined();
  });
});
```

### Testando Fluxos Completos 🔁

Além de testar endpoints isolados, é importante testar fluxos completos que simulem interações reais dos usuários. Por exemplo, ao testar o fluxo de cadastro e login de usuários, você pode realizar os seguintes passos:

1. Enviar dados para o endpoint de cadastro 📝.
2. Verificar se o usuário foi criado ✅.
3. Enviar dados de login 🔑.
4. Verificar se o login retorna um token de autenticação válido ✅.

#### Exemplo de Fluxo Completo com Supertest

```javascript
describe('Fluxo de cadastro e login', () => {
  it('deve cadastrar e logar um usuário', async () => {
    // Cadastro
    let response = await request(app)
      .post('/cadastro')
      .send({ nome: 'Usuário Teste', email: 'teste@teste.com', senha: '12345' });
    expect(response.status).toBe(201);

    // Login
    response = await request(app)
      .post('/login')
      .send({ email: 'teste@teste.com', senha: '12345' });
    expect(response.status).toBe(200);
    expect(response.body.token).toBeDefined();
  });
});
```

## 3. Boas Práticas para Testes 📚

- **Escreva testes claros e objetivos** ✍️: O objetivo é que os testes sejam legíveis e que você possa entender rapidamente o que está sendo testado.
- **Testes isolados** 🧑‍🔬: Teste componentes de forma isolada, usando mocks e stubs para evitar dependências externas como bancos de dados 🏦.
- **Cobertura de testes** 🛡️: Tente cobrir o maior número possível de casos de uso, incluindo testes de borda, como entradas inválidas ⚠️.
- **Rodar os testes frequentemente** 🔄: Execute os testes sempre que modificar o código para garantir que nada foi quebrado.

## 4. Conclusão 🎉

Testes são fundamentais para garantir a confiabilidade e a qualidade de qualquer sistema 🏆. O uso de ferramentas como **Jest** ⚡, **Mocha** 🕰️ e **Supertest** 🚀 ajuda a facilitar a escrita e execução dos testes, garantindo que seu código esteja sempre funcionando conforme o esperado, seja em unidades isoladas 🧑‍🔬, integrações entre componentes 🔗 ou fluxos completos 🌍.