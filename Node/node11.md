

# 🚀 Deploy e Performance em Node.js

Este guia aborda as melhores práticas para realizar o **deploy** de aplicações Node.js em produção, além de estratégias de **monitoramento** e **otimização de performance**.

# 🔍 Ferramentas para Monitoramento

## ⚡ pm2
**pm2** é um gerenciador de processos que facilita a execução de aplicações Node.js em produção. Ele ajuda a manter a aplicação em execução, mesmo após falhas ou reinicializações.

#### Funcionalidades:
- 🛠️ **Gerenciamento de processos**: Inicie, pare, reinicie ou monitore seus processos.
- ⚙️ **Clustering**: Execute múltiplas instâncias da sua aplicação para melhor utilização da CPU.
- 📜 **Logs**: Centralize os logs da aplicação.
- 🔄 **Watch mode**: Monitoramento de alterações no código.

#### Comandos básicos:
```bash
# Iniciar a aplicação
pm2 start app.js

# Monitorar a aplicação
pm2 monit

# Visualizar logs
pm2 logs
```

### 📊 New Relic ou Datadog
**New Relic** e **Datadog** são ferramentas de monitoramento e análise de performance, que permitem visualizar métricas detalhadas sobre o desempenho da aplicação.

- 📈 **New Relic**: Fornece insights sobre transações, tempo de resposta e chamadas de banco de dados.
- 📉 **Datadog**: Oferece monitoramento de métricas em tempo real e rastreamento de requisições distribuídas.

## 🌐 Deploy de Aplicações Node.js

### 🚀 Heroku
**Heroku** é uma plataforma como serviço (PaaS) que permite o deploy fácil e rápido de aplicações Node.js.

#### Passos básicos:
1. 📝 Crie uma conta no [Heroku](https://www.heroku.com/).
2. 💻 Instale o [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli).
3. 🔑 No terminal, inicialize um repositório Git e faça login no Heroku:
   ```bash
   heroku login
   ```
4. ✨ Crie um app no Heroku:
   ```bash
   heroku create
   ```
5. 🔄 Suba o código para o Heroku com Git:
   ```bash
   git push heroku master
   ```
6. ⚙️ Configure variáveis de ambiente:
   ```bash
   heroku config:set NOME_VARIAVEL=valor
   ```
7. 🌍 Acesse a aplicação:
   ```bash
   heroku open
   ```

### ☁️ DigitalOcean
**DigitalOcean** oferece servidores virtuais (droplets) onde você pode configurar sua aplicação de forma personalizada.

#### Passos básicos:
1. 📝 Crie uma conta no [DigitalOcean](https://www.digitalocean.com/).
2. 💻 Crie um droplet com uma imagem de Node.js ou uma distribuição Linux básica.
3. 🔑 Configure o ambiente com SSH para acessar o droplet.
4. 🚀 Instale o Node.js e suba sua aplicação via Git ou FTP.
5. 🌐 Configure o servidor web (Nginx ou Apache) para servir a aplicação.

### 🌩️ AWS (Amazon Web Services)
A **AWS** oferece diversos serviços para deploy de aplicações, como **Elastic Beanstalk** e **EC2**.

#### Passos básicos:
1. 📝 Crie uma conta na [AWS](https://aws.amazon.com/).
2. ⚙️ Crie um ambiente no Elastic Beanstalk para Node.js.
3. 🚀 Faça o upload do código para a AWS.
4. 🌐 A AWS gerencia a infraestrutura e o deploy para você.

## 🛠️ Configurando Variáveis de Ambiente

Variáveis de ambiente são usadas para armazenar informações sensíveis e configurar comportamentos da aplicação.

- 🔐 No Node.js, acesse variáveis de ambiente com `process.env.VARIABLE_NAME`.
- 🔧 Defina variáveis de ambiente localmente no terminal:
  ```bash
  export DATABASE_URL="mysql://user:password@host:port/database"
  ```
- 🌍 Em plataformas como Heroku e AWS, configure variáveis diretamente no painel de controle ou via CLI.

## 🚀 Otimização de Performance

### 🔄 Event Loop e Ciclo de Vida de uma Requisição

O **event loop** do Node.js permite que a aplicação manipule múltiplas requisições simultaneamente, sem bloquear a execução. O ciclo de vida de uma requisição é o seguinte:
1. 📥 A requisição chega e é colocada na fila do event loop.
2. 🔄 O Node.js processa a requisição e executa operações assíncronas, como chamadas de banco de dados.
3. 📤 Quando a operação é concluída, a resposta é enviada ao cliente.

### 💾 Caching

**Caching** é uma técnica fundamental para melhorar o desempenho, reduzindo o tempo de resposta e a carga no banco de dados.

- 🧑‍💻 **Redis** é uma ferramenta popular para caching em Node.js, armazenando dados na memória para acesso rápido.

#### Exemplo básico usando Redis:
```js
const redis = require('redis');
const client = redis.createClient();
client.set('key', 'value', redis.print);
```

### ⚖️ Balanceamento de Carga (Load Balancing)

O balanceamento de carga distribui o tráfego entre múltiplas instâncias da aplicação para evitar que uma única instância fique sobrecarregada.

- 🔧 Em Node.js, use o **pm2** para criar clusters e distribuir o tráfego entre várias instâncias.
  
#### Exemplo de clustering com pm2:
```bash
pm2 start app.js -i max  # 'max' usa o número de CPUs disponíveis
```

## ✅ Conclusão

Realizar o **deploy** e garantir a **performance** em produção é fundamental para qualquer aplicação Node.js. Utilizando ferramentas como **pm2**, **New Relic**, **Datadog**, e plataformas como **Heroku**, **DigitalOcean** e **AWS**, você pode garantir que sua aplicação esteja funcionando de forma eficiente, escalável e estável, mesmo sob alta carga. 💪🚀