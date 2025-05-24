
# **Introdução ao Java – Conceitos Fundamentais**

---

## **Como o Java Funciona**

* O arquivo que o ser humano pode entender termina com **`.java`**, que depois se torna **`.class`** — este é, basicamente, a "tradução" do arquivo `.java` para que o computador entenda.

* Quando o arquivo é convertido em **bytecode (`.class`)**, a **Java Virtual Machine (JVM)** faz uma nova tradução, permitindo que o **Sistema Operacional (Linux, Windows ou macOS)** execute o código.

---

## **Estrutura Básica de um Programa Java**

Todo programa Java **sempre começa com a declaração da classe principal**, que **deve ter o mesmo nome do arquivo Java**.

### **Exemplo básico:**

```java
public class Main {
    public static void main(String[] args) {
        // Código aqui
    }
}
```

> **Observação:** O nome da classe é **`Main`**, então o arquivo deve se chamar **`Main.java`**.

---

## **Classe Principal e Método Main**

* **Classe Principal:** Todo programa Java precisa de uma classe pública que tenha o mesmo nome do arquivo.

* **Método Main:** É o **ponto de entrada** do programa.

---

## **Tipos de Dados em Java**

Java é uma linguagem **fortemente tipada**, ou seja, **todas as variáveis precisam ter um tipo definido**.

| Tipo        | Descrição                                   | Exemplo  |
| ----------- | ------------------------------------------- | -------- |
| **boolean** | Valores lógicos (**true/false**)            | `true`   |
| **int**     | Números inteiros                            | `10`     |
| **double**  | Números de ponto flutuante (alta precisão)  | `1.0002` |
| **float**   | Ponto flutuante (menor precisão que double) | `4.75f`  |
| **char**    | Caractere único                             | `'D'`    |
| **String**  | Sequência de caracteres                     | `"Olá"`  |

> **Atenção:** `String` é uma classe, não um tipo primitivo, mas é utilizada como se fosse.

---

## **Operadores em Java**

### **Operadores Matemáticos:**

* `+` (adição)
* `-` (subtração)
* `*` (multiplicação)
* `/` (divisão)
* `%` (módulo — resto da divisão)
* `++` (incremento)
* `--` (decremento)

### **Operadores de Comparação:**

* `==` (igual)
* `!=` (diferente)
* `>` (maior)
* `<` (menor)
* `>=` (maior ou igual)
* `<=` (menor ou igual)

---

## **Entrada e Saída de Dados**

Para capturar dados do teclado em Java, utiliza-se a classe **`Scanner`**, que está no pacote **`java.util`**.

### **Exemplo de entrada de dados:**

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Digite um número: ");
        int numero = scanner.nextInt();

        System.out.println("O número digitado é: " + numero);
    }
}
```

> **Dica de especialista:** Sempre feche o Scanner no final com `scanner.close();` para evitar vazamento de recursos.

---

## **Estruturas de Controle**

### **Condicionais:**

* **if**
* **else**
* **else if**

### **Laços de Repetição:**

* **for**
* **while**
* **do-while**

---

## **Tratamento de Exceções**

O Java oferece um mecanismo robusto para tratar erros, utilizando os blocos **`try`**, **`catch`** e **`finally`**.

### **Exemplo de try-catch-finally:**

```java
try {
    // Código que pode gerar exceções
} catch (ExcecaoTipoA tipoA) {
    // Tratamento para exceções do tipo A
} catch (ExcecaoTipoB tipoB) {
    // Tratamento para exceções do tipo B
} finally {
    // Executa sempre, com ou sem exceção
}
```

---

## **Exemplos Práticos**

### **Exemplo 1: Hello World**

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

---

### **Exemplo 2: Uso de Variáveis**

```java
public class Main {
    public static void main(String[] args) {
        String nome = "João";
        int idade = 20;

        System.out.println("Nome: " + nome);
        System.out.println("Idade: " + idade);
    }
}
```

---

### **Exemplo 3: Estruturas de Controle (If/Else)**

```java
public class Main {
    public static void main(String[] args) {
        int nota = 85;

        if (nota >= 70) {
            System.out.println("Aprovado");
        } else {
            System.out.println("Reprovado");
        }
    }
}
```

---

### **Exemplo 4: Loop For**

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            System.out.println("Número: " + i);
        }
    }
}
```

---

## **Cuidados Importantes em Java**

### **Sensibilidade a Maiúsculas e Minúsculas**

* Java diferencia letras maiúsculas e minúsculas.
* **`public` ≠ `Public`**
* Escrever palavras-chave com maiúsculas gera erro.

### **Operações Compatíveis de Tipos**

* Ao realizar operações, os tipos devem ser compatíveis.

**Exemplo errado:**

```java
int a = 5;
double b = 2.5;
int resultado = a + b; // ERRO: tipos incompatíveis
```

**Solução correta:**

```java
int a = 5;
double b = 2.5;
double resultado = a + b;
```

### **Uso Correto de Métodos**

**Exemplo:**

```java
String texto = "Olá, Mundo!";
int comprimento = texto.length(); // length() retorna um int
```

> **Dica:** Sempre confira na documentação oficial os parâmetros e o tipo de retorno dos métodos.

---

## **Dicas Profissionais**

* Pratique desafios em plataformas como **HackerRank**, **LeetCode** e **Codewars**.
* Crie mini projetos para consolidar seu aprendizado.
* Documente seu código e siga boas práticas desde o início.

---
