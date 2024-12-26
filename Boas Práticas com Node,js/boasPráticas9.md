
# 🚨 **Limite Requests Simultâneos Usando um Middleware**

## 💡 **TL;DR:**  
**Ataques de DoS (Denial of Service)** são muito comuns e podem ser facilmente conduzidos. Para proteger seu aplicativo contra esses ataques, implemente uma **limitação de taxa** (rate limiting). Você pode usar serviços externos como **balanceadores de carga de nuvem** ou **firewalls de nuvem**, ou soluções mais simples como **nginx**, **rate-limiter-flexible** ou até mesmo um **middleware limitador de taxa** como o **express-rate-limit** para aplicações Node.js. ⚠️

---

## 🎯 **Por que Limitar Requests Simultâneos?**

### 🔥 **Riscos de Não Limitar Requests:**
- **Ataques de DoS (Denial of Service)** podem sobrecarregar sua aplicação, tornando o serviço **indisponível** para usuários reais. 📉
- Uma aplicação sem limitação de taxa pode sofrer **degradação de serviço**, onde o tempo de resposta aumenta e a experiência do usuário piora. 😱
- **Excesso de tráfego** pode esgotar recursos como CPU, memória e banda de rede, causando **queda do servidor**. 🚨

### 🚀 **Vantagens de Limitar Requests:**
1. **Proteção contra DoS e ataques de força bruta** 👊  
2. **Controle sobre a quantidade de tráfego** para evitar sobrecarga dos servidores ⚡  
3. **Melhor performance e resiliência**, garantindo que os recursos do servidor sejam usados de maneira eficiente 💪

---

## 🛠️ **Como Implementar Limitação de Taxa?**

### 1️⃣ **Usando o Middleware `express-rate-limit`**

Se você está utilizando o **Express.js** no seu servidor Node, o pacote `express-rate-limit` é uma maneira simples de começar a limitar a quantidade de requisições que um usuário pode fazer em um determinado período de tempo.

**Exemplo de implementação com `express-rate-limit`:**

1. Primeiro, instale o pacote:
   ```bash
   npm install express-rate-limit
   ```

2. Em seguida, adicione o middleware ao seu servidor:

   ```javascript
   const express = require('express');
   const rateLimit = require('express-rate-limit');
   
   const app = express();
   
   // Defina o limite de requisições: 100 requisições por 15 minutos
   const limiter = rateLimit({
     windowMs: 15 * 60 * 1000,  // 15 minutos
     max: 100,                  // Limite de 100 requisições
     message: 'Too many requests, please try again later.'
   });
   
   // Aplique o middleware globalmente
   app.use(limiter);
   
   app.get('/', (req, res) => {
     res.send('Olá, você está acessando o servidor!');
   });
   
   app.listen(3000, () => {
     console.log('Servidor rodando na porta 3000');
   });
   ```

**O que isso faz?**  
Este código limita cada **endereço IP** a 100 requisições em um período de 15 minutos. Se o usuário exceder esse limite, ele receberá uma mensagem de erro dizendo "Too many requests, please try again later." ⚠️

### 2️⃣ **Usando o `rate-limiter-flexible`**

Para sistemas mais robustos ou onde você precisa de um controle mais avançado, o pacote **`rate-limiter-flexible`** é uma excelente alternativa. Ele permite integrar limitação de taxa com armazenamento externo como **Redis** ou **MongoDB**.

**Exemplo básico usando `rate-limiter-flexible` e Redis:**

1. Instale os pacotes necessários:
   ```bash
   npm install rate-limiter-flexible redis
   ```

2. Implemente a limitação de taxa com Redis:

   ```javascript
   const { RateLimiterRedis } = require('rate-limiter-flexible');
   const express = require('express');
   const redis = require('redis');
   
   const app = express();
   
   // Conecte-se ao Redis
   const redisClient = redis.createClient({
     host: 'localhost',  // Ajuste conforme seu setup
     port: 6379
   });
   
   // Configure o rate limiter
   const rateLimiter = new RateLimiterRedis({
     storeClient: redisClient,
     points: 10,   // Quantidade de requisições permitidas
     duration: 1,  // Duração em segundos
   });
   
   // Middleware para verificar a limitação
   app.use((req, res, next) => {
     rateLimiter.consume(req.ip)  // Verifica o IP do cliente
       .then(() => next())         // Se permitido, continua a requisição
       .catch(() => {
         res.status(429).send('Too many requests, please try again later.');
       });
   });
   
   app.get('/', (req, res) => {
     res.send('Bem-vindo! Você não ultrapassou o limite de requisições!');
   });
   
   app.listen(3000, () => {
     console.log('Servidor rodando na porta 3000');
   });
   ```

**O que acontece aqui?**  
A cada requisição, o middleware verifica se o cliente ultrapassou o limite de 10 requisições por segundo. Se ultrapassar, retorna o código de status **429 Too Many Requests**. Caso contrário, o servidor continua a atender normalmente. 🎯

### 3️⃣ **Usando `nginx` como Limitação de Taxa**

Se você preferir usar **nginx** como middleware para limitar o tráfego, você pode adicionar as seguintes configurações ao arquivo de configuração do nginx (`nginx.conf`):

```nginx
http {
  # Limitação de taxa por IP
  limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

  server {
    listen 80;

    location / {
      limit_req zone=mylimit burst=20 nodelay;
      proxy_pass http://localhost:3000;  # Redireciona para seu servidor Node.js
    }
  }
}
```

**O que acontece aqui?**  
- **10r/s**: Limita a 10 requisições por segundo.
- **burst=20**: Permite até 20 requisições extras em picos de tráfego.
- **nodelay**: Não retarda o tráfego extra, apenas bloqueia quando o limite é atingido.

---

## 🚨 **O que acontece se você não limitar requests?**

Se você **não implementar limitação de taxa**, sua aplicação fica vulnerável a **ataques de DoS** ou **flooding**, onde um grande número de requisições simultâneas pode **derrubar** o servidor. Sem a limitação, os usuários reais podem enfrentar **indisponibilidade** ou **serviço degradado**. ⚠️

**Exemplo**: Um atacante pode enviar milhares de requisições por minuto para o seu servidor, sobrecarregando o sistema e **degradando a experiência** dos seus usuários legítimos. 😨

---

## 🎯 **Conclusão**
1. **Implemente limitação de taxa** para proteger sua aplicação contra ataques DoS e garantir que o serviço permaneça estável e eficiente.
2. **Middleware como `express-rate-limit`** ou **pacotes mais avançados** como `rate-limiter-flexible` oferecem boas opções para controle.
3. **Balanceadores de carga e nginx** também podem ser configurados para garantir a escalabilidade e proteção do seu sistema.

---

## 🔧 **Dicas Finais:**
- **Sempre faça testes de carga** para entender o comportamento do seu sistema sob diferentes volumes de requisições. 🧪
- **Monitore** suas métricas de tráfego para ajustar a limitação de taxa conforme a necessidade. 📊
- **Considere utilizar Redis ou outra solução de cache** para manter a performance ideal ao lidar com requisições. 🚀

# 💪 **Proteja sua aplicação contra ataques e garanta uma experiência estável para seus usuários!** 🌍
