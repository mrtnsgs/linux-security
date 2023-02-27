# Conectando vault cluster com o consul

- /etc/vault/config.json

```bash

# Como boa prática o vault não se conecta direto ao cluster consul
# A conexão abaixo é com o consul cli, este sim se conecta ao cluster consul
storage "consul" {
	address = "127.0.0.1:8500"
	path = "vault/"
}

listener "tcp" {
	address = "0.0.0.0:8200"
	cluster_address = "192.168.0.51:8201"
	tls_disable = 1
}

ui = true
api_addr = "http://0.0.0.0:8200"
cluster_addr = "http://192.168.0.51:8201"
cluster_name = "giropops"
disable_mlock = true
disable_cache = true
max_lease_ttl = "12h"
default_lease_ttl = "6h"
pid_file = "/var/lib/vault/vault.pid"
```

# Configurar consul cli

Nos mesmos nodes do vault
- /etc/consul/consul.json

```bash
{
  "server": false,
  "node_name": "vault-server-1",
  "datacenter": "dc1",
  "data_dir": "/var/lib/consul/data",
  "bind_addr": "192.168.0.51",
  "client_addr": "127.0.0.1",
  "retry_join": ["192.168.0.51", "192.168.0.52", "192.168.0.53"],
  "ui": true,
  "log_level": "DEBUG",
  "enable_syslog": true,
  "acl_enforce_version_8": false
}
```
 - Criar arquivo de unit com o mesmo conteúdo do consul server, ajustando
   somente o hostname
