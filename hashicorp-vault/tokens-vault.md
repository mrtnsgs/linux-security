
### Gerando um novo token root

# Gerando números de key shares e key threshold
$ vault operator init \
  -key-shares=3 \
  -key-thresholds=2

# Gerando um novo token root (necessário threshold keys)
$ vault operator generate-root -init 

# Serão gerados valores como Nonce e OTP, que serão utilizados nos próximos
# passos
# Usando as chaves iniciais para gerar um novo token root (necessário 3) 
$ vault operator generate-root -nonce xxxxx.xxxx.xxx.xxxx.xxxxxx
uma-das-thresholds-keys

# No resultado do comando anterior será gerado um Encoded token, necessário
# para o próximo comando
$ vault operator generate-root -decode <encoded-token> -otp
<otp-gerad-no-primeiro-passo>

### Rekey process

# Gerando novas key shares e thresholds keys
$ vault operator rekey -init -key-shares 5 -key-threshold 3

# Salvar o output (Nonce) para os próximos passos
# Usar o nonce no seguinte comando, que pedira uma das keys iniciais
$ vault operator rekey -nonce <xxxxxx-xxx-xxxx-xxx>

