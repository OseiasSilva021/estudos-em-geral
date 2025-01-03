# Introdução ao Nginx
O **Nginx** é um servidor web poderoso e eficiente, amplamente utilizado para diversas funções, como:
1. **Servidor Web** - Servir arquivos estáticos (HTML, CSS, JavaScript, imagens, etc.).
2. **Proxy Reverso** - Encaminhar solicitações para servidores de backend, como Node.js, PHP, ou outros.
3. **Balanceador de Carga** - Distribuir tráfego entre vários servidores para garantir alta disponibilidade e escalabilidade.
4. **Cache** - Melhorar o desempenho armazenando respostas em cache.
5. **Gerenciador de TLS/SSL** - Proteger conexões HTTPS.

Nginx é conhecido por seu desempenho, modularidade e capacidade de lidar com alta concorrência, tornando-o ideal para projetos pequenos ou de grande escala.

---

### Instalação do Nginx

#### No Ubuntu/Debian:
```bash
sudo apt update
sudo apt install nginx
```

#### No CentOS/RHEL:
```bash
sudo yum install epel-release
sudo yum install nginx
```

Após a instalação, inicie o serviço:
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

### Estrutura do Arquivo de Configuração
O arquivo principal de configuração geralmente está localizado em:
- **Debian/Ubuntu:** `/etc/nginx/nginx.conf`
- **CentOS:** `/etc/nginx/nginx.conf`

A configuração básica do Nginx usa "blocos de servidor" definidos com a diretiva `server`. Estes blocos são usados para configurar hosts virtuais.

---

### Exemplos Práticos de Configuração

#### 1. **Servidor Web Simples**
Servindo arquivos estáticos de um diretório local:
```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- **`listen 80`**: Porta HTTP padrão.
- **`server_name`**: Nome do domínio.
- **`root`**: Diretório raiz dos arquivos do site.
- **`try_files`**: Verifica se o arquivo ou diretório existe, caso contrário retorna erro 404.

#### 2. **Proxy Reverso**
Encaminhando solicitações para um servidor Node.js rodando em `localhost:3000`:
```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
- **`proxy_pass`**: Define o endereço do backend.
- **`proxy_set_header`**: Passa cabeçalhos adicionais para o backend.

#### 3. **Balanceador de Carga**
Distribuindo o tráfego entre dois servidores backend:
```nginx
upstream backend_servers {
    server backend1.example.com;
    server backend2.example.com;
}

server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://backend_servers;
    }
}
```

- **`upstream`**: Define um grupo de servidores.
- **`proxy_pass`**: Redireciona as solicitações para o grupo.

#### 4. **Habilitando HTTPS**
Usando certificados TLS/SSL para proteger conexões:
```nginx
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /etc/nginx/ssl/example.com.crt;
    ssl_certificate_key /etc/nginx/ssl/example.com.key;

    location / {
        root /var/www/html;
        index index.html;
    }
}
```

- **`ssl_certificate`** e **`ssl_certificate_key`**: Apontam para os arquivos de certificado e chave privada.
- Para obter um certificado gratuito, você pode usar o Let's Encrypt:
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d example.com -d www.example.com
```

#### 5. **Configuração de Cache**
Habilitando o cache para conteúdo estático:
```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        root /var/www/html;
        index index.html;

        # Cache para 30 dias
        expires 30d;
        add_header Cache-Control "public";
    }
}
```

- **`expires`**: Define o tempo de cache para os navegadores.
- **`add_header`**: Adiciona cabeçalhos HTTP personalizados.

#### 6. **Restrições de IP**
Bloqueando acesso de um IP específico:
```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        deny 192.168.1.1;
        allow all;
    }
}
```

---

### Comandos Úteis

- **Testar a configuração:**
```bash
sudo nginx -t
```

- **Recarregar o Nginx após alterações:**
```bash
sudo systemctl reload nginx
```

- **Verificar status do Nginx:**
```bash
sudo systemctl status nginx
```

---

### Boas Práticas
1. **Manter backups** do arquivo de configuração antes de alterações.
2. **Testar configurações** com `nginx -t` para evitar erros.
3. Utilizar **certificados SSL** para garantir segurança.
4. Ativar **logs de acesso e erro** para monitorar o servidor:
   ```nginx
   access_log /var/log/nginx/access.log;
   error_log /var/log/nginx/error.log;
   ```
5. Limitar solicitações abusivas com **rate limiting**:
   ```nginx
   limit_req_zone $binary_remote_addr zone=mylimit:10m rate=1r/s;

   server {
       location / {
           limit_req zone=mylimit;
       }
   }
   ```

Se precisar de exemplos mais avançados ou resolver problemas específicos, é só pedir!
