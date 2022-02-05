# Performance na conexão

É possível aumentar o número de workder do processo master do nginx.
Recomenda-se utilizar um worker para cada cpu presente no servidor.

Alterar para auto no nginx.conf faz com que o nginx crie o número de workers de acordo com o número de cpus:
```bash
worker_processes auto;
```

### Keepalive

Habilita um tempo de espera para enviar novas requisições, enquanto o keepalive estiver garantindo a conexão aberta todas as requisições são enviadas na mesma.
Habilitado através da diretiva add_header Keep-Alive:
```bash
server {
  server 80;
  root /var/www/html;
  index index.html;
  gzip on;
  gzip_types text/css;
  add_header Keep-Alive "timeout=5, max=1000"

  location ~ \.jpg$ {
    expires 30d;
    add_header Cache-Control public;
  }

}
```
