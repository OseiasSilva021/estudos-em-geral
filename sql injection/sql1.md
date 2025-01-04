

# SQL Injection 

É uma vulnerabilidade crítica que ocorre quando entradas fornecidas pelo usuário são injetadas em consultas SQL sem validação adequada, permitindo que um atacante manipule a consulta. Vamos abordar tudo sobre prevenção com foco em **Node.js**, dicas práticas e exemplos:

---

## **1. O que é SQL Injection?**
É a manipulação maliciosa de consultas SQL por entradas de usuários. Um atacante pode injetar comandos SQL para roubar dados, modificar informações ou até apagar tabelas.

**Exemplo vulnerável**:
```javascript
const express = require("express");
const mysql = require("mysql");
const app = express();

const connection = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "",
  database: "test"
});

app.get("/user", (req, res) => {
  const username = req.query.username;
  const query = `SELECT * FROM users WHERE username = '${username}'`;

  connection.query(query, (err, results) => {
    if (err) throw err;
    res.send(results);
  });
});
```

**Entrada maliciosa**:
```sql
' OR '1'='1
```
Resultado: Retorna todos os usuários, já que `'1'='1'` sempre será verdadeiro.

---

## **2. Boas práticas para prevenir SQL Injection**
### **2.1 Use Queries Preparadas (Prepared Statements)**
Essa é a solução mais eficaz, pois separa o SQL do dado fornecido pelo usuário.

**Exemplo seguro**:
```javascript
app.get("/user", (req, res) => {
  const username = req.query.username;
  const query = "SELECT * FROM users WHERE username = ?";
  
  connection.query(query, [username], (err, results) => {
    if (err) throw err;
    res.send(results);
  });
});
```

### **2.2 Utilize ORMs Seguros**
Frameworks ORM como **Sequelize**, **TypeORM** ou **Prisma** abstraem o uso direto de SQL e incluem proteções nativas contra injeções.

**Exemplo com Sequelize**:
```javascript
const { Sequelize, DataTypes } = require("sequelize");
const sequelize = new Sequelize("test", "root", "", { dialect: "mysql" });

const User = sequelize.define("User", {
  username: DataTypes.STRING,
  password: DataTypes.STRING
});

app.get("/user", async (req, res) => {
  const username = req.query.username;
  const user = await User.findOne({ where: { username } });
  res.send(user);
});
```

### **2.3 Validação e Sanitização de Entradas**
Utilize bibliotecas como **Joi**, **express-validator** ou **validator.js** para garantir que as entradas tenham os valores esperados.

**Exemplo com express-validator**:
```javascript
const { check, validationResult } = require("express-validator");

app.get("/user", 
  [check("username").isAlphanumeric().notEmpty()],
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }

    const username = req.query.username;
    const query = "SELECT * FROM users WHERE username = ?";
    
    connection.query(query, [username], (err, results) => {
      if (err) throw err;
      res.send(results);
    });
  }
);
```

### **2.4 Limite de Permissões no Banco de Dados**
- **Regra de ouro**: A aplicação deve usar um usuário de banco de dados com permissões mínimas. 
  - Evite que esse usuário tenha privilégios como `DROP`, `DELETE` ou `UPDATE`, exceto quando absolutamente necessário.

---

## **3. Configurações Adicionais**
### **3.1 Escape de Strings**
Use funções de escape fornecidas pela biblioteca do banco de dados, como `mysql.escape()`.

**Exemplo**:
```javascript
const username = mysql.escape(req.query.username);
const query = `SELECT * FROM users WHERE username = ${username}`;
connection.query(query, (err, results) => {
  if (err) throw err;
  res.send(results);
});
```

### **3.2 Parametrize Queries em Bibliotecas Não SQL**
Se você usa bancos como MongoDB, use operadores seguros (`$eq`, `$gt`, etc.) para evitar injeções de consulta.

---

## **4. Como Explorar e Prevenir (Exemplo Prático)**
### **Exploração de uma vulnerabilidade:**
- Com um formulário de login:
```sql
' OR '1'='1' --
```
Se a consulta for:
```sql
SELECT * FROM users WHERE username = '' OR '1'='1' --' AND password = ''
```
Isso retorna todos os usuários.

### **Como consertar:**
- Usando consultas parametrizadas:
```javascript
const username = req.body.username;
const password = req.body.password;

const query = "SELECT * FROM users WHERE username = ? AND password = ?";
connection.query(query, [username, password], (err, results) => {
  if (err) throw err;
  res.send(results);
});
```

---

## **5. Ferramentas para Testar e Auditar**
- **sqlmap**: Ferramenta automatizada para detectar SQL Injection.
- **OWASP ZAP**: Escaneia vulnerabilidades em aplicações web.
- **Burp Suite**: Proxy para análise e manipulação de requisições HTTP.

---

## **6. Checklist Final**
- [x] Sempre use **prepared statements**.
- [x] Valide e sanitize as entradas do usuário.
- [x] Aplique limites de permissões ao banco.
- [x] Escape os dados onde necessário.
- [x] Faça auditorias regulares de segurança.

Com essas práticas, você estará bem preparado para prevenir SQL Injection em suas aplicações Node.js.
