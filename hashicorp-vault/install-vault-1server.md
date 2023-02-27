
# Install vault from source

````bash
# Download vault bin
$ wget https://releases.hashicorp.com/vault/1.12.1/vault_1.12.1_linux_amd64.zip

# Unzip and move to correct path
$ unzip vault_1.12.1_linux_amd64.zip && mv vault /usr/local/bin

# Criando diretório para os logs do vault
$ mkdir /var/log/vault 

# Criando diretórios de dados
$ mkdir -p /var/lib/vault/data/

# Criando link simbólico para os logs
$ ln -s /var/log/vault/ /var/lib/vault/logs

# Criando diretório para a config do vault
$ mkdir /etc/vault

# Criando usuário de sistema para o vault
$ useradd -r vault
$ chown -Rv vault.vault /var/lib/vault
$ chown -Rv vault.vault /etc/vault/
$ chown -Rv vault.vault /var/log/vault/

# Criando arquivo e config
$ vi /etc/vault/config.json
storage "file" {
	path = "/var/lib/vault/data"
	
}

listener "tcp" {
	address = "0.0.0.0:8200"
	tls_disable = 1
}

# Criando arquivo de unidade para o systemd
$ vi /etc/systemd/system/vault.service
[Unit]
Description = Vault Server
Requires = network-online.target
After = network-online.target
ConditionFileNotEmpty = /etc/vault/config.json

[Service]
User = vault
Group = vault
Restart = on-failure
ExecStart = /usr/local/bin/vault server -config=/etc/vault/config.json
StandardOutput = /var/log/vault/output.log
StandardError = /var/log/vault/error.log
ExecReload = /bin/kill -HUP $MAINPID
KillSignal = SIGTERM
LimitMEMLOCK = infinity

[Install]
WantedBy = multi-user.target

# Exportando vault addr
$ export VAULT_ADDR="http://127.0.0.1:8200"

```
Unseal Key 1: A5ek/yHv460ACpIoRWv2SOm7uEaOdnt0NETlNRnPwyuc
Unseal Key 2: mSrQXvNxIq6Hwaqk++kWhBV+ZBWUIgyxCq3INiFerzgH
Unseal Key 3: FpOLvA6BhpKWsW4k5Ac5cOZZFdrdZbvGKmd4mfQc7kXZ
Unseal Key 4: iIyRp2gTwmK4Qhrkrf6F8iito1Mavz+xEjTCeXLNWYl4
Unseal Key 5: q7r77kNea/o/D7zELV8ZY61N2rOBRQoO0o9N1lrQ8G9J

Initial Root Token: hvs.fdRFkr7nKwGLJIridGQUabMN
