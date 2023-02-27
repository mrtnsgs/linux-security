## Enable ssh secret engine on vault
vault secrets enable ssh

## Download vault ssh helper 
wget https://releases.hashicorp.com/vault-ssh-helper/<version>

## In ec2 instance unzip and install vault-ssh-helper
unzip vault-ssh-helper_<version>_linux_amd64.zip
mv vault-ssh-helper /usr/local/bin/
vault-ssh-helper --help

## Set config on vault-ssh-helper
mkdir /etc/vault-ssh-helper.d
vi config.hcl

```bash
vault_addr = "http://192.168.0.54:8200" # internal ip of ec2 instance
tls_skip_verify = false
#ca_cert = ""
ssh_mount_point = "ssh"
#namespace = "" #only for vault enterprise
allowed_roles = "*" #specy roles in ssh secret engine
allowed_cidr_list = "18.185.58.200/32" # cidr external
```

# Config pam in ec2
cp /etc/pam.d/ssh{,-backup}
vi /etc/pam.d/ssh

```bash
auth requisite pam_exec_so quiet expose_authtok log=/var/log/vault-ssh.log
/usr/local/vault-ssh-helper -dev -config=/etc/vault-ssh-helper.d/config.hcl
auth optional pam_unix.so not_set_pass use_first_pass nodelay
```

# Config sshd service
cp /etc/ssh/sshd_config{,-backup}

```bash
ChallengeResponseAuthentication yes
UsePAM yes
PasswordAuthentication no
```

## test vault ssh helper
vault-ssh-helper -verify-only -dev -config /etc/vault-ssh-helper.d/config.hcl

## config in vault server
- Create the follow policy in ACL default

```bash
# To view in Web UI
path "sys/mounts" {
  capabilities [ "read", "update"] 
}

path "ssh/*" {
  capabilities [ "create", "read", "update", "delete", "list" ] 
}

path "sys/mounts/*" {
  capabilities [ "create", "read", "update", "delete" ] 
}
```

## Create aws role in vault
vault wirte ssh/roles/otp_key_role key_type=otp default_user=ubuntu
cidr_list=0.0.0.0/0 

## create acl policy to read, list and update role otp_key_role
vi otp_key_role_acl.hcl
```bash
path "ssh/creds/otp_key_role" {
  capabilities = ["create", "read", "update"]
}
```
vault policy write otp_ssh ./otp_key_role_acl.hcl

## enable userpass in vault
vault auth enable userpass

## create user
vault write auth/userpass/users/catota password="giropops" policies="otp_ssh"

## login with new user
vault login -method=userpass username=catota password=giropops
- this will return a vault token

## generate otp
vault write ssh ssh/creds/otp_key_role ip=192.168.0.24
- return password key to access

atention in configuration on ec2 instance network interface**

## Connect with ssh (need sshpass in client)
vault ssh --help
vault ssh -role otp_key_role -mode otp ubuntu@192.168.0.99
