# Nginx

É um servidor web e proxy reverso. Trabalha em layer 4 load balancing/proxy, ou seja, é baseado na camada 4 da camada OSI. Significa que só consegue realizar o proxy através de ip e porta que recebeu a requisição.

Possui um processo master, sendo possível setar o número de worker_process 

### Balanceamento de carga

Algoritmo Round robin define um espaço de tempo onde o processo executa e é interrompdio  para execução de um próximo processo, assim sucessivamente até o último processo. Encerrando a execução dos processos é feito o retorno para o processo inicial, que executa novamente e inicia a cadeia de processos.
Este algoritmo é padrão no load balancing do nginx.

Weight Round Robin, seleciona o processo de acordo com o seu peso e executa sequêncialmente.

- Least Connection
Verifica qual dos servidores tem menos conexões ativas e manda requisições para lá, levando em conta o weight de cada servidor.
least_conn;

- ip_hash;
envia as requisições de acordo com o endereço ip configurado.

- hash;
envia requisições de acordo com uma chave configurada, que pode ser uma string de texto, variável

- randon
Seleciona randomicamente para onde enviar a requisição
randon two least_time=las-byt

## Servidores de Backup

Caso o servidor principal caia outro de backup assume.
``` bash
upstream servicos{
  server localhost:8001;
  server localhost:8002 backup;
}

server {
  listen 8003;
  server_name localhost;

  location / {
    proxy_pass http://servicos;
    proxy_set_header X-Real-IP $remote_addr;
 }
}
```

## Peso (weight)

Escolhe o servidor de acordo com o peso dele, quanto maior o valor maior a prioridade, setado através da diretiva weight:
```bash
upstream servicos{
  server localhost:8001 weight=2;
  server localhost:8001 weight=1;
}

server {
  listen 8003;
  server_name localhost;

  location / {
    proxy_pass http://servicos;
    proxy_set_header X-Real-IP $remote_addr;
  }
}
```

