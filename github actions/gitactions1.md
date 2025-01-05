# O **GitHub Actions**

 é uma poderosa ferramenta de automação integrada ao GitHub, que permite criar, gerenciar e executar fluxos de trabalho automatizados diretamente em repositórios. Ele é amplamente utilizado para **CI/CD (Integração Contínua e Entrega Contínua)**, mas suas capacidades vão além, abrangendo tarefas como testes, deploy, linting, publicação de pacotes e até a automação de questões e pull requests.

Aqui está um guia detalhado sobre o GitHub Actions:

---

### **1. Conceitos Básicos**
- **Workflow:** Uma automação configurada no repositório, descrita em arquivos YAML localizados na pasta `.github/workflows/`.
- **Event:** O gatilho que inicia o workflow. Pode ser um push, pull request, agendamentos (cron), ações manuais ou eventos personalizados.
- **Job:** Uma sequência de etapas que será executada. Cada job pode ser independente ou depender de outro.
- **Step:** Uma unidade de execução dentro de um job. Pode executar comandos ou usar ações predefinidas.
- **Runner:** Um ambiente onde os jobs são executados. Pode ser hospedado pelo GitHub ou configurado como self-hosted.

---

### **2. Estrutura de um Workflow**
Um workflow básico tem a seguinte estrutura:

```yaml
name: CI Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Check out code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

#### Detalhes:
- **`name:`** Define o nome do workflow.
- **`on:`** Especifica os eventos que acionam o workflow (ex.: push, pull_request, schedule).
- **`jobs:`** Define os jobs que serão executados.
- **`runs-on:`** Determina o runner (ex.: `ubuntu-latest`, `windows-latest`, `macos-latest`).
- **`steps:`** Contém as ações ou comandos que o job executará.

---

### **3. Principais Recursos**
1. **Ações Reutilizáveis (Reusable Actions):**
   - Você pode criar e compartilhar ações específicas, reutilizáveis em múltiplos workflows.
   - Ações populares:
     - `actions/checkout`: Faz o checkout do código.
     - `actions/setup-node`: Configura o Node.js.
     - `actions/upload-artifact`: Salva artefatos gerados durante o build.

2. **Secrets:**
   - Variáveis sensíveis (como tokens de acesso ou credenciais) podem ser armazenadas no repositório e acessadas via `secrets`.
   ```yaml
   - name: Use secret token
     run: echo ${{ secrets.MY_SECRET }}
   ```

3. **Matrizes (Matrix Builds):**
   - Permitem testar o código em diferentes ambientes simultaneamente.
   ```yaml
   jobs:
     build:
       runs-on: ubuntu-latest
       strategy:
         matrix:
           node-version: [14, 16, 18]
       steps:
         - name: Set up Node.js
           uses: actions/setup-node@v3
           with:
             node-version: ${{ matrix.node-version }}
   ```

4. **Cache:**
   - Melhor performance ao reutilizar dependências.
   ```yaml
   - name: Cache dependencies
     uses: actions/cache@v3
     with:
       path: node_modules
       key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
       restore-keys: |
         ${{ runner.os }}-node-
   ```

5. **Executores Self-hosted:**
   - Configuração de runners próprios para maior controle e personalização.

---

### **4. Melhores Práticas**
1. **Mantenha o código limpo:**
   - Use arquivos YAML bem organizados.
2. **Minimize dependências externas:**
   - Sempre que possível, use runners ou ações que você controla.
3. **Otimize builds com cache:**
   - Utilize cache para reduzir o tempo de execução.
4. **Automatize testes e deploy:**
   - Configure pipelines de CI/CD para verificar commits antes de integrar à branch principal.
5. **Monitore e analise:**
   - Use logs detalhados para identificar problemas rapidamente.

---

### **5. Exemplos Avançados**
1. **Deploy Automático:**
   - Publicação de um site no GitHub Pages:
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches:
         - main

   jobs:
     deploy:
       runs-on: ubuntu-latest

       steps:
         - name: Check out code
           uses: actions/checkout@v3

         - name: Build site
           run: npm run build

         - name: Deploy to GitHub Pages
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./build
   ```

2. **Teste em múltiplos SOs:**
   ```yaml
   jobs:
     test:
       runs-on: ${{ matrix.os }}
       strategy:
         matrix:
           os: [ubuntu-latest, windows-latest, macos-latest]
       steps:
         - name: Check out code
           uses: actions/checkout@v3

         - name: Run tests
           run: npm test
   ```

---

### **6. Casos de Uso Comuns**
- **CI/CD:** Compilar, testar e fazer deploy automaticamente.
- **Automação de Pull Requests:** Adicionar labels, revisores ou rodar validações automáticas.
- **Publicação de Pacotes:** Automatizar a publicação de pacotes npm, PyPI, entre outros.
- **Infraestrutura como Código (IaC):** Implantar ambientes usando ferramentas como Terraform ou Ansible.

---

### **7. Limitações**
- Limite de execução para repositórios gratuitos: 2000 minutos/mês.
- Tarefas complexas podem exigir runners self-hosted.
- Pode se tornar confuso em projetos muito grandes sem uma organização adequada.

