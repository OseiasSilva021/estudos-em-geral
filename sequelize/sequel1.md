# O Sequelize

 é uma biblioteca ORM (Object-Relational Mapping) para Node.js, que permite interagir com bancos de dados relacionais (como MySQL, PostgreSQL, SQLite e MariaDB) usando JavaScript. Ele abstrai as consultas SQL, tornando o gerenciamento de bancos de dados mais simples e orientado a objetos.

Abaixo está um guia completo sobre o Sequelize, incluindo conceitos, exemplos e boas práticas.

---

### **1. Instalação**
Para usar o Sequelize, você precisa instalá-lo junto com o driver do banco de dados que deseja usar. Por exemplo, para um projeto com MySQL:

```bash
npm install sequelize mysql2
```

---

### **2. Configuração Inicial**
Configure a conexão ao banco de dados:

```javascript
const { Sequelize } = require('sequelize');

const sequelize = new Sequelize('nome_do_banco', 'usuario', 'senha', {
  host: 'localhost',
  dialect: 'mysql', // Pode ser 'mysql', 'postgres', 'sqlite', 'mariadb', ou 'mssql'
});

// Testar a conexão
(async () => {
  try {
    await sequelize.authenticate();
    console.log('Conexão com o banco de dados foi estabelecida com sucesso!');
  } catch (error) {
    console.error('Erro ao conectar ao banco de dados:', error);
  }
})();
```

---

### **3. Definição de Modelos**
Um **modelo** no Sequelize é uma representação de uma tabela no banco de dados.

```javascript
const { DataTypes } = require('sequelize');

const User = sequelize.define('User', {
  name: {
    type: DataTypes.STRING,
    allowNull: false, // Campo obrigatório
  },
  email: {
    type: DataTypes.STRING,
    unique: true, // Garante que o email seja único
    allowNull: false,
  },
  password: {
    type: DataTypes.STRING,
    allowNull: false,
  },
}, {
  timestamps: true, // Adiciona `createdAt` e `updatedAt` automaticamente
});
```

---

### **4. Sincronizando o Banco de Dados**
Após definir os modelos, você pode sincronizar o banco de dados:

```javascript
(async () => {
  try {
    await sequelize.sync({ force: true }); // `force: true` recria as tabelas
    console.log('As tabelas foram criadas!');
  } catch (error) {
    console.error('Erro ao criar tabelas:', error);
  }
})();
```

---

### **5. Operações CRUD**
#### **a) Criar registros**
```javascript
(async () => {
  const newUser = await User.create({
    name: 'Oséias',
    email: 'oseias@exemplo.com',
    password: 'senha123',
  });
  console.log(newUser.toJSON());
})();
```

#### **b) Ler registros**
```javascript
// Encontrar todos os usuários
const users = await User.findAll();
console.log(users);

// Encontrar um usuário por ID
const user = await User.findByPk(1);
console.log(user);
```

#### **c) Atualizar registros**
```javascript
const user = await User.findByPk(1);
if (user) {
  user.name = 'Novo Nome';
  await user.save();
  console.log('Usuário atualizado:', user.toJSON());
}
```

#### **d) Deletar registros**
```javascript
const user = await User.findByPk(1);
if (user) {
  await user.destroy();
  console.log('Usuário deletado');
}
```

---

### **6. Relacionamentos**
#### **a) Relacionamento 1:N**
Um usuário pode ter vários posts.

```javascript
const Post = sequelize.define('Post', {
  title: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  content: {
    type: DataTypes.TEXT,
    allowNull: false,
  },
});

User.hasMany(Post, { onDelete: 'CASCADE' });
Post.belongsTo(User);

await sequelize.sync({ force: true });
```

#### **b) Relacionamento N:M**
Um usuário pode pertencer a várias equipes, e uma equipe pode ter vários usuários.

```javascript
const Team = sequelize.define('Team', {
  name: {
    type: DataTypes.STRING,
    allowNull: false,
  },
});

const UserTeam = sequelize.define('UserTeam', {});

User.belongsToMany(Team, { through: UserTeam });
Team.belongsToMany(User, { through: UserTeam });

await sequelize.sync({ force: true });
```

---

### **7. Consultas Avançadas**
#### **a) Filtragem**
```javascript
const users = await User.findAll({
  where: {
    email: 'oseias@exemplo.com',
  },
});
```

#### **b) Ordenação**
```javascript
const users = await User.findAll({
  order: [['createdAt', 'DESC']],
});
```

#### **c) Paginação**
```javascript
const users = await User.findAll({
  limit: 10, // Máximo de registros
  offset: 20, // Pula os 20 primeiros registros
});
```

---

### **8. Migrações e Seeders**
Para projetos maiores, é recomendado usar migrações e seeders.

#### **Instalação**
```bash
npm install sequelize-cli
npx sequelize-cli init
```

Isso cria uma estrutura de pastas (`migrations`, `seeders`, etc.).

#### **Exemplo de Migração**
```bash
npx sequelize-cli migration:generate --name create-users-table
```

No arquivo gerado:

```javascript
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('Users', {
      id: {
        type: Sequelize.INTEGER,
        autoIncrement: true,
        primaryKey: true,
      },
      name: Sequelize.STRING,
      email: Sequelize.STRING,
      createdAt: Sequelize.DATE,
      updatedAt: Sequelize.DATE,
    });
  },
  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('Users');
  },
};
```

---

### **9. Dicas e Boas Práticas**
- **Validações**: Adicione validações nos modelos para evitar erros nos dados.
- **Configurações de Produção**: Use variáveis de ambiente para armazenar informações sensíveis (como senhas).
- **Transações**: Use transações para garantir consistência ao realizar operações complexas.
- **Lazy vs Eager Loading**: Prefira o **eager loading** quando souber de antemão os relacionamentos necessários.

Exemplo de **eager loading**:
```javascript
const users = await User.findAll({
  include: [Post], // Carrega os posts relacionados
});
```

