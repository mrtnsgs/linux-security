### Perguntas e respostas

- Você trabalha como administrador de rede da Secure World Inc. A empresa tem uma rede baseada em Linux. Você quer executar um comando com o diretório raiz alterado. Qual dos seguintes comandos você usará?
Sua resposta está correta.
A resposta correta é:
chroot &lt;new root&gt; &lt;command&gt;


- Qual das seguintes afirmações é verdadeira sobre ambientes chroot?
a. Links físicos para arquivos fora do caminho chroot não são seguidos, para aumentar a segurança
b. O caminho chroot precisa conter todos os dados requeridos pelos programas em execução no ambiente chroot
c. Os programas não são capazes de definir um caminho chroot usando uma chamada de função, eles têm que usar o comando chroot
d. Links simbólicos para dados fora do caminho chroot são seguidos, tornando arquivos e diretórios acessíveis
e. Ao usar o comando chroot, o comando iniciado está sendo executado em seu próprio namespace e não pode se comunicar com outros processos
Sua resposta está incorreta.
A resposta correta é:
O caminho chroot precisa conter todos os dados requeridos pelos programas em execução no ambiente chroot


- Quais arquivos lista quais usuários podem executar comandos usando o sudo? (Especifique o nome completo do arquivo, incluindo o caminho.)
Resposta: /etc/sudoers
A resposta correta é: /etc/sudoers

- O que significa a seguinte linha do arquivo de configuração do sudo? geeko ALL=/sbin/shutdown
a. Todos os usuários (exceto geeko) têm permissão para desligar o computador.
b. Permite ao usuário geeko desligar o computador.
c. Todos os usuários têm permissão para desligar o computador.
d. Todos os usuários do computador com o nome geeko estão autorizados a desligar o computador.
e. Usuário geeko tem permissão para desligar o computador com o nome ALL.
Sua resposta está correta.
A resposta correta é:
Permite ao usuário geeko desligar o computador.

- Em qual caminho os dados, que podem ser alterados pelo comando sysctl, são acessíveis?
a. /sysctl/
b. /proc/sys/
c. /dev/sys/
d. /sys/
Sua resposta está correta.
A resposta correta é:
/proc/sys/

- Qual das seguintes ações deve ser considerada quando um jail chroot FTP é criado? (Escolha TRÊS respostas corretas.)
a. Crie /dev/kmem no ambiente chroot.
b. Crie o usuário ftp no ambiente chroot.
c. Bind-mount /proc no ambiente chroot.
d. Crie /etc/ passwd no ambiente chroot.
e. Crie /dev/ e /etc/ no ambiente chroot.
Sua resposta está parcialmente correta.
Você selecionou corretamente 2.
As respostas corretas são:
Crie /etc/ passwd no ambiente chroot.,
Crie /dev/ e /etc/ no ambiente chroot.,
Crie o usuário ftp no ambiente chroot.

- Em um novo sistema Linux, o usuário root está sendo solicitado a fornecer a senha do usuário root antes de poder usar o comando su. Qual linha no arquivo /etc/pam.d/su permitirá que o root use o su sem fornecer senhas?
a. auth sufficient pam_norootpw.so
b. auth required pam_rootok.so
c. auth sufficient pam_rootok.so
d. auth required pam_norootpw.so
Sua resposta está correta.
A resposta correta é:
auth sufficient pam_rootok.so

- Qual das seguintes ações corrigiria o erro?
a. O arquivo /etc/ld.so.conf no sistema de arquivos raiz deve conter o caminho para o diretório lib apropriado na cadeia chroot
b. Execute o programa usando o comando chroot e a opção -static_libs
c. Crie um link simbólico que aponte para a biblioteca necessária fora da cadeia chroot
d. Copie a biblioteca requerida para o diretório lib apropriado na cadeia chroot
Sua resposta está correta.
A resposta correta é:
Copie a biblioteca requerida para o diretório lib apropriado na cadeia chroot

- Executar o sysctl tem o mesmo efeito que:
a. Alterando os parâmetros de compilação do kernel
b. Alterando os limites do processo usando ulimit
c. Não há equivalente a este utilitário
d. Editando arquivos dentro de / etc / sysconfig
e. Escrevendo para arquivos dentro de / proc
Sua resposta está incorreta.
A resposta correta é:
Escrevendo para arquivos dentro de / proc

- O programa vsftpd, rodando em uma jaula chroot, dá o seguinte erro:
/bin/vsftpd: error while loading shared libraries: libc.so.6: cannot open shared object file: No such file or directory. 
Qual das seguintes ações corrigiria o erro?
a. Copie a biblioteca requerida para o diretório lib apropriado na cadeia chroot
b. Crie um link simbólico que aponte para a biblioteca necessária fora da cadeia chroot
c. O arquivo /etc/ld.so.conf no sistema de arquivos raiz deve conter o caminho para o diretório lib apropriado na cadeia chroot
d. Execute o programa usando o comando chroot e a opção: -static_libs
Sua resposta está correta.
A resposta correta é:
Copie a biblioteca requerida para o diretório lib apropriado na cadeia chroot
