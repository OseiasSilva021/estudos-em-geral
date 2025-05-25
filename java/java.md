

# **ROADMAP DEFINITIVO DE JAVA ENTERPRISE**

### **Objetivo:**

Sair de zero (ou básico) até domínio de **Java Enterprise**, incluindo back-end, microserviços, cloud, alta performance, arquitetura e boas práticas exigidas no mercado.

---

## **1. FUNDAMENTOS ABSOLUTOS DE JAVA (BASE INQUEBRÁVEL)**

### Aprender:

* Sintaxe Java
* Tipos primitivos e objetos
* Operadores
* Estruturas de controle (if, switch, loops)
* Manipulação de Strings
* Entrada e saída básica
* Tratamento de exceções (checked vs unchecked)

### Foco:

* **Dominar a sintaxe sem dúvidas.**
* Praticar criando mini-programas, como calculadoras, jogos simples (ex.: adivinhação), conversores de temperatura, etc.

### Ferramentas:

* **IntelliJ IDEA Community (recomendado) ou Eclipse.**
* Java 17 ou 21 LTS.

---

## **2. ORIENTAÇÃO A OBJETOS PROFISSIONAL**

### Aprender:

* Classes, objetos, instância
* Encapsulamento, herança, polimorfismo
* Abstração (interfaces vs classes abstratas)
* Modificadores de acesso (public, private, protected)
* Métodos estáticos vs de instância
* Construtores, sobrecarga
* Uso de `this` e `super`

### Foco:

* **Desenvolver mentalidade OOP**, modelar entidades do mundo real.
* Criar sistemas simulados: banco, loja, sistema de cadastro.

### Ferramenta de prática:

* Diagramas UML simples (usar PlantUML ou Lucidchart).

---

## **3. CONCEITOS AVANÇADOS DE OOP + ARQUITETURA DE CÓDIGO**

### Aprender:

* Princípios **SOLID** aplicados no Java
* **Design Patterns essenciais**: Singleton, Factory, Strategy, Observer, Builder, Adapter, etc.
* Composição vs herança
* Generics avançado (`<?>, <? extends>, <? super>`)
* Enum avançado com métodos
* Classes internas, anônimas, estáticas

### Foco:

* Escrever código limpo, reutilizável e fácil de manter.
* Entender arquitetura de código e design orientado a objetos real.

---

## **4. COLLECTIONS FRAMEWORK E ESTRUTURAS DE DADOS NO JAVA**

### Aprender:

* List, Set, Map: diferenças e aplicações
* ArrayList vs LinkedList
* HashMap vs TreeMap vs LinkedHashMap
* HashSet vs TreeSet
* Iteradores, loops aprimorados
* Comparator vs Comparable
* Utilitários da classe `Collections`

### Foco:

* Saber escolher a estrutura certa para cada problema.
* Simular cenários como carrinho de compras, cache, indexação, etc.

---

## **5. PROGRAMAÇÃO FUNCIONAL MODERNA (JAVA 8+)**

### Aprender:

* Lambdas na prática
* Functional Interfaces: Predicate, Function, Consumer, Supplier
* Stream API: filter, map, reduce, collect
* Optional (evitar NullPointerException)
* Method References
* Parallel Streams (e seus perigos)

### Foco:

* Escrever código conciso, expressivo e funcional.
* Migrar códigos imperativos para funcionais.

---

## **6. CONCORRÊNCIA E MULTITHREADING (NÍVEL AVANÇADO)**

### Aprender:

* Ciclo de vida de Thread
* Sincronização (`synchronized`, Locks)
* Problemas clássicos: deadlock, race conditions
* Collections thread-safe
* Executor Framework
* CompletableFuture (programação assíncrona)
* java.util.concurrent em detalhes

### Foco:

* Desenvolver sistemas robustos que fazem várias tarefas simultâneas.
* Saber quando e como usar paralelismo corretamente.

---

## **7. I/O, SERIALIZAÇÃO E NETWORKING**

### Aprender:

* File I/O (`java.io` e `java.nio`)
* Streams de bytes e caracteres
* Serialização e deserialização de objetos
* Manipular JSON (Gson, Jackson)
* Networking básico (Sockets)

### Foco:

* Desenvolver aplicações que leem/escrevem arquivos, comunicam-se via rede, e manipulam dados persistentes.

---

## **8. ACESSO A BANCO DE DADOS (JDBC)**

### Aprender:

* Conexão JDBC
* Statement vs PreparedStatement
* Manipulação de ResultSet
* Connection Pool (HikariCP)
* Controle de transações
* DAO Pattern (Data Access Object)

