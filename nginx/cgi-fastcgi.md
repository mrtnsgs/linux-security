#  CGI e FastCGI

### CGI - Common Gateway Interface

Permite que o servidor web execute um programa externo, geralmente enviado via requisição do usuário.
Cada requisição abre um processo cada requisição.

### FastCGI

O gerenciador de FastCGI executa uma função de enviar requisições para programas externas.
Somente um processo administra todas as requisições.

Linguagens interpretadas tem por padrão utilizar o FastCGI com gerenciadores de FastCGI nativos. Como por exemplo o PHP.
Utiizado para diminuir o uso de IO do servidor web.

Para configurar o nginx para utilizar o FastCGI no proxy, é necessário habilitar no location.
Estas configuração devem estar na configuração do nginx (nginx.conf) ou caso exista outro arquivo de configuração no diretório /etc/nginx/sites-enabled

```bash
server {
  listen 80;

  location / {
    fastcgi_pass localhost:9000;
  }
}
```

Neste caso são enviadas requisições FastCGI, que puramente não enviam dados das requisições http.
Para isso é necessário adicionar include para o arquivo de configuração do fastcgi.conf e também o document root onde estão os arquivos do web server ou do container docker:

```bash
server 
  listen 80;
  root /caminho/projeto;

  location / {
    include fastcgi.conf;
    fastcgi_pass localhost:9000;   
  }  
}
```
