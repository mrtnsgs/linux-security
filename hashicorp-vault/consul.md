# Install consul

```bash
# Criar o diretório de dados do consul
$ mkdir /var/lib/consul

# Criar o diretório de config
$ mkdir /etc/consul

# Adicionar usuário do consul
$ useradd -r consul

# Ajustar permissões nos respectivos diretórios
$ chown -v consul. /etc/consul
$ chown -v consul. /var/lib/consul

# Download binário
$ wget https://releases.hashicorp.com/consul/1.14.1/consul_1.14.1_linux_amd64.zip

# unzip and move bin
$ unzip consul_1.14.1_linux_amd64.zip && mv consul /usr/local/bin/

```

# Criando arquivo de config do consul

Criar o arquivo de configuração config.json em cada node do cluster ajustando conforme
informações de cada um:

```bash
{
  "server": true,
  "node_name": "ubuntu-server-1",
  "datacenter": "dc1",
  "data_dir": "/var/lib/consul/data",
  "bind_addr": "0.0.0.0",
  "client_addr": "0.0.0.0",
  "advertise_addr": "192.168.0.51",
  "bootstrap_expect": 3,
  "retry_join": ["192.168.0.51", "192.168.0.52", "192.168.0.53"],
  "ui": true,
  "log_level": "DEBUG",
  "enable_syslog": true,
  "acl_enforce_version_8": false
}
```

# Confirmar usuário dono e grupo do arquivo de configuração

```bash
$ chown -Rv consul. /etc/consul

# Start no service
$ systemctl start consul.service 
```

# Consul commands

```bash
# Exibindo os membros do cluster
$ consul members

# Listing peers
$ consul operator raft list-peers
```
