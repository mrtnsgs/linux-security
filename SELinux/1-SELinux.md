# Security-Enhanced Linux - SELinux

É um modulo de segurança do kernel linux que provém um mecanismo para suporte à políticas de controle de acesso, incluíndo controles de acesso mandatórios.
É um conjunto user-space tools e a modificiações no kernel linux e esta em diversas distribuições linux.

SELinux implementa o Mandatory Access Control (MAC) sobre o Discretionary Access Control (DAC) que esta presente em todas as distribuições linux.
Confina um processo a determinados outros processos, binários ou diretórios.

Instalação do SELinux:
```bash
# Debian based
$ sudo apt install policycoreutils selinux-utils selinux-basics
# RedHat based
$ sudo yum install selinux
```

### Pacotes a mais utilizados no CentOS

policycoreutils: Fornece utilitários para gerenciar o selinux
policycoreutils-python: Fornece utilitários para gerenciar o selinux no python
selinux-policy: politica de referencia do selinux
selinux-policy-targeted: diretiva segmentada do selinux
libselinux-utils: ferramentas gerencar selinux
setroubleshoot-server: // decrifrar log auditoria
setools: ferramentas monitorar log de auditoria
setools-console: ferramenta de log de auditoria
mcstrans traduzir diferentes níves para formatos facil de entender.

### Arquivo de configuração do SELinux

Arquivo de configuração do SELinux: /etc/selinux/config

SELINUX=
Seta o modo do selinux.

Valores:
Enforce: Reforça a sua política no sistema linux. Garante que todas as tentivas de acesso não permitidas são negadas.
Permissive: Não aplica sua politíca, nenhum acesso é negado, somente registra nos logs de auditoria violações.
Disable: SELinux desabilitado.

SELINUXTYPE=
Seta a política do selinux.

Valores:
targeted: O processo é protegido
minimium: Somente protegera processos selecionados.
mls: Multi Level Security Protection. Modo avançado, permite customizações.

*Após editar o arquivo de configuração é necessário reiniciar o servidor/computador.

Comandos de modos:
```bash
# Exibe o modo do selinux
$ sudo getenforce

# Exibe o status do selinux
$ sudo sestatus

# Habilitar selinux via linha de comando: (ou pode ser editado diretamente no arquivo de configuração do selinux na diretiva SELINUX=)
$ sudo setenforce 

#
$ 
```

...
work in progress...
