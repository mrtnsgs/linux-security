
# Criando kv
$ vault kv put secret/giropops value=VAIIII

# Acessando kv
$ vault kv get secret/giropops

# Visualizando metadata do kv
$ vault kv metadata get secret/giropops

# Atualiando valor do kv
$ vault kv put secret/giropops value=FUIIII

# Acessando versão 2 do kv
$ vault kv get -version=2 secret/giropops

# Acessando o kv de uma versão especifica
$ vault kv get -version=2 -field=value secret/giropops

# Removendo versão especifica do secret
$ vault kv delete -versions=1 secret/giropops

# Voltando versão deletada do secret
$ vault kv undelete -versions=1 secret/giropops

# Destruindo versão do secret 
$ vault kv destroy -versions=1 secret/giropops

# Acessando um value especifico de um kv
$ vault kv get -field frase secret/opa

# Habilitando versão 1 do kv (kv = path)
$ vault secrets enable -version=1 kv

# Upgrade de versão do kv (kv = path)
$ vault kv -enable-versioning kv
$ vault secrets enable -version=2 kv

# Criando vários kvs ao mesmo tempo
$ vault kv put mrtnsgs/treinamentos/production_vault/plataforma
api_token='asdsqtweerteread' user='giropops'
admin_token='kjhjhwjerw3242kjwdfjklf' password='123mudar'
$ vault kv get mrtnsgs/treinamentos/production_vault/plataforma

# visualizando um value especifico
$ vault kv get -field=admin_token
mrtnsgs/treinamentos/production_vault/plataforma
