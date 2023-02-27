
# opcoes
$ vault auth (disable, enable, help, list, tune)

# listando métodos de auth
$ vault auth list

# habilitando um novo método de auth
$ vault auth enable (app.id, approle, aws, gcp, cert, github, ldap, okta,
plugin, radius, userpass)

# escrevendo um user e pass
$ vault write auth/production_users/users/jeferson password=giropops

# info sobre o userpass criado
$ vault read auth/production_users/users/jeferson

# login com usuário
$ vault login -method=userpass -path=production_users username=jeferson password=giropops

# logando com token
$ vault login token='xxxxxxxxxxxx'

# desabilitando metodo de auth
$ vault auth disable production_users


