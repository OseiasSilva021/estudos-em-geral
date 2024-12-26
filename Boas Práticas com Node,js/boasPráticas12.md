
# 🔐 **Evite Ataques de Força Bruta Contra Autorização**

## 💡 **TL;DR:**  
Para proteger sua aplicação contra **ataques de força bruta**, limite as tentativas de autenticação usando duas métricas principais:  
1. O número de tentativas consecutivas com falha para o **mesmo usuário** (ID/nome) e **endereço IP** exclusivos.
2. O número de tentativas falhas de **um único endereço IP** ao longo de um **período de tempo** (exemplo: bloquear o IP após 100 tentativas malsucedidas em um dia). ⚠️

---

## 🎯 **Por que Evitar Ataques de Força Bruta?**

### 🔥 **Riscos de Não Limitar Tentativas de Autorização:**
1. **Acesso Não Autorizado**: Ataques de força bruta envolvem a tentativa automatizada de adivinhar senhas. Se você não implementar uma limitação, um invasor pode fazer **tentativas ilimitadas** até conseguir acessar a conta de um usuário com privilégio.
2. **Desempenho Degradado**: Sem a limitação de tentativas, sua aplicação pode ser sobrecarregada com muitas solicitações, afetando o desempenho para usuários legítimos.
3. **Comprometimento de Contas Sensíveis**: Em sistemas críticos, como **bancos**, **e-commerce**, ou **sistemas de administração**, a proteção contra ataques de força bruta é fundamental para garantir a **segurança dos dados**.

---

## 🛠️ **Como Limitar Tentativas de Autorização?**

### 1️⃣ **Instale o Pacote `express-rate-limit`**

Uma forma simples de implementar a limitação de tentativas de login é utilizando a biblioteca **`express-rate-limit`**, que permite limitar o número de solicitações em um determinado período de tempo.

**Instalação**:

```bash
npm install express-rate-limit
```

### 2️⃣ **Configure a Limitação de Tentativas de Login**

Aqui está um exemplo básico de como usar o **`express-rate-limit`** para proteger o endpoint de login contra **ataques de força bruta**:

```javascript
const express = require('express');
const rateLimit = require('express-rate-limit');
const app = express();

// Limitar tentativas de login
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutos
  max: 5, // Limite de 5 tentativas de login
  message: 'Muitas tentativas de login. Tente novamente em 15 minutos.',
  keyGenerator: (req) => req.body.username || req.ip, // Limitar por usuário ou IP
});

// Aplica o limite de tentativas ao endpoint de login
app.post('/login', loginLimiter, (req, res) => {
  // Lógica de autenticação
  res.send('Autenticação bem-sucedida!');
});

// Inicia o servidor
app.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
```

### 3️⃣ **Limite Tentativas de Login por Endereço IP**

Para uma proteção ainda mais robusta, você pode combinar a limitação do número de tentativas **por usuário** e **por IP**. Isso impede que um invasor abuse de múltiplos usuários, realizando tentativas em grande quantidade a partir de um único IP.

```javascript
const limiterByIP = rateLimit({
  windowMs: 24 * 60 * 60 * 1000, // 1 dia
  max: 100, // Limite de 100 tentativas por IP
  message: 'Muitas tentativas de login a partir deste IP. Tente novamente mais tarde.',
  keyGenerator: (req) => req.ip, // Limitar por IP
});

// Aplica o limite de tentativas ao endpoint de login
app.post('/login', limiterByIP, (req, res) => {
  // Lógica de autenticação
  res.send('Autenticação bem-sucedida!');
});
```

### 4️⃣ **Uso de Captcha após Tentativas Múltiplas**

Outra medida importante é **adicionar CAPTCHA** após várias tentativas falhas, forçando o invasor a resolver um desafio para continuar tentando.

Aqui está um exemplo de como integrar o **reCAPTCHA** do Google após um número específico de tentativas falhas:

```javascript
// Após x tentativas falhas, mostre um CAPTCHA
let failedAttempts = 0;
app.post('/login', (req, res) => {
  if (failedAttempts >= 3) {
    // Exibir reCAPTCHA
    res.send('Por favor, resolva o CAPTCHA.');
  } else {
    // Lógica de autenticação
    res.send('Autenticação bem-sucedida!');
  }
});
```

### 5️⃣ **Use Bancos de Dados para Armazenar Tentativas de Login**

Para um controle mais detalhado das tentativas, você pode armazenar as tentativas de login e bloquear temporariamente a conta ou o IP em seu **banco de dados**. Isso ajuda a evitar que as tentativas sejam resetadas ao reiniciar o servidor.

Exemplo (pseudo-código):

```javascript
// Verifica as tentativas no banco de dados
db.getFailedLoginAttempts(userID, (attempts) => {
  if (attempts >= 5) {
    // Bloqueia o IP ou usuário
    res.send('Conta temporariamente bloqueada devido a tentativas de login excessivas.');
  } else {
    // Processa a autenticação
    res.send('Autenticação bem-sucedida!');
  }
});
```

---

## 🚨 **Consequências de Não Implementar Limitação de Tentativas**

Se você **não limitar as tentativas de login**, sua aplicação estará vulnerável a ataques automatizados de força bruta. Isso pode levar a:

1. **Roubo de credenciais**: Um invasor pode conseguir adivinhar a senha de um usuário legítimo e obter acesso a informações sensíveis.
2. **Comprometimento de contas com privilégios**: Se um atacante obter acesso a uma conta com privilégios elevados, ele pode comprometer toda a aplicação ou sistema.
3. **Negação de serviço (DoS)**: Tentativas excessivas de login podem sobrecarregar o servidor, degradando a performance ou tornando a aplicação indisponível para usuários legítimos.

---

## 🎯 **Conclusão**

1. **Limite as tentativas de login** para proteger sua aplicação contra ataques de força bruta.
2. Use bibliotecas como **`express-rate-limit`** para implementar facilmente a limitação de tentativas por usuário ou IP.
3. Combine a limitação com outras práticas de segurança, como **CAPTCHA** e **bloqueio temporário de IPs**.
4. Armazene tentativas de login em um **banco de dados** para maior controle e segurança.

---

## 🔧 **Dicas Finais**:

- **Monitore e registre** tentativas de login para detectar padrões de ataque e agir rapidamente.
- **Use autenticação multifatorial (MFA)** para adicionar uma camada extra de segurança, mesmo que a senha seja comprometida.
- **Implemente uma política de bloqueio** de contas após várias tentativas falhas para proteger suas contas mais sensíveis.

# 🔒 **Proteja sua aplicação contra ataques de força bruta!** 🚀
