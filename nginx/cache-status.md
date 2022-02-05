# Verificando o status do cache utilizado

Para verificar o status do cache é necessário adicionar um cabeçalho http na configuração de location:
```
add_header X-Cache-Status $upstream_cache_status;
```

Retornos esperados:
expired: cache expirado
misse: não possui cache ainda
hit: cache salvo 

Limpeza do cache:
Presente na versão comercial do nginx, possibilita realizar a limpeza do cache de forma automática, através de um request.


