# 🚀 **Construindo e Versionando uma API RESTful com Node.js** 🖥️

## 📑 Índice

- [🚀 **Construindo e Versionando uma API RESTful com Node.js** 🖥️](#-construindo-e-versionando-uma-api-restful-com-nodejs-️)
  - [📑 Índice](#-índice)
  - [🛠️ Construção de uma API RESTful com Node.js](#️-construção-de-uma-api-restful-com-nodejs)
    - [Passos para Construir a API RESTful: 🚶‍♂️](#passos-para-construir-a-api-restful-️)
  - [📋 Estrutura de Resposta Adequada](#-estrutura-de-resposta-adequada)
    - [Códigos de Status HTTP: 🔢](#códigos-de-status-http-)
    - [Cabeçalhos: 🏷️](#cabeçalhos-️)
    - [Exemplo de Resposta Adequada: 💬](#exemplo-de-resposta-adequada-)
  - [🧪 Testando a API com Ferramentas como Postman ou Insomnia](#-testando-a-api-com-ferramentas-como-postman-ou-insomnia)
    - [Como Usar: 📲](#como-usar-)
  - [📜 Versionamento de API](#-versionamento-de-api)
    - [Por Que Versionar? 🤔](#por-que-versionar-)
    - [Como Versionar uma API? 🔢](#como-versionar-uma-api-)
    - [Manutenção da Compatibilidade Retroativa 🔧](#manutenção-da-compatibilidade-retroativa-)
    - [Exemplo de Versionamento na URL: 🌍](#exemplo-de-versionamento-na-url-)
  - [🔚 Conclusão](#-conclusão)

## 🛠️ Construção de uma API RESTful com Node.js

APIs RESTful são uma arquitetura de comunicação entre sistemas onde os dados são trocados via HTTP 🌐, utilizando os métodos HTTP para interagir com os recursos. Node.js, com o framework Express, é uma excelente escolha para construir APIs RESTful 💡.

### Passos para Construir a API RESTful: 🚶‍♂️

1. **Instalar Node.js e Express** 📥
   ```bash
   npm init -y
   npm install express
   ```

2. **Configuração Básica do Servidor** ⚙️
   Crie um arquivo `server.js` e adicione o seguinte código:
   ```javascript
   const express = require('express');
   const app = express();

   app.use(express.json()); // Para que o Express entenda o JSON enviado no corpo da requisição

   const port = 3000;

   app.listen(port, () => {
     console.log(`Server running on port ${port}`);
   });
   ```

3. **Definir Endpoints (Rotas)** 🛣️
   Defina os métodos HTTP para os endpoints da API:

   ```javascript
   // Recupera todos os itens
   app.get('/items', (req, res) => {
     res.status(200).json({ message: 'List of items' });
   });

   // Cria um novo item
   app.post('/items', (req, res) => {
     const newItem = req.body;
     res.status(201).json(newItem);
   });

   // Atualiza um item
   app.put('/items/:id', (req, res) => {
     const id = req.params.id;
     const updatedItem = req.body;
     res.status(200).json({ id, updatedItem });
   });

   // Deleta um item
   app.delete('/items/:id', (req, res) => {
     const id = req.params.id;
     res.status(200).json({ message: `Item with ID ${id} deleted` });
   });
   ```

## 📋 Estrutura de Resposta Adequada

Ao criar uma API RESTful, é importante seguir uma estrutura de resposta clara 📝. Isso inclui códigos de status HTTP e cabeçalhos apropriados.

### Códigos de Status HTTP: 🔢
- **200 OK**: Solicitação bem-sucedida ✅.
- **201 Created**: Recurso criado com sucesso ✨.
- **400 Bad Request**: Erro na solicitação ❌.
- **401 Unauthorized**: Acesso não autorizado 🚫.
- **404 Not Found**: Recurso não encontrado 🔍.
- **500 Internal Server Error**: Erro no servidor 🛑.

### Cabeçalhos: 🏷️
- **Content-Type**: Tipo de conteúdo da resposta (`application/json`).
- **Location**: Usado para indicar a URL do recurso criado (em respostas de criação).

### Exemplo de Resposta Adequada: 💬
```javascript
res.status(200).json({
  message: 'Item retrieved successfully',
  data: item
});
```

## 🧪 Testando a API com Ferramentas como Postman ou Insomnia

Ferramentas como **Postman** e **Insomnia** são essenciais para testar APIs RESTful 🛠️. Elas permitem enviar requisições HTTP, verificar a resposta e identificar problemas.

### Como Usar: 📲
- **Postman**: Crie requisições HTTP, defina cabeçalhos e visualize as respostas. Ideal para testar rotas, verificar códigos de status e debugar a API 🔍.
- **Insomnia**: Semelhante ao Postman, permite enviar requisições e testar endpoints de forma eficaz ⚡.

Ambas as ferramentas ajudam a garantir que a API esteja funcionando corretamente durante o desenvolvimento 🏗️.

## 📜 Versionamento de API

O versionamento de API é crucial para garantir que alterações na API não quebrem a compatibilidade com consumidores existentes 🔄.

### Por Que Versionar? 🤔
- **Evolução da API**: Permite adicionar novas funcionalidades sem afetar os consumidores existentes 🔧.
- **Compatibilidade Retroativa**: Garante que versões anteriores da API continuem funcionando enquanto novas funcionalidades são introduzidas 🔄.

### Como Versionar uma API? 🔢
1. **Versão na URL**: A maneira mais comum de versionar APIs é incluir a versão diretamente na URL:
   ```
   /api/v1/items
   /api/v2/items
   ```

2. **Versão no Cabeçalho**: Outra abordagem é passar a versão através do cabeçalho `Accept`:
   ```
   GET /items
   Header: Accept: application/vnd.myapi.v1+json
   ```

### Manutenção da Compatibilidade Retroativa 🔧
- **Degradando Versões Antigas**: Mantenha versões antigas por um tempo, dando tempo para os consumidores migrarem 🕒.
- **Depreciação Suave**: Informe quando uma versão será descontinuada 🛑.
- **Semântica na Versão**: Use convenções de versionamento para indicar mudanças significativas (major), melhorias (minor) e correções (patch):
   - **v1.0.0**: Primeira versão 🌱.
   - **v1.1.0**: Nova funcionalidade, mas compatível com v1 🔥.
   - **v2.0.0**: Mudanças que podem quebrar a compatibilidade 🚨.

### Exemplo de Versionamento na URL: 🌍
```javascript
app.get('/api/v1/items', (req, res) => {
  res.status(200).json({ message: 'Version 1 of items' });
});

app.get('/api/v2/items', (req, res) => {
  res.status(200).json({ message: 'Version 2 of items with new features' });
});
```

## 🔚 Conclusão

Construir e versionar APIs RESTful com Node.js envolve criar endpoints com os métodos HTTP adequados 🛣️, fornecer respostas claras com códigos de status e cabeçalhos 📊, e garantir que a API evolua sem quebrar a compatibilidade com versões anteriores 🔄. Ferramentas como Postman e Insomnia são essenciais para testar a API durante o desenvolvimento 🔧.

