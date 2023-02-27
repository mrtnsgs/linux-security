# Approle
Approle similar ao userpass utiliza uma espécia de usuário e senha, nesse caso
RoleID SecretID. Que é uma forma do servidor autenticar e buscar os secrets
desejados.

# Personas
 - admin: com privilégios e permissões para gerenciar os auth methods.
 - app: consumidor dos secrets armazenados no vault.

Desde que cada approle tenha uma policy anexada, é possível escrever politicas
especificando o path que cada aplicação terá acesso.

```bash
# Criar a policy de read only ao path do secret
$ cat jenkins.hcl 
Read-only permission on 'secret/data/myapp/*' path
path "secret/data/myapp/*" {
  capabilities = [ "read" ]
}

# Aplicar a nova policy
$ vault-server:~# vault policy write jenkins jenkins.hcl
Success! Uploaded policy: jenkins

# Criar o secret com seu conteúdo
$ vault kv put secret/myapp/db-config @data.json
$ vault-server:~# cat data.json 
{
  "url": "foo.example.com:35533",
  "db_name": "users",
  "username": "admin",
  "password": "passw0rd"
}

# Habilitar o método de autenticação approle (caso não esteja habilitado)
$ vault auth enable approle
Success! Enabled approle auth method at: approle/

# Criar o novo path de auth approle com a policy criado anteriormente
$ vault write auth/approle/role/jenkins token_policies="jenkins" \
       token_ttl=1h token_max_ttl=4h
Success! Data written to: auth/approle/role/jenkins
```


# Role ID and Secret ID
The Role ID and Secret ID are like a username and password that a machine or app uses to authenticate.

```bash
# Buscando o role_id do novo path criado
$ vault read -format=json auth/approle/role/jenkins/role-id \
       | jq -r ".data.role_id" > role_id.txt

# Buscando o role_id do novo path criado
$ vault read -format=json auth/approle/role/jenkins/role-id \

# Buscando o role_id do novo path criado
$ vault read auth/approle/role/jenkins/role-id

# Buscando o secret-id
$ vault write -f -format=json auth/approle/role/jenkins/secret-id \
       | jq -r ".data.secret_id" > secret_id.txt

$ vault-server:~# cat secret_id.txt 
277235d8-2487-6bc6-df29-4015fd0dcdbb

# Gerando token de acesso com o secret_id e role_id
$ vault write -format=json auth/approle/login \
       role_id=$(cat role_id.txt) secret_id=$(cat secret_id.txt) \
       | jq -r ".auth.client_token" > app_token.txt

# Vendo informações sobre o token gerado
$ vault token lookup $(cat app_token.txt)

```
