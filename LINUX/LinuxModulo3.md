# Aula 32
- abrir o terminal: ctrl + alt + T
- prompt travado,  para recuperar: ctrl + C

# Aula 38

Para mostrar todos os diretórios e arquivos que estão começando com '/' :

> cd /
> ls -l

# Aula 39

diretórios importantes
1. /boot : contém os arquivos usados para o gerenciador de inicialização;
2. /root : diretório inicial do usuário;
3. /dev : contém os os dispositivos do sitema.. drives, disco etc
4. /etc : contém toda a configuração dos arquivos/aplicativos... é possivel modificar os arquivos (emails,etc) com /etc

# Aula 40

- Quais os comandos para ir de um diretório a outra.

1. mudança de diretório:
> ~$ cd
2. 'print working diretory': informa qual diretório você esta atualmente
> ~$ pwd
3. Lista o conteúdo de um diretório ou arquivo
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
- 'd' : diretório
- 'l' : link 
- '-' : arquivo

# Aula 43

1. Criando diretórios:

> ~$ touch 'arquivo' : cria um arquivo vazio

> ~$ cp 'arquivo' 'diretório de destinação' : copia um arquivo ja existente 

> ~$ vi 'arquivo' : cria um arquivo e abre um editor

_'shift + Q' + digitar 'wq!' + enter : para sair do editor_

2. Criando diretórios:

> ~$ mkdir 'diretório'

# Aula 45

- comandos para encontrar arquivos e diretórios

> ~$ find . -name "'arquivo/diretório'"

> ~$ find / -name "'arquivo'"  : quando não se sabe o diretório, esse comando procura em 'root'. (precisa da permissão do su)

> ~$ locate 'arquivo/diretório'

- obs: o 'locate' é mais rápido que o 'find', porém precisa atualizar sempre que criar um novo arquivo ou diretório:

> ~$ sudo updatedb

- Quando a permissão for negada:

> ~$ su -

# Aula 46

- diferença entre 'find' e 'locate':

_'locate' tem um banco de dados (e precisa ser atualizado regularmente), já 'find' procura o arquivo dentro do sistema._

# Aula 47 

- Alterando a senha

> ~$ passwd 'userid'

# Aula 48

- Curingas

_Um curinga é um caractere que pode ser usado como substituto para qualquer classe de caracteres em uma pesquisa_

1. '*' : representa o zero ou mais caracteres

2. ? : representa um único caractere

3. {} : representa um intervalo de caracteres 

> ~$ touch diretório{1..9} : irá criar 9 diretórios (diretório1, diretório2... diretório9)

> ~$ ls -l diretório* : irá imprimir todos os diretórios que começam com 'diretório'

> ~$ ls -l ?asta* : irá imprimir todos os arquivos, independente do primeiro caractere, que tenha 'asta' e qualquer coisa depois

> ~$ ls -l * [cd] * : imprime qualquer diretório que tenh 'cd' no meio 

# Aula 49 

_inode: ponto ou número de um arquivo no 'hard disk'_ 

_soft link: link que vai ser removido se um arquivo for removido ou renomeado_

_hard link: deletando, renomeando ou movendo o arquivo original não vai afetar o 'hard link'_

- criar um hard link:

> ~$ ln 'arquivo'

- criar um soft link:

> ~$ ln -s 'arquivo'

- escrever dentro de um arquivo:

> ~$ echo "'qualquer coisa aqui'" > 'arquivo'  
> ~$ echo "'comentário adicional'" >> 'arquivo'

- imprimir o que está escrito:

> ~$ cat 'arquivo'