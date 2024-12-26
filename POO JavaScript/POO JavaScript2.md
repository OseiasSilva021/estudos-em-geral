
# 🚀 Métodos Getters e Setters em JavaScript 👩‍💻👨‍💻

🎯 **Introdução**  
Os métodos `getter` e `setter` em JavaScript são ferramentas poderosas para controlar o acesso a propriedades de objetos! 🛠️ Eles permitem encapsular a lógica de leitura e escrita de dados, tornando seu código mais seguro, limpo e organizado.  

---

## 🧐 O que são?  
### 🟢 **Getters (`get`)**  
Os métodos *getters* permitem que você "leia" uma propriedade como se ela fosse pública, mas por baixo dos panos, executam uma função. 💡  
```javascript
class Pessoa {
  constructor(nome, sobrenome) {
    this.nome = nome;
    this.sobrenome = sobrenome;
  }

  // Getter
  get nomeCompleto() {
    return `${this.nome} ${this.sobrenome}`;
  }
}

const pessoa = new Pessoa('Oséias', 'Silva');
console.log(pessoa.nomeCompleto); // 👉 "Oséias Silva"
```

### 🔵 **Setters (`set`)**  
Os métodos *setters* permitem modificar uma propriedade enquanto aplicam lógica personalizada, como validações ou transformações. ⚙️  
```javascript
class Pessoa {
  constructor(nome, sobrenome) {
    this.nome = nome;
    this.sobrenome = sobrenome;
  }

  // Setter
  set nomeCompleto(nomeCompleto) {
    const partes = nomeCompleto.split(' ');
    this.nome = partes[0];
    this.sobrenome = partes[1] || '';
  }
}

const pessoa = new Pessoa('Oséias', 'Silva');
pessoa.nomeCompleto = 'João Oliveira';
console.log(pessoa.nome); // 👉 "João"
console.log(pessoa.sobrenome); // 👉 "Oliveira"
```

---

## 🎯 Por que usar getters e setters?  
1. **🔒 Encapsulamento**: Controle o acesso direto às propriedades.  
2. **🎯 Validação de Dados**: Evite dados inválidos sendo atribuídos.  
3. **🤓 Abstração**: Torne seu código mais intuitivo e organizado.  
4. **💾 Compatibilidade**: Permita mudanças futuras sem impactar usuários do seu código.  

---

## ⚠️ Dicas de boas práticas  

1. 🛡️ **Evite lógica pesada nos getters e setters.**  
   - Lembre-se de que getters são chamados como propriedades. Qualquer operação lenta pode afetar o desempenho.  
   
2. 📛 **Nomeação clara.**  
   - Use nomes que façam sentido para quem vai ler seu código.  

3. 🚧 **Não abuse.**  
   - Getters e setters são úteis, mas nem tudo precisa deles. Simplicidade é essencial!  

4. 📚 **Considere usar `Object.defineProperty`.**  
   - Para criar getters e setters em objetos literais:  
   ```javascript
   const user = {
     firstName: 'Oséias',
     lastName: 'Silva'
   };

   Object.defineProperty(user, 'fullName', {
     get() {
       return `${this.firstName} ${this.lastName}`;
     },
     set(value) {
       const parts = value.split(' ');
       this.firstName = parts[0];
       this.lastName = parts[1] || '';
     }
   });

   console.log(user.fullName); // 👉 "Oséias Silva"
   user.fullName = 'Maria Clara';
   console.log(user.firstName); // 👉 "Maria"
   ```

---

## 🔥 Desafios para você!  
1. 🏋️‍♂️ Crie uma classe `Carro` com getters e setters para `modelo`, `ano` e `idadeDoCarro`.  
2. 🧠 Implemente validação nos setters para garantir que nenhum campo seja vazio.  

🌟 **Dica Extra:** Combine getters e setters com APIs e autenticação JWT para criar perfis dinâmicos e seguros!  

---  

💻 **Agora é a sua vez!** Melhore seu código, pratique, e aproveite o poder do JavaScript com *getters* e *setters*! 🎉  
