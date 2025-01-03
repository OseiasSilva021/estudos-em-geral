# Docker  

É uma plataforma de contêineres que permite empacotar, distribuir e executar aplicações de maneira isolada do sistema operacional. Ele facilita o desenvolvimento, a distribuição e a execução de software, garantindo que as aplicações sejam consistentes em diferentes ambientes, como desenvolvimento, teste e produção.

---

## **Conceitos Fundamentais do Docker**

### 1. **Imagem (Image)**
Uma imagem é um pacote leve e imutável que contém tudo o que sua aplicação precisa para ser executada: código, runtime, bibliotecas e dependências. É como um template para criar contêineres.

### 2. **Contêiner (Container)**
Um contêiner é uma instância de uma imagem. Ele é executado de forma isolada, garantindo que a aplicação dentro dele funcione de maneira previsível.

### 3. **Dockerfile**
Um Dockerfile é um script de texto que contém uma lista de instruções para construir uma imagem Docker.

### 4. **Docker Hub**
Um repositório público onde você pode armazenar e compartilhar imagens Docker.

### 5. **Docker Compose**
Uma ferramenta para definir e gerenciar aplicações multi-contêiner com um arquivo YAML.

---

## **Comandos Básicos do Docker**

1. **Verificar a versão do Docker**:
   ```bash
   docker --version
   ```

2. **Listar contêineres em execução**:
   ```bash
   docker ps
   ```

3. **Listar todos os contêineres (incluindo parados)**:
   ```bash
   docker ps -a
   ```

4. **Executar um contêiner com uma imagem existente**:
   ```bash
   docker run -d -p 80:80 nginx
   ```

5. **Parar um contêiner**:
   ```bash
   docker stop <container_id>
   ```

6. **Remover um contêiner**:
   ```bash
   docker rm <container_id>
   ```

7. **Construir uma imagem a partir de um Dockerfile**:
   ```bash
   docker build -t minha-imagem .
   ```

8. **Remover uma imagem**:
   ```bash
   docker rmi <image_id>
   ```

---

## **Exemplo Prático**

### Criando um Contêiner com Nginx

1. Execute o seguinte comando para baixar a imagem do Nginx e rodá-la:
   ```bash
   docker run -d -p 8080:80 nginx
   ```

2. Acesse o navegador em `http://localhost:8080` para ver a página padrão do Nginx.

---

### **Usando um Dockerfile**

#### Criar um aplicativo Node.js simples em Docker:

1. Crie um arquivo chamado `app.js`:
   ```javascript
   const http = require('http');

   const hostname = '0.0.0.0';
   const port = 3000;

   const server = http.createServer((req, res) => {
       res.statusCode = 200;
       res.setHeader('Content-Type', 'text/plain');
       res.end('Hello, Docker!');
   });

   server.listen(port, hostname, () => {
       console.log(`Server running at http://${hostname}:${port}/`);
   });
   ```

2. Crie um arquivo `Dockerfile`:
   ```Dockerfile
   FROM node:16

   WORKDIR /app

   COPY package*.json ./

   RUN npm install

   COPY . .

   EXPOSE 3000

   CMD ["node", "app.js"]
   ```

3. Construa a imagem:
   ```bash
   docker build -t meu-node-app .
   ```

4. Rode o contêiner:
   ```bash
   docker run -d -p 3000:3000 meu-node-app
   ```

5. Acesse `http://localhost:3000` no navegador para ver a mensagem "Hello, Docker!".

---

### **Usando Docker Compose**

#### Arquivo `docker-compose.yml` para rodar Node.js e MongoDB:

```yaml
version: '3.8'
services:
  app:
    build:
      context: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    depends_on:
      - db
  db:
    image: mongo
    ports:
      - "27017:27017"
```

1. Inicie os serviços:
   ```bash
   docker-compose up -d
   ```

2. Ambos os serviços (Node.js e MongoDB) estarão rodando.

---

## **Melhores Práticas**

1. **Mantenha o Dockerfile simples**: Evite camadas desnecessárias para otimizar o tempo de build e o tamanho da imagem.
   
2. **Use imagens leves**: Prefira imagens base como `alpine` para reduzir o tamanho.

3. **Gerencie volumes**: Use volumes para persistir dados e evitar perda de informações ao reiniciar contêineres.

4. **Rotule seus contêineres**: Utilize `--label` para documentar seus contêineres.

5. **Atualize frequentemente**: Garanta que as imagens usadas sejam mantidas atualizadas.

6. **Limpeza regular**:
   ```bash
   docker system prune -a
   ```

---

Docker é essencial para desenvolvedores full stack como você, Oséias. Ao dominar essa tecnologia, você pode criar ambientes consistentes e escaláveis. Precisa de mais detalhes sobre algum aspecto?
