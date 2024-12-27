# 🧩 Padrão de Projeto Estrutural: Decorator

## 📖 Visão Geral
O **Decorator** é um padrão de projeto estrutural que permite adicionar dinamicamente novos comportamentos a um objeto, sem modificar seu código fonte original. Este padrão segue o princípio de **aberto/fechado**: o código deve estar aberto para extensões, mas fechado para modificações.

---

## 🛠 Quando Usar?
- Quando você precisa adicionar responsabilidades a objetos individualmente e de forma dinâmica.
- Quando não é possível modificar diretamente o código da classe.
- Para evitar uma explosão de subclasses ao tentar cobrir todas as combinações de funcionalidades.

### 📝 Benefícios
- **Extensível:** Permite adicionar funcionalidades sem alterar o código original.
- **Flexível:** Combinações de comportamentos são aplicadas em tempo de execução.
- **Modularidade:** Torna o código mais organizado e reutilizável.

---

## 🚀 Implementação

### 🧑‍💻 Exemplo em JavaScript
```javascript
// Componente base
class Coffee {
  cost() {
    return 5;
  }

  description() {
    return "Café simples";
  }
}

// Decorador base
class CoffeeDecorator {
  constructor(coffee) {
    this.coffee = coffee;
  }

  cost() {
    return this.coffee.cost();
  }

  description() {
    return this.coffee.description();
  }
}

// Decoradores concretos
class MilkDecorator extends CoffeeDecorator {
  cost() {
    return this.coffee.cost() + 2;
  }

  description() {
    return this.coffee.description() + ", leite";
  }
}

class SugarDecorator extends CoffeeDecorator {
  cost() {
    return this.coffee.cost() + 1;
  }

  description() {
    return this.coffee.description() + ", açúcar";
  }
}

// Uso
let coffee = new Coffee();
console.log(coffee.description() + " custa R$" + coffee.cost());

coffee = new MilkDecorator(coffee);
console.log(coffee.description() + " custa R$" + coffee.cost());

coffee = new SugarDecorator(coffee);
console.log(coffee.description() + " custa R$" + coffee.cost());
```

### 🧑‍💻 Exemplo em Python
```python
class Coffee:
    def cost(self):
        return 5

    def description(self):
        return "Café simples"

# Decorador base
class CoffeeDecorator:
    def __init__(self, coffee):
        self._coffee = coffee

    def cost(self):
        return self._coffee.cost()

    def description(self):
        return self._coffee.description()

# Decoradores concretos
class MilkDecorator(CoffeeDecorator):
    def cost(self):
        return self._coffee.cost() + 2

    def description(self):
        return self._coffee.description() + ", leite"

class SugarDecorator(CoffeeDecorator):
    def cost(self):
        return self._coffee.cost() + 1

    def description(self):
        return self._coffee.description() + ", açúcar"

# Uso
coffee = Coffee()
print(f"{coffee.description()} custa R${coffee.cost()}")

coffee = MilkDecorator(coffee)
print(f"{coffee.description()} custa R${coffee.cost()}")

coffee = SugarDecorator(coffee)
print(f"{coffee.description()} custa R${coffee.cost()}")
```

---

## ⚠️ Cuidados ao Usar
- **Complexidade:** Muitos decoradores encadeados podem dificultar a manutenção do código.
- **Desempenho:** Decoradores em excesso podem impactar negativamente o desempenho.

---

## 🌟 Conclusão
O Decorator é uma solução elegante e flexível para adicionar funcionalidades a objetos de forma dinâmica. Utilize este padrão com moderação e avalie a necessidade de balancear simplicidade e extensibilidade. 💡

