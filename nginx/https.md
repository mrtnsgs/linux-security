# SSL - Secure Socker Layer

### Como funciona https?

Requisição e resposta http trafégam informações em texto puro, expondo dados para quem estiver analisando a rede.
O https existe para suprir a necessidade de privacidade no envio e recebimento de dados.

Como funciona o https?
O cliente conexão com o servidor e o servidor retorna um certificado, emitido por uma entidade certificadora, que emitem certificados tanto gratuitos quanto pagos. Garantindo a autenticidade do servidor.
A partir deste certificado (chave pública) o navegador gera uma chave assimétrica que ira realizar a criptografia do conteúdo e enviará o request ao servidor. Ao receber o request com as informações criptografadas o servidor, que possui a chave privada (compatível com a chave púbica enviada inicialmente), conseguirá descriptografar as informações.
Quem estiver analisando a rede notará que as informações contidas na requisição estão criptografadas, impossibilitando a exposição das informações.


