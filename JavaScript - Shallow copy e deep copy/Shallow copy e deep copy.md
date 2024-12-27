

# 📝 **Shallow Copy vs Deep Copy em JavaScript**  

> 📚 Entenda as diferenças entre cópias superficiais e profundas e saiba quando utilizá-las no seu código!  

## 📖 **O que é Shallow Copy?**  
Uma **shallow copy (cópia superficial)** copia apenas o **primeiro nível** do objeto ou array.  
Se houver referências a objetos aninhados, a cópia mantém a referência ao mesmo lugar na memória.  

### ⚠️ **Atenção!**
Modificações nos objetos aninhados da cópia também irão refletir no original.  

### ✅ **Exemplo de Shallow Copy**
```javascript
const original = {
  nome: "Oséias",
  habilidades: { frontend: true, backend: false },
};

const copiaShallow = { ...original }; // Shallow Copy usando spread operator

console.log(copiaShallow.habilidades === original.habilidades); // true (mesma referência)

// Alterando um objeto aninhado na cópia
copiaShallow.habilidades.frontend = false;

console.log(original.habilidades.frontend); // false (o original também foi alterado)
```

### 🛠️ **Métodos de Shallow Copy**  
1. **Spread Operator** (`...`)  
   ```javascript
   const copia = { ...original };
   const copiaArray = [...arrayOriginal];
   ```
2. **Object.assign()**  
   ```javascript
   const copia = Object.assign({}, original);
   ```
3. **Array.prototype.slice()** (para arrays)  
   ```javascript
   const copia = arrayOriginal.slice();
   ```

---

## 📖 **O que é Deep Copy?**  
Uma **deep copy (cópia profunda)** copia **todo o objeto**, incluindo referências aninhadas, criando novas instâncias na memória.  

### ✅ **Exemplo de Deep Copy**
```javascript
const original = {
  nome: "Oséias",
  habilidades: { frontend: true, backend: false },
};

// Criando uma deep copy
const copiaDeep = JSON.parse(JSON.stringify(original));

console.log(copiaDeep.habilidades === original.habilidades); // false (referência diferente)

// Alterando um objeto aninhado na cópia
copiaDeep.habilidades.frontend = false;

console.log(original.habilidades.frontend); // true (o original permanece intacto)
```

### 🛠️ **Métodos de Deep Copy**  
1. **JSON.parse() + JSON.stringify()**  
   **🔍 Limitação:** Não funciona com objetos que contenham funções, undefined ou valores especiais como `Date`.  
   ```javascript
   const copia = JSON.parse(JSON.stringify(original));
   ```
2. **Bibliotecas externas** (ex.: Lodash)  
   ```javascript
   const _ = require("lodash");
   const copia = _.cloneDeep(original);
   ```
3. **Recursão manual**  
   ```javascript
   function deepCopy(obj) {
     if (obj === null || typeof obj !== "object") return obj;

     const copia = Array.isArray(obj) ? [] : {};
     for (const key in obj) {
       copia[key] = deepCopy(obj[key]);
     }
     return copia;
   }

   const copia = deepCopy(original);
   ```

---

## 🎭 **Comparação Final**
| Característica             | Shallow Copy                             | Deep Copy                                |
|----------------------------|------------------------------------------|------------------------------------------|
| 🔗 Referência               | Copia apenas o primeiro nível            | Copia todos os níveis (nova memória)     |
| 🕒 Velocidade               | Mais rápido                              | Mais lento                               |
| 💡 Uso recomendado          | Objetos simples                         | Objetos aninhados ou complexos           |
| ❗ Cuidado                  | Pode causar efeitos colaterais          | Mais seguro, mas exige mais processamento |

---

## ⚡ **Dicas Rápidas**  
- Use **shallow copy** para objetos simples ou quando performance é essencial.  
- Opte por **deep copy** em objetos complexos para evitar bugs difíceis de rastrear.  
- Considere ferramentas como Lodash para lidar com objetos aninhados de forma eficiente.  


