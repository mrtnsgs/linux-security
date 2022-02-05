# Servidor de Cache com Nginx

O cache é salvo no servidor onde se encontra o nginx.
O caso abaixa utiliza o cache junto ao FastCGI

```bash
fastcgi_cache_path /tmp/cache levels=1:2 keys_zone=fpm:10m;
# proxy_cache_path /tmp/cache levels=1:2 keys_zone=proxy:1m;  # Utilizado para guardar o cache para proxy_pass

server {
  listen 80;
  root /caminho/projeto;

  location / {
    fastcgi_pass localhost:9000;
    include fastcgi.conf;
    fastcgi_cache fpm;
    fastcgi_cache_key $request_method$request_uri;
    fastcgi_cache_valid 200 301 302 10m;
  }
}
```
fastcgi_pass: qual porta esta rodando o web server da aplicação.
include fastcgi.conf: incluí o arquivo de configuração do FastCGI
fastcgi_cache: o tipo de cache.
fastcgi_cache_key: as chaves que serão utilizadas no cahce.
fastcgi_cache_valid: tipos de requisições que serão cacheadas, o recomendado pela documentação do nginx são: 200, 301 e 302. Usar any para habilitar todas.
