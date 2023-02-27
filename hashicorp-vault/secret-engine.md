
# secrets engine types
$ vault secrets (disable, enable, list, move, tune)

# habilitando novo secret engine
$ vault secrets enable aws

# habilitando um novo kv em outro path
$ vault secrets enable -path=production kv
$ vault kv list production

# desabilitando um secret engine
$ vault secrets disable aws

# movendo o secret engine de path
$ vault secrets move ssh/ production_ssh/

# informações sobre um path especifico
$ vault path-help production


