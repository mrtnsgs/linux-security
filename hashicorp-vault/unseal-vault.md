
# Exportando vault addr
$ echo "export VAULT_ADDR='http://127.0.0.1:8200' >> /root/.bashrc

# Iniciando o vault
$ vault operator init

```bash
Unseal Key 1: CMPUn21xiChusAwovJZtaz8YExOxeZxbUIDdfRoKD9DM
Unseal Key 2: r60XPnGYA50e5cqJJX8eIVKwS4+DdznO/x14Q8g7kVqw
Unseal Key 3: EihNU5zKwdTm69jjmAbdkeJKdmNLxhOLScDxYnN4LqMo
Unseal Key 4: NV6psdffllJ+tI1exKLbVbQvdeHXcM65BPvGuBHv6l0L
Unseal Key 5: d4DQBRdihEJ+pVi2cdT2YP82QUgp9s75eA6xKQdWyb4W

Initial Root Token: hvs.tnxYjSvKZtN4BVNsVYZjt6Fj
```

# Unseal do vault com as chaves geradas
$ vault operator unseal

# Exportar o token root para acesso a api
$ export VAULT_TOKEN=hvs.tnxYjSvKZtN4BVNsVYZjt6Fj

# Criando secret do tipo kv na versão 2
$ vault secrets enable -version=2 -path giropops kv

# Habilitando user interface
$ echo "ui = true" >> /etc/vault/config.json

# Outras possíveis configs
api_addr = "http://0.0.0.0:8200"
cluster_name = "giropops"
disable_mlock = true
disable_cache = true
max_lease_ttl = "12h"
default_lease_ttl = "6h"
pid_file = "/var/lib/vault/vault.pid"


