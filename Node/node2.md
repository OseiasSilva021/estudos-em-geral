# Fundamentos do **Node.js** 🚀

Este guia cobre os conceitos básicos do **Node.js**, incluindo módulos nativos, criação de servidores HTTP simples, manipulação de arquivos, execução assíncrona, eventos, e streams. 🌐

## 1. **Node.js** Básico 🖥️

O **Node.js** é uma plataforma baseada no motor V8 do Google Chrome que permite a execução de JavaScript no lado do servidor. Ele é popular devido à sua alta performance, escalabilidade e ao uso de JavaScript para desenvolvimento backend. ⚡

### Características principais:
- **Single-threaded**: O **Node.js** utiliza um único thread para processar múltiplas requisições, aproveitando a execução assíncrona e a não-bloqueante. 🧵
- **Event-driven**: O código no **Node.js** é altamente dependente de eventos. As operações de I/O não bloqueiam o fluxo de execução e podem ser tratadas com callbacks. 📡

## 2. Módulos Nativos 🧰

O **Node.js** vem com diversos módulos nativos para facilitar o desenvolvimento, como:

### **fs (File System)** 📂

O módulo `fs` é utilizado para manipulação de arquivos no sistema de arquivos. Ele permite a leitura, escrita e outras operações de manipulação de arquivos.

#### Exemplo de leitura de arquivo:
```javascript
const fs = require('fs');

// Ler um arquivo de forma assíncrona
fs.readFile('exemplo.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

### **http (Servidor)** 🌐

O módulo `http` permite criar servidores HTTP simples e manipular requisições e respostas. Ele é útil para construir servidores web e APIs RESTful.

#### Exemplo de servidor simples:
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Olá, mundo!');
});

server.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
```

### **path (Caminhos)** 🛤️

O módulo `path` ajuda a trabalhar com caminhos de arquivos e diretórios, sendo útil para manipulação de arquivos no sistema de arquivos.

#### Exemplo:
```javascript
const path = require('path');
const caminhoAbsoluto = path.join(__dirname, 'arquivo.txt');
console.log(caminhoAbsoluto);
```

### **os (Sistema Operacional)** 🖥️

O módulo `os` fornece informações sobre o sistema operacional, como memória, CPU, plataforma, etc.

#### Exemplo:
```javascript
const os = require('os');
console.log(`Plataforma: ${os.platform()}`);
console.log(`Memória livre: ${os.freemem()} bytes`);
```

## 3. Criando Servidores HTTP Simples 🌍

Com o módulo `http`, você pode criar servidores que respondem a requisições HTTP. Isso é fundamental para aplicações web e APIs.

#### Exemplo de servidor básico:
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify({ message: 'API funcionando!' }));
});

server.listen(5000, () => {
  console.log('Servidor HTTP rodando na porta 5000');
});
```

## 4. Trabalhando com o Sistema de Arquivos (fs) 📁

Além de ler e escrever arquivos, o módulo `fs` permite realizar outras operações no sistema de arquivos, como renomear arquivos e criar pastas.

#### Exemplo de escrita assíncrona:
```javascript
fs.writeFile('novo-arquivo.txt', 'Conteúdo do arquivo', (err) => {
  if (err) throw err;
  console.log('Arquivo criado!');
});
```

#### Exemplo de verificação de existência de arquivo:
```javascript
fs.exists('arquivo.txt', (exists) => {
  console.log(exists ? 'Arquivo existe!' : 'Arquivo não existe');
});
```

## 5. Execução Assíncrona e Callbacks ⏳

A execução assíncrona é um dos pilares do **Node.js**, permitindo que operações de I/O não bloqueiem o fluxo de execução.

### O que são **Callbacks**? 🔄

Um **callback** é uma função passada como argumento para outra função, e é executada quando a operação assíncrona termina.

#### Exemplo:
```javascript
function lerArquivo(caminho, callback) {
  fs.readFile(caminho, 'utf8', (err, data) => {
    if (err) return callback(err);
    callback(null, data);
  });
}

lerArquivo('exemplo.txt', (err, data) => {
  if (err) console.error(err);
  else console.log(data);
});
```

## 6. Eventos e Streams 📡

Eventos e streams são conceitos essenciais para a manipulação eficiente de dados em tempo real no **Node.js**.

### **EventEmitter** 🔔

A classe `EventEmitter` é usada para definir e escutar eventos personalizados no **Node.js**.

#### Exemplo de uso:
```javascript
const EventEmitter = require('events');
class MeuEmissor extends EventEmitter {}

const meuEmissor = new MeuEmissor();

// Ouvir o evento 'eventoTest'
meuEmissor.on('eventoTest', () => {
  console.log('O evento foi emitido!');
});

meuEmissor.emit('eventoTest');
```

### **Streams** 🎥

As **streams** são objetos que permitem o processamento de dados de maneira eficiente e assíncrona. Elas são essenciais para lidar com grandes volumes de dados, como ler e escrever arquivos.

- **Readable Streams**: Fluxos de dados que podem ser lidos (por exemplo, leitura de arquivos). 📖
- **Writable Streams**: Fluxos de dados que podem ser gravados (por exemplo, escrita em arquivos). ✍️
- **Duplex Streams**: Fluxos de dados que podem ser lidos e gravados ao mesmo tempo (por exemplo, conexões de rede). 🔄
- **Transform Streams**: Fluxos de dados que podem ser transformados enquanto são lidos ou gravados (por exemplo, compressão de dados). 🔧

#### Exemplo de **Readable Stream**:
```javascript
const fs = require('fs');
const readStream = fs.createReadStream('exemplo.txt', 'utf8');

readStream.on('data', (chunk) => {
  console.log('Novo pedaço de dados:', chunk);
});

readStream.on('end', () => {
  console.log('Leitura concluída!');
});
```

#### Exemplo de **Writable Stream**:
```javascript
const fs = require('fs');
const writeStream = fs.createWriteStream('saida.txt');

writeStream.write('Olá, mundo!\n');
writeStream.write('Escrevendo para o arquivo!');
writeStream.end();
```

## Conclusão 🎉

Esses fundamentos formam a base do uso do **Node.js** para construção de servidores web, manipulação de arquivos e criação de aplicativos assíncronos. Com o uso de módulos nativos, a execução assíncrona com callbacks, e eventos e streams, você pode criar sistemas rápidos e escaláveis. 🚀

---
Para mais detalhes, consulte a documentação oficial do **Node.js**: [https://nodejs.org/](https://nodejs.org/). 📚