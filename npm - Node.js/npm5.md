
# 🚀 Executando Scripts com npm no Node.js 🌟  

Os scripts npm são uma funcionalidade poderosa do Node.js que facilita a execução de tarefas como iniciar um servidor, construir um projeto ou rodar testes. Eles são definidos no arquivo `package.json` do seu projeto e podem ser personalizados de acordo com suas necessidades.  

---

## 📜 O Que São Scripts npm?  

- São comandos configurados no arquivo `package.json`.  
- Permitem automatizar tarefas comuns em projetos Node.js.  
- Suportam encadeamento e organização de comandos.  

Os scripts npm ajudam a manter um fluxo de trabalho eficiente, eliminando a necessidade de digitar comandos longos repetidamente.  

---

## 🛠️ Como Configurar Scripts  

Os scripts são definidos na seção `"scripts"` do arquivo `package.json`.  

### 🎯 Estrutura Básica  

```json
{
  "scripts": {
    "start": "node server.js",
    "build": "webpack --mode production",
    "test": "jest"
  }
}
```

- **`start`**: Comando padrão para iniciar um servidor.  
- **`build`**: Comando para construir o projeto (ex.: usando Webpack).  
- **`test`**: Comando para rodar testes (ex.: usando Jest).  

---

## 🧑‍💻 Executando Scripts  

1. **Rodar um Script**:  

   ```bash
   npm run <nome-do-script>
   ```

   Exemplo:  

   ```bash
   npm run build
   ```

2. **Script Padrão (`start`)**:  

   Se o script for `start`, não é necessário usar `run`:  

   ```bash
   npm start
   ```

---

## ✨ Dividindo Scripts Grandes  

Você pode dividir scripts longos em partes menores para facilitar a manutenção:  

### Exemplo  

No `package.json`:  

```json
{
  "scripts": {
    "clean": "rimraf dist",
    "build:css": "postcss src/styles.css -o dist/styles.css",
    "build:js": "webpack --mode production",
    "build": "npm run clean && npm run build:css && npm run build:js"
  }
}
```

Agora, ao rodar `npm run build`, ele:  
1. Limpa a pasta `dist`.  
2. Processa os arquivos CSS.  
3. Compila o JavaScript.  

---

## 🌍 Scripts Globais vs Scripts Locais  

- **Globais**: Comandos do sistema, como `npm install -g`.  
- **Locais**: Específicos do projeto, definidos no `package.json`.  

Prefira scripts locais para evitar conflitos e garantir reprodutibilidade no ambiente de outros desenvolvedores.  

---

## 🛠️ Dicas e Truques  

1. **Executar Scripts npm com `npx`**:  
   Use `npx` para rodar pacotes instalados localmente sem definir scripts no `package.json`.  

   ```bash
   npx eslint src/
   ```

2. **Encadeamento de Comandos**:  
   Use `&&` para executar comandos sequenciais e `||` para comandos condicionais.  

   ```json
   "scripts": {
     "check": "eslint src/ && jest"
   }
   ```

3. **Usando Variáveis no Script**:  
   No Node.js, você pode passar variáveis diretamente nos scripts.  

   ```json
   "scripts": {
     "serve": "PORT=3000 node server.js"
   }
   ```

4. **Verificar Todos os Scripts**:  
   Liste os scripts disponíveis com:  

   ```bash
   npm run
   ```

---

## 🎯 Exemplos de Uso  

### 1️⃣ Testes Automatizados  

```json
{
  "scripts": {
    "test": "jest --watchAll"
  }
}
```

```bash
npm test
```

---

### 2️⃣ Build de Produção  

```json
{
  "scripts": {
    "build": "webpack --mode production"
  }
}
```

```bash
npm run build
```

---

### 3️⃣ Iniciando um Servidor  

```json
{
  "scripts": {
    "start": "node server.js"
  }
}
```

```bash
npm start
```

---

## 📚 Recursos Úteis  

- 🌐 [Documentação Oficial do npm](https://docs.npmjs.com/)  
- 📖 [Scripts npm em Detalhes](https://docs.npmjs.com/cli/v9/using-npm/scripts)  
- 🛠️ [Node.js e Automação de Tarefas](https://nodejs.org/)  

---

## 🎉 Conclusão  

Os scripts npm são ferramentas indispensáveis para manter seus projetos organizados e automatizar tarefas recorrentes. Dominar seu uso melhora a produtividade e reduz erros ao longo do desenvolvimento.  

🚀 **Feliz codificação com scripts npm!** 🌟  
