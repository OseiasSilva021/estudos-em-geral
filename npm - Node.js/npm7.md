
# 🚨 Erros do Sistema no Node.js 🚨

O Node.js gera erros de sistema quando exceções ocorrem dentro de seu ambiente de tempo de execução. Esses erros geralmente acontecem quando um aplicativo tenta acessar recursos do sistema ou fazer operações que violam as restrições do sistema operacional. Tais erros são comuns e devem ser tratados adequadamente para evitar falhas inesperadas em sua aplicação.

---

## ⚠️ Tipos Comuns de Erros do Sistema no Node.js

### 1️⃣ **EACCES - Permissão Negada**

Este erro ocorre quando o aplicativo tenta acessar um recurso sem permissões suficientes.

- **Exemplo**: Tentar escrever em um arquivo para o qual o processo não tem permissão.

```bash
Error: EACCES: permission denied, open '/caminho/para/arquivo'
```

### 2️⃣ **EADDRINUSE - Endereço Já em Uso**

Este erro é gerado quando você tenta ligar um servidor (geralmente HTTP ou TCP) a uma porta que já está em uso.

- **Exemplo**: Tentando executar um servidor em uma porta que já está ocupada por outro processo.

```bash
Error: listen EADDRINUSE: address already in use :::3000
```

### 3️⃣ **ECONNRESET - Redefinição de Conexão por Peer**

O erro `ECONNRESET` ocorre quando a outra parte de uma conexão TCP fecha a conexão de forma inesperada.

- **Exemplo**: A conexão foi fechada pelo cliente enquanto o servidor estava tentando enviar dados.

```bash
Error: ECONNRESET: connection reset by peer
```

### 4️⃣ **EEXIST - O Arquivo Existe**

Este erro ocorre quando você tenta criar um arquivo ou diretório, mas o arquivo ou diretório já existe.

- **Exemplo**: Tentando criar um arquivo ou diretório que já existe no sistema.

```bash
Error: EEXIST: file already exists, mkdir '/caminho/para/diretorio'
```

### 5️⃣ **EISDIR - É um Diretório**

Este erro ocorre quando você tenta executar uma operação de arquivo em um diretório.

- **Exemplo**: Tentando abrir um diretório como se fosse um arquivo.

```bash
Error: EISDIR: illegal operation on a directory, open '/caminho/para/diretorio'
```

### 6️⃣ **EMFILE - Muitos Arquivos Abertos no Sistema**

Esse erro acontece quando o processo atinge o limite de arquivos abertos no sistema operacional.

- **Exemplo**: O número de arquivos abertos simultaneamente excede o limite imposto pelo sistema.

```bash
Error: EMFILE: too many open files, open '/caminho/para/arquivo'
```

### 7️⃣ **ENOENT - Nenhum Arquivo ou Diretório Desse Tipo**

Este erro ocorre quando você tenta acessar um arquivo ou diretório que não existe.

- **Exemplo**: Tentando ler ou acessar um arquivo inexistente.

```bash
Error: ENOENT: no such file or directory, open '/caminho/para/arquivo'
```

### 8️⃣ **ENOTDIR - Não é um Diretório**

Esse erro ocorre quando uma operação espera um diretório, mas encontra um arquivo em seu lugar.

- **Exemplo**: Tentando acessar um arquivo como se fosse um diretório.

```bash
Error: ENOTDIR: not a directory, open '/caminho/para/arquivo'
```

### 9️⃣ **ENOTEMPTY - Diretório Não Vazio**

Este erro é gerado quando você tenta excluir um diretório que não está vazio.

- **Exemplo**: Tentando remover um diretório que ainda contém arquivos ou subdiretórios.

```bash
Error: ENOTEMPTY: directory not empty, rmdir '/caminho/para/diretorio'
```

### 🔟 **ENOTFOUND - Falha na Pesquisa de DNS**

O erro `ENOTFOUND` ocorre quando o DNS não consegue resolver um nome de domínio.

- **Exemplo**: Tentando acessar um endereço de URL ou servidor que não pode ser encontrado.

```bash
Error: ENOTFOUND: getaddrinfo ENOTFOUND exemplo.com
```

### 1️⃣1️⃣ **EPERM - Operação Não Permitida**

Este erro ocorre quando uma operação não é permitida pelo sistema operacional.

- **Exemplo**: Tentando excluir um arquivo ou diretório sem permissões suficientes.

```bash
Error: EPERM: operation not permitted, unlink '/caminho/para/arquivo'
```

### 1️⃣2️⃣ **EPIPE - Cano Quebrado**

O erro `EPIPE` acontece quando o processo tenta escrever em um pipe ou socket que foi fechado pela outra parte.

- **Exemplo**: Tentando escrever em um stream de saída que foi fechado.

```bash
Error: EPIPE: broken pipe
```

### 1️⃣3️⃣ **ETIMEDOUT - Tempo Limite da Operação Esgotado**

Este erro ocorre quando uma operação atinge o tempo limite.

- **Exemplo**: Uma solicitação de rede ou conexão de banco de dados leva mais tempo do que o limite configurado.

```bash
Error: ETIMEDOUT: timeout of 10000ms exceeded
```

---

## 🛠️ Como Lidar com Erros do Sistema?

### 1️⃣ **Usar Try-Catch para Capturar Erros**

Em Node.js, você pode capturar erros de sistema usando o bloco `try-catch`. Isso ajuda a evitar que o aplicativo trave quando um erro ocorre.

```javascript
try {
  // Tente realizar alguma operação que pode gerar erro
  fs.readFileSync('arquivo_inexistente.txt');
} catch (error) {
  console.error('Ocorreu um erro: ', error.message);
}
```

### 2️⃣ **Verificar Permissões e Existência de Arquivos**

Antes de realizar operações em arquivos ou diretórios, sempre verifique se eles existem e se o processo tem permissões adequadas.

```javascript
const fs = require('fs');

fs.access('/caminho/para/arquivo', fs.constants.F_OK | fs.constants.W_OK, (err) => {
  if (err) {
    console.error('Arquivo não existe ou sem permissões:', err);
  } else {
    console.log('Arquivo existe e tem permissões de leitura e escrita.');
  }
});
```

### 3️⃣ **Tratamento de Erros de Rede**

Ao realizar conexões de rede ou chamadas de API, sempre trate erros de rede, como `ECONNRESET`, `ETIMEDOUT` e `ENOTFOUND`.

```javascript
const http = require('http');

http.get('http://exemplo.com', (res) => {
  console.log('Resposta:', res.statusCode);
}).on('error', (err) => {
  console.error('Erro de rede:', err.message);
});
```

---

## 📝 Conclusão

Os erros de sistema no Node.js são comuns quando você interage com o sistema operacional, redes e arquivos. Com a abordagem correta para tratamento de erros e verificação de permissões e existência de arquivos, você pode criar aplicações mais robustas que lidam com falhas de maneira eficiente. 

⚠️ **Sempre trate erros de maneira adequada para garantir a estabilidade da sua aplicação!**  
