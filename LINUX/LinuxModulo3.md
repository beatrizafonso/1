# Aula 32
- abrir o terminal: ctrl + alt + T
- prompt travado,  para recuperar: ctrl + C

# Aula 38

Para mostrar todos os diretórios e arquivos que estão começando com '/' :

> cd /
> ls -l

# Aula 39

Pastas importantes
1. /boot : contém os arquivos usados para o gerenciador de inicialização;
2. /root : pasta inicial do usuário;
3. /dev : contém os os dispositivos do sitema.. drives, disco etc
4. /etc : contém toda a configuração dos arquivos/aplicativos... é possivel modificar os arquivos (emails,etc) com /etc

# Aula 40

- Quais os comandos para ir de uma pasta a outra.

1. mudança de diretório:
> ~$ cd
2. 'print working diretory': informa qual pasta você esta atualmente
> ~$ pwd
3. Lista o conteúdo de uma pasta ou arquivo
> ~$ ls -l

_cd .. : um diretório atrás_

_cd boot : encaminha para o diretório 'boot'_

_cd / : voltar ao direorio principal_

# Aula 41

- Existem dois caminhos de navegar em um sistema de arquivos:
1. Absolute path: sempre começa com '/' (cd/var/log/samba)
2. relative path: identifica um local em relação a sua posição atual (cd /var -> cd log -> cd samba)

# Aula 42

> ~$ ls -l

- drwxr-xr-x   2 root root       4096 dez 31 10:56 bin

 tipo de arquivo - quantidade de links - proprietário - grupo - tamanho - mês - dia - horário - nome

primeira coluna - quando começa com:
- 'd' : pasta
- 'l' : link 
- '-' : arquivo

# Aula 43

1. Criando pastas:

> ~$ touch 'nome do arquivo' : cria um arquivo vazio

> ~$ cp 'nome do arquivo' 'nome da pasta de destinação' : copia um arquivo ja existente 

> ~$ vi 'nome da arquivo' : cria um arquivo e abre um editor

_'shift + Q' + digitar 'wq!' + enter : para sair do editor_

2. Criando pastas:

> ~$ mkdir 'nome da pasta'

# Aula 45

- comandos para encontrar arquivos e pastas

> ~$ find . -name "'nome do arquivo/pasta'"

> ~$ find / -name "'nome do arquivo'"  : quando não se sabe o diretório, esse comando procura em 'root'. (precisa da permissão do su)

> ~$ locate 'nome do arquivo/pasta'

- obs: o 'locate' é mais rápido que o 'find', porém precisa atualizar sempre que criar um novo arquivo ou pasta:

> ~$ sudo updatedb

- Quando a permissão for negada:

> ~$ su -

# Aula 46

- diferença entre 'find' e 'locate':

_'locate' tem um banco de dados (e precisa ser atualizado regularmente), já 'find' procura o arquivo dentro do sistema.

# Aula 47 

- Alterando a senha

> ~$ passwd 'userid'

# Aula 48

- Curingas

_Um curinga é um caractere que pode ser usado como substituto para qualquer classe de caracteres em uma pesquisa_

1. '*' : representa o zero ou mais caracteres

2. ? : representa um único caractere

3. {} : representa um intervalo de caracteres 

> ~$ touch pasta{1..9} : irá criar 9 pastas (pasta1, pasta2... pasta9)

> ~$ ls -l pasta* : irá imprimir todas as pastas que comçam com 'pasta'

> ~$ ls -l ?asta* : irá imprimir todos os arquivos, independente do primeiro caractere, que tenha 'asta' e qualquer coisa depois

> ~$ ls -l * [cd] * : imprime qualquer pasta que tenh 'cd' no meio 

# Aula 49 

_inode: ponto ou número de um arquivo no 'hard disk'_ 

_soft link: link que vai ser removido se um arquivo for removido ou renomeado_

_hard link: deletando, renomeando ou movendo o arquivo original não vai afetar o 'hard link'_

- criar um hard link:

> ~$ ln 

- criar um soft link:

> ~$ ln -s

- escrever dentro de um arquivo:

> ~$ echo "'qualquer coisa aqui'" > 'nome do arquivo'  
> ~$ echo "'comentário adicional'" >> 'nome do arquivo'

- imprimir o que está escrito:

> ~$ cat 'nome do arquivo'