# **Criptografia em Node.js com Bcrypt**

📅 **Data:** 31 de julho de 2022  
✍️ **Autor:** Ronaldo B.  

---

## 📚 **Conhecendo a biblioteca Bcrypt**

A segurança dos dados é um dos principais pilares no desenvolvimento de sistemas modernos. Informações como **credenciais de acesso** e **dados sensíveis** precisam ser protegidas contra ataques como força bruta e tabelas rainbow. 

🚀 **Bcrypt** é uma biblioteca poderosa desenvolvida por **Niels Provos** e **David Mazières**, projetada para oferecer uma das melhores criptografias atuais. Seu grande diferencial é o uso de **salt**, que adiciona aleatoriedade ao hash original, dificultando ataques.

🔒 **Por que usar Bcrypt?**  
- Protege contra ataques de força bruta.  
- Adiciona segurança extra com salt.  
- Recomendado para armazenamento de dados sensíveis como **senhas**, **CPF**, **RG** e **IDs internos**.  
- Amplamente utilizado em linguagens populares e disponível no **Node.js**.

---

## 💻 **Instalação da biblioteca**

Para usar o Bcrypt em **Node.js**, basta instalá-lo pelo **NPM**:

```bash
npm i bcrypt
```

✔️ **Requisitos:** Para Node.js versão `12.13`, use a biblioteca na versão `3.0.6` ou superior.

---

## 🛠️ **Como usar Bcrypt**

### 🔢 Gerando hash com salt
O código abaixo demonstra como encriptar uma senha utilizando diferentes níveis de salt:

```javascript
const bcrypt = require('bcrypt');
const pass = '!]m:#$xDY@p/QDeW';

// Examinando o hash de 2^10 até 2^15
for (let saltRounds = 10; saltRounds <= 15; saltRounds++) { 
  bcrypt.hash(pass, saltRounds)
    .then((passHashed) => {
      console.time(`Time: ${saltRounds}`);
      console.log(passHashed);
      console.timeEnd(`Time: ${saltRounds}`);
    });
}
```

⚡ **Dica:**  
- Use **salt** de forma estratégica. Em testes, salt **12** é eficiente, mantendo o tempo de processamento em até **240ms**.  
- Ajuste o valor com base no desempenho do seu servidor.

### 🔄 Comparando dados criptografados

Utilize o método `bcrypt.compare()` para verificar se os dados fornecidos correspondem aos armazenados no banco:

```javascript
let userPass = '!]m:#$xDY@p/QDeW';

async function check(username, pass) {
  let passHashedDB = '$2b$12$dbstSfo1FN9jnZOSQ96N7eMMMe9FFI2QmYWo6E44WhutEUg9kZOcW';

  const match = await bcrypt.compare(pass, passHashedDB);
  
  if (match) {
    console.log('✅ Access Granted!');
  } else {
    console.log('❌ Access Denied!');
  }
}

// Chamando a função check
check('JediMaster', userPass);
```

---

## 📝 **Recomendações**
- ⚙️ Utilize **métodos assíncronos** para melhor desempenho no Node.js.  
- 🎛️ Teste diferentes valores de salt para encontrar o equilíbrio ideal entre **desempenho** e **segurança**.  
- 🛡️ Nunca armazene senhas ou dados sensíveis em texto limpo.  
- 📊 Monitore o consumo de CPU ao usar salt altos em sistemas com grande tráfego.

---

👨‍💻 **Conclusão:**  
O Bcrypt é uma ferramenta essencial para a segurança de aplicações. Com ele, você pode proteger dados sensíveis e garantir que sua aplicação esteja preparada para resistir a ataques comuns.

🔗 **Saiba mais:**  
- [Documentação oficial do BcryptJS](https://www.npmjs.com/package/bcrypt)  
- [Artigo completo sobre segurança de senhas](#)

