
# 🧪 **Desenvolvimento Orientado a Testes (TDD)**

## 📚 **O que é TDD?**

**Desenvolvimento Orientado a Testes (TDD)** é uma abordagem de desenvolvimento de software onde **testes são escritos antes de escrever o código de produção**. Essa prática ajuda a garantir que o código esteja funcionando corretamente, promove o design modular e extensível e melhora a cobertura de testes.

### Como funciona o TDD? 🤔

TDD segue um ciclo simples e poderoso conhecido como **Red-Green-Refactor**:
1. **Red**: Escreva um **teste falho** para a funcionalidade que você vai implementar.
2. **Green**: Escreva o código **mínimo necessário** para fazer o teste passar.
3. **Refactor**: Refatore o código para melhorar a qualidade e a estrutura, sem mudar seu comportamento.

---

## 🔄 **Ciclo do TDD (Red-Green-Refactor)**

### 1️⃣ **Red (Teste Falho)**
   - O primeiro passo no TDD é escrever um **teste que falha**. Esse teste deve cobrir o comportamento esperado do código que será implementado.

   **Exemplo**: Se você está criando uma função para somar dois números, o primeiro passo é escrever um teste que falha.
   
   ```javascript
   test('soma dois números', () => {
     expect(soma(2, 3)).toBe(5); // Esse teste vai falhar inicialmente, pois a função soma ainda não existe.
   });
   ```

### 2️⃣ **Green (Código Mínimo)**
   - O segundo passo é escrever o código **mínimo necessário** para fazer o teste passar. A ideia é escrever apenas o suficiente para que o teste seja bem-sucedido.

   **Exemplo**: Agora, implementamos a função `soma` para passar no teste.
   
   ```javascript
   function soma(a, b) {
     return a + b; // Implementação simples para passar no teste
   }
   ```

   Após a implementação, o teste agora deve passar, indicando que a funcionalidade está correta (pelo menos no caso básico que testamos).

### 3️⃣ **Refactor (Refatoração)**
   - Após ter o teste funcionando, o próximo passo é **refatorar** o código para torná-lo mais limpo, eficiente ou legível. Importante: a refatoração **não deve alterar o comportamento do código**, apenas melhorar sua estrutura.

   **Exemplo**: Podemos melhorar a legibilidade do código ou adicionar validações sem alterar o comportamento da função.

   ```javascript
   function soma(a, b) {
     if (typeof a !== 'number' || typeof b !== 'number') {
       throw new Error('Ambos os parâmetros devem ser números');
     }
     return a + b;
   }
   ```

---

## 🔧 **Benefícios do TDD**

### ✔️ **Melhoria da Qualidade do Código**
   - Com TDD, o código é testado desde o início, o que ajuda a evitar bugs e regressões ao longo do desenvolvimento.

### ✔️ **Design Modular e Extensível**
   - Ao escrever testes primeiro, você é forçado a **pensar em unidades pequenas e coesas** de código, o que leva a um design mais modular e fácil de estender.

### ✔️ **Maior Cobertura de Testes**
   - Como os testes são escritos antes do código, há uma **maior cobertura de testes**, o que ajuda a garantir que a funcionalidade esteja bem testada.

### ✔️ **Feedback Imediato**
   - O ciclo rápido de escrever o teste, implementar o código e refatorar oferece **feedback imediato**, permitindo que os desenvolvedores corrijam problemas rapidamente.

---

## 🚀 **Exemplo Prático de TDD**

Aqui está um exemplo prático de como aplicar TDD em uma função simples.

### Objetivo: Criar uma função que calcule o fatorial de um número.

1. **Escreva o Teste (Red)**:
   
   ```javascript
   test('calcula fatorial de 5', () => {
     expect(fatorial(5)).toBe(120); // O teste falha porque ainda não implementamos a função
   });
   ```

2. **Escreva o Código Mínimo (Green)**:
   
   ```javascript
   function fatorial(n) {
     if (n === 0 || n === 1) {
       return 1;
     }
     return n * fatorial(n - 1);
   }
   ```

3. **Refatoração (Refactor)**:

   O código já está funcional, mas podemos refatorá-lo para verificar se há valores inválidos:

   ```javascript
   function fatorial(n) {
     if (n < 0) throw new Error('Número não pode ser negativo');
     if (n === 0 || n === 1) return 1;
     return n * fatorial(n - 1);
   }
   ```

---

## 📈 **Dicas para Implementar TDD**

1. **Comece Pequeno** 🍀
   - Comece com pequenas funções e escreva testes para funcionalidades simples. À medida que ganha confiança, pode começar a testar funcionalidades mais complexas.

2. **Escreva Testes para Casos de Erro** 🚨
   - Não se concentre apenas no "caminho feliz" (quando tudo funciona como esperado), mas também escreva testes para situações inesperadas ou casos de erro (por exemplo, entrada inválida).

3. **Não Tenha Medo de Refatorar** 🔧
   - O TDD permite que você refatore o código com segurança, já que os testes garantirão que a funcionalidade não seja quebrada. Não tenha medo de melhorar o design!

4. **Use Ferramentas de Teste** 🛠️
   - Utilize frameworks de teste como **Jest**, **Mocha** ou **Jasmine** para facilitar a escrita e execução dos testes.

   **Exemplo de Instalação do Jest**:
   ```bash
   npm install --save-dev jest
   ```

   **Exemplo de comando para rodar os testes**:
   ```bash
   npm test
   ```

---

## 🔑 **Conclusão**

O **Desenvolvimento Orientado a Testes (TDD)** é uma prática poderosa que melhora a qualidade do código, o design e a cobertura de testes. Com o ciclo **Red-Green-Refactor**, os desenvolvedores conseguem criar código confiável, modular e bem testado, o que resulta em aplicações mais robustas e sustentáveis.

Se você ainda não aplicou TDD, **dê o primeiro passo hoje mesmo**! Comece pequeno, escreva testes para suas funcionalidades e veja a qualidade do seu código crescer! 🚀

---

## 📚 **Recursos Adicionais**

- [Documentação do Jest](https://jestjs.io/docs/getting-started)
- [Tutorial de TDD com JavaScript](https://www.freecodecamp.org/news/test-driven-development-tdd-with-javascript/)
