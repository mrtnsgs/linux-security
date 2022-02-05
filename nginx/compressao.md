# Compressão e compactação

Visa diminuir o tamanho dos arquivos transferem ao cliente.
Através de um módulo do nginx é ativado pela diretiva gzip:

```bash
server{
  listen 80;
  root /var/www/html;
  index index.html;
  gzip on;
  gzip_types image/jpg text/css;

  location ~\..jpg$ {
    expires 30d;
    add_header Cache-Control public;
  }
}
```
gzip_types: Especifica quais arquivos serão compactados.