### Foco:

* Construir aplicações CRUD robustas conectadas a bancos relacionais (MySQL, PostgreSQL, Oracle).

---

## **9. FRAMEWORKS ENTERPRISE ESSENCIAIS**

### Spring Framework:

* **Spring Core:** Inversão de Controle (IoC) e Injeção de Dependências (DI)
* **Spring Boot:** configuração zero para microserviços
* **Spring MVC:** APIs REST
* **Spring Data JPA:** integração com bancos
* **Spring Security:** autenticação, autorização
* **Spring Cloud:** microserviços, Eureka, Config Server, Circuit Breaker

### Hibernate / JPA:

* Mapeamento objeto-relacional
* CRUD avançado
* Relacionamentos (OneToMany, ManyToMany)

### Ferramentas auxiliares:

* Maven/Gradle
* JUnit (testes unitários)
* Mockito (testes com mocks)

---

## **10. PERFORMANCE E OTIMIZAÇÃO DE SISTEMAS JAVA**

### Aprender:

* JVM tuning
* Garbage Collector (G1GC, ZGC)
* Memory Management
* Profiling (VisualVM, JConsole, JProfiler)
* Micro-benchmarking com JMH
* Boas práticas para aplicações de alta performance

### Foco:

* Escrever sistemas escaláveis, rápidos e eficientes.

---

## **11. SEGURANÇA EM JAVA**

### Aprender:

* Criptografia básica (AES, RSA)
* SSL/TLS em aplicações
* JWT (JSON Web Token)
* Validação e sanitização de inputs
* Prevenção de SQL Injection, XSS, CSRF

### Foco:

* Garantir que sua aplicação não seja vulnerável a ataques comuns.

---

## **12. FERRAMENTAS PROFISSIONAIS E DEVOPS PARA JAVA**

### Aprender:

* IDEs: IntelliJ, Eclipse, VS Code
* Git avançado (branches, rebases, squash)
* CI/CD: GitHub Actions, GitLab CI, Jenkins
* Docker (conteinerização de aplicações Java)
* Kubernetes básico (deployment de microsserviços)
* Observabilidade: logs (Logback, Log4j), métricas (Micrometer, Prometheus), tracing (Jaeger)

---

## **13. ARQUITETURA DE SISTEMAS ENTERPRISE EM JAVA**

### Aprender:

* Arquitetura Monolítica vs Microsserviços
* Clean Architecture
* Hexagonal Architecture
* Event-driven (RabbitMQ, Kafka)
* Design para escalabilidade horizontal
* Padrões como Circuit Breaker, API Gateway, Service Discovery

### Foco:

* Ser capaz de desenhar, desenvolver e escalar sistemas de alta complexidade.

---

## **MÉTODO DE ESTUDO ACELERADO**

### **Dividir em 4 etapas:**

1. **FUNDAMENTAÇÃO:** Java básico + OOP + Collections → 2 a 3 semanas
2. **NIVELAMENTO PROFISSIONAL:** Design Patterns + Programação Funcional + JDBC + Multithreading → 3 semanas
3. **ENTERPRISE:** Spring Boot + JPA + Segurança + Arquitetura → 4 a 5 semanas
4. **MAESTRIA:** Performance, Segurança Avançada, Kubernetes, Microsserviços, Cloud → Contínuo

### **Rotina Ideal:**

* **3 a 4 horas por dia.**
* 70% prática (código) + 30% teoria.
* Fazer projetos próprios simulando empresas (API, e-commerce, banco, rede social, etc.).
* Resolver desafios do LeetCode, HackerRank focando em algoritmos + entrevistas.

---

## **CHECKLIST DE PROJETOS QUE VOCÊ DEVE CONSTRUIR:**

* [ ] CRUD com JDBC puro
* [ ] API REST com Spring Boot + JPA
* [ ] Sistema de autenticação JWT
* [ ] Microsserviço com comunicação via RabbitMQ ou Kafka
* [ ] Aplicação containerizada com Docker
* [ ] Deploy na nuvem (AWS, Azure ou Google Cloud)

---

## **FERRAMENTAS PARA APRENDER JUNTO:**

