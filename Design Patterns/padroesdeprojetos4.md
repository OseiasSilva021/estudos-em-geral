# ⚙️ Padrão de Projeto Comportamental: Command

## 📖 Visão Geral
O **Command** é um padrão de projeto comportamental que transforma uma solicitação em um objeto autônomo, permitindo parametrizar outros objetos com diferentes solicitações, enfileirar ou registrar solicitações e suportar operações reversíveis.

---

## 🛠 Quando Usar?
- Quando você precisa encapsular uma solicitação como um objeto.
- Para implementar operações que podem ser desfeitas ou refeitas.
- Para organizar comandos em filas, logs ou para implementações de transação.

### 📝 Benefícios
- **Desacoplamento:** Separa o objeto que emite uma solicitação daquele que a executa.
- **Flexibilidade:** Fácil adicionar novos comandos sem modificar o código existente.
- **Reversibilidade:** Suporte às operações de desfazer e refazer.

---

## 🚀 Implementação

### 🧑‍💻 Exemplo em JavaScript
```javascript
// Comando base
class Command {
  execute() {}
  undo() {}
}

// Comandos concretos
class LightOnCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.on();
  }

  undo() {
    this.light.off();
  }
}

class LightOffCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.off();
  }

  undo() {
    this.light.on();
  }
}

// Receptor
class Light {
  on() {
    console.log("A luz está ligada");
  }

  off() {
    console.log("A luz está desligada");
  }
}

// Invocador
class RemoteControl {
  setCommand(command) {
    this.command = command;
  }

  pressButton() {
    this.command.execute();
  }

  pressUndo() {
    this.command.undo();
  }
}

// Uso
const light = new Light();
const lightOn = new LightOnCommand(light);
const lightOff = new LightOffCommand(light);
const remote = new RemoteControl();

remote.setCommand(lightOn);
remote.pressButton(); // A luz está ligada
remote.pressUndo();   // A luz está desligada

remote.setCommand(lightOff);
remote.pressButton(); // A luz está desligada
remote.pressUndo();   // A luz está ligada
```

### 🧑‍💻 Exemplo em Python
```python
from abc import ABC, abstractmethod

# Comando base
class Command(ABC):
    @abstractmethod
    def execute(self):
        pass

    @abstractmethod
    def undo(self):
        pass

# Comandos concretos
class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.on()

    def undo(self):
        self.light.off()

class LightOffCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.off()

    def undo(self):
        self.light.on()

# Receptor
class Light:
    def on(self):
        print("A luz está ligada")

    def off(self):
        print("A luz está desligada")

# Invocador
class RemoteControl:
    def __init__(self):
        self.command = None

    def set_command(self, command):
        self.command = command

    def press_button(self):
        self.command.execute()

    def press_undo(self):
        self.command.undo()

# Uso
light = Light()
light_on = LightOnCommand(light)
light_off = LightOffCommand(light)
remote = RemoteControl()

remote.set_command(light_on)
remote.press_button()  # A luz está ligada
remote.press_undo()    # A luz está desligada

remote.set_command(light_off)
remote.press_button()  # A luz está desligada
remote.press_undo()    # A luz está ligada
```

---

## ⚠️ Cuidados ao Usar
- **Overhead:** Pode introduzir complexidade extra em aplicações simples.
- **Manutenção:** Muitas classes de comandos podem aumentar o esforço de manutenção.

---

## 🌟 Conclusão
O Command é uma excelente escolha para encapsular solicitações e promover flexibilidade no código. Use-o para melhorar a organização e permitir operações reversíveis. Experimente e implemente! 🚀

