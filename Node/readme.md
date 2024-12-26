# 🚀 Introdução ao **Node.js**

## O que é o **Node.js**? 🌐

**Node.js** é uma **plataforma de desenvolvimento open-source** e multiplataforma que permite executar código **JavaScript** no lado do servidor. Ele é construído sobre o mecanismo **V8** do Google Chrome, o que torna a execução de **JavaScript** mais rápida e eficiente ⚡. Ao contrário do **JavaScript** tradicionalmente executado em navegadores, o **Node.js** permite que o código **JavaScript** seja executado fora do ambiente do navegador, possibilitando a criação de servidores 🖥️, aplicações web 🌍, ferramentas de linha de comando 🖱️, APIs 🔗, entre outros.

**Node.js** é frequentemente usado para desenvolver back-end de aplicações web, por sua alta performance ⚡, facilidade de escalabilidade 📈 e vasto ecossistema de pacotes de terceiros que podem ser gerenciados com o npm (Node Package Manager) 📦.

## Entenda a diferença entre **Node.js** e **JavaScript** no navegador 🌍 vs 🖥️

### **JavaScript** no navegador 🌐

O **JavaScript** no navegador é executado dentro de um ambiente controlado pelo próprio navegador 🖱️. Ele é utilizado para manipular o DOM (Document Object Model) 🧩, interagir com o usuário 👥 e fazer requisições assíncronas 🔄, como chamadas AJAX. A execução é limitada ao contexto do navegador, ou seja, você não pode acessar o sistema de arquivos ou a rede diretamente 🔒.

### **Node.js** 🖥️

Ao contrário do **JavaScript** no navegador, **Node.js** permite que o **JavaScript** seja executado no servidor 🌐 e tenha acesso a recursos do sistema, como o sistema de arquivos 📁, rede 🌍 e processos ⚙️. **Node.js** é projetado para construir aplicações de alto desempenho 🏎️ que requerem manipulação de dados em tempo real ⏱️, como chats 💬, jogos online 🎮 e servidores web 🌐.

# 🛠️ Arquitetura do **Node.js** (Event-driven, Non-blocking)

**Node.js** adota uma arquitetura baseada em eventos 🔔 e não-bloqueante 🚫, o que significa que ele é altamente eficiente para processar múltiplas requisições simultâneas ⚡.

## Event-driven (Baseado em eventos) 🎉

Em **Node.js**, operações como leitura de arquivos 📂, requisições HTTP 🌐 e interações com bancos de dados 🏦 são tratadas por meio de eventos 🔔. Ao invés de bloquear a execução do programa enquanto espera uma resposta (como acontece em outras linguagens de programação tradicionais), **Node.js** emite um evento quando a operação é concluída 🏁. Isso permite que o **Node.js** continue processando outras requisições enquanto aguarda a conclusão de operações mais lentas ⏳.

## Non-blocking (Não-bloqueante) 🚫

A característica não-bloqueante de **Node.js** significa que ele não espera que uma operação seja completada para passar para a próxima 🚀. Isso é especialmente útil para aplicações de I/O (entrada/saída) 📥📤, onde a espera por dados de um banco de dados ou de uma rede pode ser feita sem interromper a execução do restante do programa ⚙️. Em vez disso, **Node.js** faz uso de callbacks, promises e async/await para gerenciar operações assíncronas ⏱️.

Essa arquitetura torna o **Node.js** muito eficiente para aplicações que requerem alta escalabilidade 📈, como servidores web que precisam lidar com múltiplas requisições simultâneas 🚀.

## Instalação do **Node.js** e npm (Node Package Manager) ⚙️

Para começar a usar o **Node.js**, você precisa instalá-lo em sua máquina 💻. Aqui estão os passos gerais:

### 1. Instalar o **Node.js** 🔧

- Acesse o site oficial do **Node.js**: [https://nodejs.org](https://nodejs.org) 🌐.
- Escolha a versão mais recente do **Node.js** (geralmente, você terá uma versão "LTS" recomendada para estabilidade e outra mais atual para recursos mais recentes 🔄).
- Baixe o instalador adequado para o seu sistema operacional (Windows, macOS, Linux) e siga o processo de instalação ⚙️.

### 2. Verificar a instalação ✔️

Após a instalação, você pode verificar se o **Node.js** foi instalado corretamente através do terminal ou prompt de comando 🖥️:

```bash
node -v
```

Isso retornará a versão instalada do **Node.js** 🎉.

## 3. Instalar o npm 📦

O **npm (Node Package Manager)** é o gerenciador de pacotes que acompanha o **Node.js** e facilita a instalação de bibliotecas e dependências. O npm é automaticamente instalado com o **Node.js**, então você não precisa instalá-lo separadamente.

Para verificar a versão do npm, você pode usar:

```bash
npm -v
```

### 4. Usando o npm 🔧

O npm permite que você instale pacotes 📦, gerencie dependências de projetos e execute scripts de automação ⚙️. Para instalar pacotes, você pode usar o seguinte comando:

```bash
npm install <nome-do-pacote>
```

Com o **Node.js** e npm instalados, você já pode começar a desenvolver suas aplicações 💻, seja utilizando pacotes de terceiros ou criando suas próprias funcionalidades com **JavaScript** no back-end 🔧.