* **Documentação oficial:** [https://docs.oracle.com/en/java/](https://docs.oracle.com/en/java/)
* **Spring Docs:** [https://spring.io/docs](https://spring.io/docs)
* **Livro:** *Effective Java (Joshua Bloch)*
* **Livro:** *Clean Code (Robert C. Martin)*
* **Cursos recomendados:** Alura, Udemy, Pluralsight, ou canal Amigos do Código (gratuito)


---

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


# Fundamentos de Java
## Estrutura Básica de uma Classe Java
Em Java, sempre que você cria uma classe, ela é definida com o uso de `public class`, e os métodos, como `main`, são definidos dentro dessa estrutura.
É por meio do método `main` que o código Java é executado.
---



## Encapsulamento

O **encapsulamento** é um dos pilares da programação orientada a objetos (POO). Ele permite que você **controle o acesso às propriedades de uma classe**, protegendo seus dados.
Em Java, isso é feito por meio de **modificadores de acesso**:
- `public`
- `private`
- `protected`
Essa abordagem garante a **segurança e integridade dos dados manipulados**.
🔗 **Leituras recomendadas:**
- [Entendendo os modificadores de acesso em Java](https://www.rocketseat.com.br/blog/artigos/post/entendendo-os-modificadores-de-acesso-em-java)
- [Encapsulamento em Java: Getters e Setters](https://www.rocketseat.com.br/blog/artigos/post/encapsulamento-em-java-getters-setters)
---
## Construtores
Os **construtores** são usados para **inicializar objetos em Java**. Eles são métodos especiais que:
- Possuem o **mesmo nome da classe**.
- **Não têm tipo de retorno**.
Ao criar um objeto, o construtor é chamado automaticamente para inicializar suas propriedades.
### Exemplo:
```java
public class Carro {
String marca;
int ano;
// Construtor
public Carro(String marca, int ano) {
this.marca = marca;
this.ano = ano;
}
}
````
🔗 **Saiba mais:** Guia completo sobre **Java: Construtores**.
---
## Vetores em Java
Os **vetores (arrays)** são uma forma básica de armazenar **múltiplos valores do mesmo tipo** em uma única variável.
* Têm **tamanho fixo**.
* Podem armazenar qualquer tipo de dado primitivo ou objetos.
### Exemplo:
```java
int[] numeros = {1, 2, 3, 4, 5};
System.out.println(numeros[0]); // Imprime 1
```
> ⚠️ **Atenção:** Se você tentar acessar um índice que não existe, obterá uma exceção `ArrayIndexOutOfBoundsException`.
### Alternativas mais flexíveis:
* `ArrayList` (do pacote `java.util`) permite adicionar e remover elementos dinamicamente.
🔗 **Leitura recomendada:** [Java: Guia sobre Vetores](https://www.rocketseat.com.br/blog/artigos/post/java-guia-sobre-vetores)
---
## Estruturas de Repetição
Laços de repetição permitem que um bloco de código seja executado várias vezes com base em uma condição.
### Principais laços em Java:
* `for`
* `while`
### Exemplo com `for`:
```java
for (int i = 0; i < 5; i++) {
System.out.println(i);
}
```
> ✅ **Uso comum:** percorrer elementos de vetores, listas, coleções e executar tarefas repetitivas.
🔗 **Saiba mais:** [Java: Estruturas de Repetição](https://www.rocketseat.com.br/blog/artigos/post/java-estruturas-de-repeticao)
---
## Ferramentas Importantes no Mundo Java
### O que é Maven?
O **Maven** é uma ferramenta de:
* **Gerenciamento de dependências.**
* **Automatização da construção (build) de projetos Java.**
### Benefícios:
* Facilita adicionar bibliotecas externas.
* Automatiza processos como compilação, testes e empacotamento.
* Padroniza a estrutura dos projetos.
### 💡 **Observação:** O Maven é amplamente usado em conjunto com frameworks como **Spring Boot**.
🔗 **Leitura recomendada:** [Java Maven e Spring Boot Initializr](https://www.rocketseat.com.br/blog/artigos/post/java-maven-e-spring-boot-initializr)
---
## Programação Orientada a Objetos em Java
Java é uma linguagem **fortemente baseada na Programação Orientada a Objetos (POO)**.
### 📌 **Pilares da POO:**
1. **Abstração:**
* Foca apenas nos detalhes essenciais, escondendo a complexidade.
2. **Encapsulamento:**
* Controla o acesso aos atributos de um objeto.
3. **Herança:**
* Permite que uma classe herde atributos e métodos de outra classe.
4. **Polimorfismo:**
* Objetos diferentes podem responder de formas diferentes ao mesmo método.
> ⚠️ **Dominar POO em Java é obrigatório para escrever código limpo, escalável e de fácil manutenção.**
---
## 🚀 Considerações Finais
Entender esses conceitos não é apenas teórico — eles são **essenciais no desenvolvimento profissional com Java**, especialmente em aplicações backend, sistemas corporativos e APIs robustas.

# Tipos de Dados em Java  

---

## Introdução

Em Java, os tipos de dados desempenham um papel fundamental na definição e manipulação de informações dentro de um programa. Neste artigo, exploramos os diferentes tipos de dados em Java, incluindo:

- Tipos Primitivos
- Tipos Definidos pelo Usuário
- Tipos Complexos

Entender esses tipos é essencial para desenvolver aplicativos robustos, escaláveis e eficientes em Java.

---

## Tipos de Dados Primitivos

Os tipos de dados primitivos representam os valores mais básicos e fundamentais que a linguagem pode manipular. Java possui **oito tipos primitivos**, que são:

| Tipo    | Tamanho | Descrição                                  |
|---------|---------|---------------------------------------------|
| `byte`  | 8 bits  | Inteiro pequeno                            |
| `short` | 16 bits | Inteiro curto                              |
| `int`   | 32 bits | Inteiro padrão                             |
| `long`  | 64 bits | Inteiro longo                              |
| `float` | 32 bits | Ponto flutuante de precisão simples        |
| `double`| 64 bits | Ponto flutuante de precisão dupla          |
| `char`  | 16 bits | Caractere Unicode                          |
| `boolean`| 1 bit* | Valor lógico (`true` ou `false`)           |

> **Nota:** O tipo `boolean` tecnicamente ocupa 1 bit conceitualmente, mas na prática pode ocupar 1 byte ou mais, dependendo da JVM.

Esses tipos são altamente performáticos, armazenados diretamente na pilha (stack) quando não estão encapsulados, e são ideais para valores simples como números, caracteres e lógicos.

---

## Tipos de Dados Definidos pelo Usuário

Além dos primitivos, Java permite criar tipos personalizados utilizando **classes**, **interfaces**, **enums** e **records** (a partir do Java 14+).

### Exemplo de Classe:

```java
public class Pessoa {
    private String nome;
    private int idade;

    // Construtor
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }

    // Getters e Setters
    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getIdade() {
        return idade;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }
}
````

> **Observação:** Tipos definidos pelo usuário são fundamentais para aplicar os princípios de **Programação Orientada a Objetos (POO)** como encapsulamento, herança e polimorfismo.

---

## Tipos de Dados Complexos

Java oferece tipos complexos que são estruturas de dados prontas para manipular coleções e objetos mais sofisticados.

### Exemplos de tipos complexos:

* **Arrays:** Coleções ordenadas de elementos do mesmo tipo.
* **Strings:** Sequências de caracteres (classe `String` é imutável).
* **Coleções:** Estruturas como `List`, `Set`, `Map` (disponíveis no pacote `java.util`).

### Exemplo com Array e Lista:

```java
import java.util.ArrayList;
import java.util.List;

public class Exemplo {
    public static void main(String[] args) {
        // Array de inteiros
        int[] numeros = {1, 2, 3, 4, 5};

        // Lista de strings
        List<String> nomes = new ArrayList<>();
        nomes.add("Alice");
        nomes.add("Bob");
        nomes.add("Carol");

        // Iterando sobre o array
        for (int numero : numeros) {
            System.out.println(numero);
        }

        // Iterando sobre a lista
        for (String nome : nomes) {
            System.out.println(nome);
        }
    }
}
```

> **Dica Profissional:** Prefira coleções (`List`, `Set`, `Map`) no lugar de arrays sempre que precisar de flexibilidade, dinamismo ou operações mais sofisticadas. Arrays são mais performáticos, mas limitados em funcionalidade.

---

## Conclusão

Os tipos de dados são a base da construção de qualquer software em Java. Compreender os diferentes tipos — primitivos, definidos pelo usuário e complexos — permite:

* Modelar dados do mundo real de forma precisa.
* Escrever código mais limpo, eficiente e escalável.
* Aplicar boas práticas de desenvolvimento orientado a objetos.

> **Recomendação:** Pratique implementando classes, manipulando coleções e entendendo como os tipos interagem na memória (heap vs stack). Isso te tornará um desenvolvedor Java muito mais sólido.

---

## Próximos Passos

* Explore outros tópicos como **Generics**, **Enums**, **Records** e **Imutabilidade** em Java.
* Aprofunde-se nas APIs de Collections e Streams.
* Pratique projetos reais aplicando esses conceitos.

---

