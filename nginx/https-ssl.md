# Gerando certificados SSL


```bash
# Gerando um certificado com:
# -days: 1024 dias de válidade 
# auto assinado: -x509
# não precisa criptografar a chave: -nodes
# -newkey: nova chave com criptografia rsa de 2048 bits
# -keyout: saída da chave privada
# -out: certificado gerado
$ openssl req -x509 -nodes -days 1024 -newkey rsa:2048 -keyout localhost.key -out localhost.crt
```


Para que o certificado seja reconhecido em distribuições linux é utilizado o certutil:
```bash
$ certutil -d sql:$HOME/.pki/nssdb -A -t "P,," -n "meu certificado" -i /caminho/para/arquivo/certificado.crt
```
Necessário reiniciar o navegador para que seja lida novamente a base de dados, com os novos dados referênte ao certificado auto-assinado.

### Adicionando SSL na configuração do NGINX

```bash
server {
  listen 443;
  root /var/www/html;
  index index.html;
  gzip on;
  gzip_types text/css;
  add_header Keep-Alive ""timeout=5, max=1000;
  ssl_certicate /tmp/localhost.crt;
  ssl_key /tmp/localhost.key;
   
  location ~ \.jpg$ {
    expires 30d;
    add_header Cache-Control public;
  }
}
server {
  ...
}
```
