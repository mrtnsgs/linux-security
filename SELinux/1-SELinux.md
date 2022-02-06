# Security-Enhanced Linux - SELinux

<p>
É um modulo de segurança do kernel linux que provém um mecanismo para suporte à políticas de controle de acesso, incluíndo controles de acesso mandatórios.<br />
É um conjunto user-space tools e a modificiações no kernel linux e esta em diversas distribuições linux.

SELinux implementa o Mandatory Access Control (MAC) sobre o Discretionary Access Control (DAC) que esta presente em todas as distribuições linux.<br />
Confina um processo a determinados outros processos, binários ou diretórios.
</p>

Instalação do SELinux:
```bash
# Debian based
$ sudo apt install policycoreutils selinux-utils selinux-basics
# RedHat based
$ sudo yum install selinux
```

### Pacotes a mais utilizados no CentOS

<p>
policycoreutils: Fornece utilitários para gerenciar o selinux <br />
policycoreutils-python: Fornece utilitários para gerenciar o selinux no python <br />
selinux-policy: politica de referencia do selinux <br />
selinux-policy-targeted: diretiva segmentada do selinux <br />
libselinux-utils: ferramentas gerencar selinux <br />
setroubleshoot-server: // decrifrar log auditoria <br />
setools: ferramentas monitorar log de auditoria <br />
setools-console: ferramenta de log de auditoria <br />
mcstrans traduzir diferentes níves para formatos facil de entender.
</p>

### Arquivo de configuração do SELinux

Arquivo de configuração do SELinux: /etc/selinux/config

<p>
SELINUX=<br />
Seta o modo do selinux.

Valores:
Enforce: Reforça a sua política no sistema linux. Garante que todas as tentivas de acesso não permitidas são negadas. <br />
Permissive: Não aplica sua politíca, nenhum acesso é negado, somente registra nos logs de auditoria violações. <br />
Disable: SELinux desabilitado.

SELINUXTYPE=<br />
Seta a política do selinux.

Valores: <br />
targeted: O processo é protegido <br />
minimium: Somente protegera processos selecionados. <br />
mls: Multi Level Security Protection. Modo avançado, permite customizações.
</p>
*Após editar o arquivo de configuração é necessário reiniciar o servidor/computador.

Comandos de modos:
```bash
# Exibe o modo do selinux
$ sudo getenforce

# Exibe o status do selinux
$ sudo sestatus

# Habilitar selinux via linha de comando: (ou pode ser editado diretamente no arquivo de configuração do selinux na diretiva SELINUX=)
$ sudo setenforce enforce
```

Os logs sao escritos no /var/log/messages ou /var/log/syslog, no ubuntu.

### Politica

<p>
Define o acesso do usuário as funções e acesso a funções ao domínio e acesso do domíno a tipos. <br />
O SELinux possuí usuários ativos e toda conta do linux é mapeada para um ou mais usuário do SELinux. <br />
Um processo é chamado de subject no mundo do SELinux. <br />
Uma role realiza um gateway entre usuários e processos, definindo o que cada usuário pode acessar. <br />
Uma função na política do SELinux define quais usuários tem acesso a esta função tem RBAC's que controlam o acesso a subjects. <br />
Um subject é um processo e pode afetar um object. <br />
O domínio define quais os links, dispositivos e portas que estão disponíveis para um object. <br />
O contexto de um arquivo é chamado de type.
</p>

Por fim, a política do selinux define acesso do usuário a funções, acesso das funções aos domínios e o acesso dos domínios aos tipos.
user -> role -> domain -> file

<p>
As regras do SELinux não bloqueiam/liberam restrições do DAC, pois entram em ação após. <br />
Caso o DAC permita o acesso, as regras do SELinux podem bloquear, se assim estiverem configuradas
</p>

### Módulos

<p>
Os módulos são ativos na inicilização do sistema. <br />
Diretório de módulos do SELinux: /etc/selinux/targeted/active/modules
</p>

```bash
# Listando módulos do SELinux
$ sudo semodules -l

# Listando módulos e seus valores (Allow, on, off)
$ sudo semanage boolean -l

# Listando o valor booleano do módulo
$ sudo getsebool ftp_anon_write

# Ativando o módulo temporariamente
$ sudo setsebool ftp_anon_write on

# Ativando o módulo permanentemente
$ sudo setsebool ftp_anon_write on -P
```
