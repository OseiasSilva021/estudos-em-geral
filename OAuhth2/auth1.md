
# O OAuth 2.0
 é um padrão aberto para autorização, amplamente utilizado para permitir que aplicativos acessem recursos protegidos em nome de um usuário, sem expor suas credenciais (como nome de usuário e senha). Ele é muito usado para integrações com serviços como Google, Facebook, GitHub, etc. Em Node.js, podemos implementar OAuth2 com bibliotecas como **passport.js**, **oauth2orize**, ou até diretamente com **axios** para realizar as solicitações.

Abaixo, segue uma explicação detalhada com exemplos práticos para implementar OAuth2 com Node.js:

---

## **Componentes do OAuth 2.0**
1. **Resource Owner (Usuário):** Quem possui os dados protegidos.
2. **Client (Aplicação):** O aplicativo que solicita acesso aos dados.
3. **Resource Server:** O servidor que hospeda os recursos protegidos.
4. **Authorization Server:** O servidor que autentica o usuário e emite tokens de acesso.

---

## **Fluxo Básico do OAuth 2.0**
1. O cliente redireciona o usuário para o servidor de autorização.
2. O usuário faz login e autoriza o acesso.
3. O servidor de autorização retorna um **authorization code**.
4. O cliente troca esse código por um **access token**.
5. O cliente usa o **access token** para acessar os recursos protegidos.

---

## **Exemplo com Node.js usando Passport.js**

### 1. **Instalando as dependências**
```bash
npm install express passport passport-google-oauth20 express-session
```

### 2. **Configurando o servidor**
```javascript
const express = require('express');
const passport = require('passport');
const session = require('express-session');
const { Strategy: GoogleStrategy } = require('passport-google-oauth20');

const app = express();

// Configuração do Passport com o Google OAuth2
passport.use(new GoogleStrategy({
    clientID: 'SEU_CLIENT_ID',
    clientSecret: 'SEU_CLIENT_SECRET',
    callbackURL: '/auth/google/callback',
}, (accessToken, refreshToken, profile, done) => {
    return done(null, profile);
}));

// Serializar e desserializar usuário
passport.serializeUser((user, done) => done(null, user));
passport.deserializeUser((user, done) => done(null, user));

// Middleware
app.use(session({ secret: 'segredo', resave: false, saveUninitialized: true }));
app.use(passport.initialize());
app.use(passport.session());

// Rotas
app.get('/', (req, res) => res.send('<a href="/auth/google">Login com Google</a>'));

app.get('/auth/google', passport.authenticate('google', {
    scope: ['profile', 'email'],
}));

app.get('/auth/google/callback', 
    passport.authenticate('google', { failureRedirect: '/' }),
    (req, res) => {
        res.redirect('/profile');
    }
);

app.get('/profile', (req, res) => {
    if (!req.isAuthenticated()) {
        return res.redirect('/');
    }
    res.send(`Bem-vindo, ${req.user.displayName}`);
});

// Iniciar servidor
app.listen(3000, () => console.log('Servidor rodando em http://localhost:3000'));
```

---

### 3. **Passo a passo para configuração**
- Crie um projeto no **Google Cloud Console**.
- Ative a API OAuth2 e configure um **Client ID**.
- Adicione `http://localhost:3000/auth/google/callback` como URI de redirecionamento autorizado.

---

## **Implementação Manual com Axios**

Caso prefira implementar diretamente, sem bibliotecas como Passport.js:

### 1. **Trocar o código de autorização por um token**
```javascript
const axios = require('axios');

async function getAccessToken(code) {
    const response = await axios.post('https://oauth2.googleapis.com/token', {
        client_id: 'SEU_CLIENT_ID',
        client_secret: 'SEU_CLIENT_SECRET',
        redirect_uri: 'http://localhost:3000/auth/callback',
        grant_type: 'authorization_code',
        code,
    });
    return response.data.access_token;
}
```

### 2. **Acessar recursos com o token**
```javascript
async function getUserInfo(accessToken) {
    const response = await axios.get('https://www.googleapis.com/oauth2/v2/userinfo', {
        headers: { Authorization: `Bearer ${accessToken}` },
    });
    return response.data;
}
```

### 3. **Integrando ao fluxo**
```javascript
app.get('/auth/callback', async (req, res) => {
    const code = req.query.code;
    try {
        const accessToken = await getAccessToken(code);
        const userInfo = await getUserInfo(accessToken);
        res.send(`Bem-vindo, ${userInfo.name}`);
    } catch (err) {
        console.error(err);
        res.send('Erro na autenticação');
    }
});
```

---

## **Dicas e Recomendações**
1. **Segurança:**
   - Sempre use HTTPS em produção.
   - Proteja suas credenciais (Client ID e Secret).
   - Armazene tokens de forma segura (por exemplo, com JWT ou na sessão do usuário).

2. **Scopes:** 
   - Defina apenas os escopos necessários para sua aplicação.

3. **Refresh Token:** 
   - Se o access token expirar, implemente a lógica para solicitar um novo usando o **refresh token**.

4. **Bibliotecas Úteis:**
   - Além de Passport.js, explore **simple-oauth2** e **openid-client** para fluxos mais avançados.

