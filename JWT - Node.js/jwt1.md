JSON Web Token (JWT) é uma tecnologia amplamente usada para autenticação e troca segura de informações entre partes no desenvolvimento de APIs. Vou explicar tudo sobre JWT no contexto do Node.js! 🚀

---

## **O que é JWT?** 🛡️

JWT é um padrão aberto (RFC 7519) que define um formato compacto e auto-contido para representar informações de forma segura entre duas partes como um objeto JSON. Ele é geralmente usado para:

1. **Autenticação**: Manter usuários logados de forma segura.
2. **Autorização**: Garantir que usuários tenham acesso somente a recursos permitidos.
3. **Troca de informações seguras**.

---

## **Estrutura do JWT** 📦

Um JWT é dividido em três partes separadas por pontos (`.`):

1. **Header**: Contém o tipo de token (`JWT`) e o algoritmo de assinatura usado, como `HS256` ou `RS256`.
   ```json
   {
     "alg": "HS256",
     "typ": "JWT"
   }
   ```

2. **Payload**: Contém as "claims", ou seja, os dados que queremos transmitir, como `id do usuário`, `papel` (role), etc.
   ```json
   {
     "userId": "123",
     "role": "admin",
     "iat": 1516239022
   }
   ```

3. **Signature**: Garante a integridade e autenticidade do token. É gerada usando:
   ```
   HMACSHA256(
     base64UrlEncode(header) + "." +
     base64UrlEncode(payload),
     secret
   )
   ```

Um JWT completo se parece com isso:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.eyJ1c2VySWQiOiIxMjMiLCJyb2xlIjoiYWRtaW4iLCJpYXQiOjE1MTYyMzkwMjJ9
.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

---

## **Como usar JWT no Node.js?** 🛠️

### Instale os pacotes necessários:
Use o pacote **jsonwebtoken**:
```bash
npm install jsonwebtoken
```

---

### Gerando um JWT 🔑
```javascript
const jwt = require('jsonwebtoken');

const payload = { userId: 123, role: 'admin' };
const secretKey = 'sua-chave-secreta'; // Escolha uma chave secreta forte! 🔒
const options = { expiresIn: '1h' }; // Token expira em 1 hora ⏰

const token = jwt.sign(payload, secretKey, options);
console.log('Token:', token);
```

---

### Verificando um JWT ✅
```javascript
try {
  const verified = jwt.verify(token, secretKey);
  console.log('Token válido!', verified);
} catch (err) {
  console.error('Token inválido ou expirado!', err.message);
}
```

---

### Extraindo informações do JWT 🕵️‍♂️
Use `jwt.decode()` para decodificar o token sem verificar a assinatura:
```javascript
const decoded = jwt.decode(token);
console.log('Payload decodificado:', decoded);
```

---

## **Boas práticas com JWT** ⚡

1. **Use HTTPS**: Proteja tokens contra interceptação. 🔒
2. **Expire Tokens**: Defina um tempo de expiração curto, como `15 minutos` ou `1 hora`. ⏳
3. **Renovação de Tokens**: Implemente **refresh tokens** para evitar logouts forçados. 🔄
4. **Armazene com segurança**: Guarde o JWT no `localStorage` ou `cookies` de forma segura.
   - Prefira **cookies com flags HttpOnly e Secure**. 🍪
5. **Revogação de Tokens**: Mantenha uma lista de tokens revogados, se necessário. 🚫
6. **Não inclua informações sensíveis no payload**: O payload é visível para qualquer um que decodificar o token. ⚠️

---

## **JWT no fluxo de autenticação** 🔐

1. **Login**:
   - O cliente envia as credenciais para o servidor.
   - O servidor valida as credenciais e retorna um JWT ao cliente.
2. **Autenticação em rotas**:
   - O cliente envia o token no cabeçalho de autorização:
     ```
     Authorization: Bearer <seu-token>
     ```
   - O servidor valida o token antes de conceder acesso.
3. **Renovação de token** (opcional):
   - Quando o token expira, um **refresh token** pode ser usado para gerar um novo.

---

Com isso, você tem o essencial (e um pouco mais) sobre JWT no Node.js.
