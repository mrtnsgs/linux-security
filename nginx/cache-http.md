# Cache HTTP

Configura o cache dos navegadores de acordo com regras criadas.

Como a regra abaixo, que cria um cache de 30 dias para arquivos .jpg
```
server {
  listen 80;
  root /var/www/html
  index index.html

  location ~ \.jpg$ {
    expire 30d;
    add_header Cache-Control public;
  }

}
```
add_header Cache-Control public: permite que outros intermediários criem cache, como proxy, load balancer, etc.

Ao verificar o header será possível verificar dois cabeçalhos relacionados ao cache:

*Cache-Control: max-age=2592000
*Expires: Mon, 7 Feb 2022 18:38 GMT
