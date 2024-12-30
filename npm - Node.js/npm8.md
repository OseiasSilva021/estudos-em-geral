
# 🚨 Erros Especificados pelo Usuário no Node.js

Em Node.js, você pode criar seus próprios tipos de erro personalizados, estendendo o objeto `Error` base. Isso é útil quando você deseja lançar erros específicos para o seu aplicativo com mensagens e comportamentos personalizados.

---

## 🛠️ Criando Erros Especificados pelo Usuário

Os erros personalizados podem ser criados estendendo a classe `Error`, que é a classe de erro interna do JavaScript. Isso permite que você adicione propriedades adicionais e forneça mensagens de erro mais específicas para o seu aplicativo.

### 1️⃣ **Estrutura Básica de um Erro Personalizado**

Para criar um erro personalizado, você pode estender a classe `Error` e adicionar a propriedade `message`, que descreve o erro. Também podemos adicionar outras propriedades, como `code` ou `status`, dependendo das necessidades do seu aplicativo.

```javascript
class MeuErroPersonalizado extends Error {
  constructor(message) {
    super(message); // Chama o construtor da classe Error
    this.name = this.constructor.name; // Define o nome do erro como o nome da classe
    this.stack = (new Error()).stack; // Captura o stack trace
  }
}
```

### 2️⃣ **Exemplo de Uso de um Erro Personalizado**

Agora que você tem uma classe de erro personalizada, pode lançar esse erro quando algo inesperado acontecer em seu aplicativo.

```javascript
function divisao(a, b) {
  if (b === 0) {
    throw new MeuErroPersonalizado('Não é possível dividir por zero!');
  }
  return a / b;
}

try {
  console.log(divisao(10, 0));
} catch (error) {
  console.error(`${error.name}: ${error.message}`);
  console.error(error.stack);
}
```

**Saída esperada:**
```
MeuErroPersonalizado: Não é possível dividir por zero!
    at divisao (app.js:4:11)
    at Object.<anonymous> (app.js:8:9)
    at Module._compile (node:internal/modules/cjs/loader:1217:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1271:10)
    at Module.load (node:internal/modules/cjs/loader:1053:32)
    at Function.Module._load (node:internal/modules/cjs/loader:896:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:81:12)
    at node:internal/modules/run_main:23:47
```

### 3️⃣ **Adicionando Mais Propriedades Personalizadas**

Além da `message`, você pode adicionar outras propriedades personalizadas que ajudam a tornar o erro mais informativo. Por exemplo, você pode adicionar um código de erro ou um status HTTP.

```javascript
class ErroAutenticacao extends Error {
  constructor(message) {
    super(message);
    this.name = this.constructor.name;
    this.statusCode = 401; // Código HTTP para "Não autorizado"
    this.stack = (new Error()).stack;
  }
}
```

Agora, ao lançar o erro:

```javascript
throw new ErroAutenticacao('Falha na autenticação!');
```

O erro terá uma `statusCode` de 401, o que pode ser útil ao lidar com erros em uma API, por exemplo.

### 4️⃣ **Exemplo Completo de Erro Personalizado em uma API**

Se você estiver criando uma API e deseja lançar erros personalizados, pode criar uma classe de erro específica para diferentes tipos de erros, como erros de validação ou de autenticação.

```javascript
class ErroValidacao extends Error {
  constructor(message) {
    super(message);
    this.name = this.constructor.name;
    this.statusCode = 400; // Código HTTP para "Bad Request"
    this.stack = (new Error()).stack;
  }
}

function validaEmail(email) {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!regex.test(email)) {
    throw new ErroValidacao('Email inválido!');
  }
  return true;
}

try {
  validaEmail('emailinvalido@com');
} catch (error) {
  console.error(`${error.name} (${error.statusCode}): ${error.message}`);
}
```

**Saída esperada:**
```
ErroValidacao (400): Email inválido!
```

---

## 🧑‍💻 Como Manipular Erros Personalizados

Ao criar erros personalizados, você pode manipulá-los de maneira mais eficaz em seu código. Aqui estão algumas abordagens para lidar com esses erros:

### 1️⃣ **Verificação do Nome do Erro**

Como você está criando um erro personalizado, é possível verificar o tipo de erro usando a propriedade `name`.

```javascript
try {
  throw new ErroAutenticacao('Falha na autenticação');
} catch (error) {
  if (error instanceof ErroAutenticacao) {
    console.error(`Erro de autenticação: ${error.message}`);
  } else {
    console.error('Erro desconhecido:', error);
  }
}
```

### 2️⃣ **Tratamento Global de Erros**

Você também pode configurar um tratamento global de erros, por exemplo, em uma aplicação Express.js, para capturar erros personalizados e enviar respostas adequadas.

```javascript
const express = require('express');
const app = express();

// Simula um erro de autenticação
app.get('/login', (req, res, next) => {
  throw new ErroAutenticacao('Falha na autenticação');
});

// Middleware para tratamento de erros
app.use((err, req, res, next) => {
  if (err instanceof ErroAutenticacao) {
    res.status(err.statusCode).send({ error: err.message });
  } else {
    res.status(500).send({ error: 'Erro interno do servidor' });
  }
});

app.listen(3000, () => console.log('Servidor rodando na porta 3000'));
```

---

## 📚 Recursos Adicionais

- 📝 [Documentação Oficial do JavaScript sobre Erros](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Error)
- 🚀 [Express.js - Tratamento de erros](https://expressjs.com/en/guide/error-handling.html)

---

## 🎯 Conclusão

Criar erros personalizados no Node.js permite que você forneça mensagens de erro mais significativas e específicas para seu aplicativo. Isso ajuda a melhorar a legibilidade do código e torna o tratamento de exceções mais claro e eficaz. Ao estender a classe `Error`, você pode adicionar comportamentos personalizados, como códigos de status, e tornar a depuração e o manuseio de falhas mais fáceis.

🚀 **Agora você está pronto para criar erros personalizados poderosos em seu projeto!** 🎉
