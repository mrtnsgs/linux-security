
### DEFAULT POLICY

````bash
# Allow tokens to look up their own properties
path "auth/token/lookup-self" {
    capabilities = ["read"]
}

# Allow tokens to renew themselves
path "auth/token/renew-self" {
    capabilities = ["update"]
}

# Allow token to revoke themselves
path "auth/token/revoke-self" {
    capabilities = ["update"]
}
...

````

###

# Toda acl tem uma capabilitie para um path

# ACL POLICY example

```bash
path "mrtnsgs/data/treinamentos/production_vault/plataforma" {
  capabilities = [ "read" ]
}

path "mrtnsgs/treinamentos/production_vault/*" {
  capabilities = [ "read" ]
}

path "mrtnsgs/treinamentos/+/plataforma" {
  capabilities = [ "read" ]
}
```

# Adicionando policy a um auth (userpass)
$ vault write auth/production_users/jeferson2 password=giropops
policies=production_acl
$ vault read auth/production_users/jeferson2

# Criando policy
$ vault policy write giropops primeira-policy.hcl

# listando policies
$ vault policy list
