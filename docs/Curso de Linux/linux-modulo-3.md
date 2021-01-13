# Módulo 3

## Aula 32
### Abrir o terminal
ctrl + alt + T
### Prompt travado
Para recuperar: ctrl + C

## Aula 38

Para mostrar todos os diretórios e arquivos que estão começando com '/' :

> `~$ cd /`

> `~$ ls -l`

## Aula 39

### Diretórios importantes
1. `/boot` : contém os arquivos usados para o gerenciador de inicialização;
2. `/root` : diretório inicial do usuário;
3. `/dev` : contém os os dispositivos do sitema.. drives, disco etc
4. `/etc` : contém toda a configuração dos arquivos/aplicativos... é possivel modificar os arquivos (emails,etc) com /etc

## Aula 40

- Quais os comandos para ir de um diretório a outra.

**1.** mudança de diretório:  
> `~$ cd`  

**2.** 'print working diretory': informa qual diretório você esta atualmente  
> `~$ pwd`  

**3.** Lista o conteúdo de um diretório ou arquivo  
> `~$ ls -l`  

_`cd ..` : um diretório atrás_

_`cd boot` : encaminha para o diretório 'boot'_

_`cd /` : voltar ao direorio principal_

## Aula 41

- Existem dois caminhos de navegar em um sistema de arquivos:  
**1.** Absolute path: sempre começa com '/' (cd/var/log/samba)  
**2.** relative path: identifica um local em relação a sua posição atual (cd /var -> cd log -> cd samba)

## Aula 42

### tipos de arquivo

> `~$ ls -l`

- `drwxr-xr-x   2 root root       4096 dez 31 10:56 bin`

 tipo de arquivo - quantidade de links - proprietário - grupo - tamanho - mês - dia - horário - nome

primeira coluna - quando começa com:  
- `d` : diretório  
- `l` : link  
- `-` : arquivo  

## Aula 43

### Criando arquivos

> `~$ touch 'arquivo'`
_cria um arquivo vazio_

> `~$ cp 'arquivo' 'diretório de destinação'`  
_copia um arquivo ja existente_ 

> `~$ vi 'arquivo'`  
_cria um arquivo e abre um editor_

_`shift + Q` + digitar `wq!` + enter : para sair do editor_

### Criando diretórios

> `~$ mkdir 'diretório'`

## Aula 45

### Comandos para encontrar arquivos e diretórios

> `~$ find . -name "'arquivo/diretório'"`

> `~$ find / -name "'arquivo'"`  
_quando não se sabe o diretório, esse comando procura em 'root'. (precisa da permissão do su)_

> `~$ locate 'arquivo/diretório'`

- obs: o `locate` é mais rápido que o `find`, porém precisa atualizar sempre que criar um novo arquivo ou diretório:

> `~$ sudo updatedb`

- Quando a permissão for negada:

> `~$ su -`

## Aula 46

- diferença entre `find` e `locate`:

_`locate` tem um banco de dados (e precisa ser atualizado regularmente), já `find` procura o arquivo dentro do sistema._

## Aula 47 

### Alterando a senha

> `~$ passwd 'userid'`

## Aula 48

### Curingas

_Um curinga é um caractere que pode ser usado como substituto para qualquer classe de caracteres em uma pesquisa_

1. `*` : representa o zero ou mais caracteres

2. `?` : representa um único caractere

3. `{}` : representa um intervalo de caracteres 

> `~$ touch diretório{1..9}`  
_irá criar 9 diretórios (diretório1, diretório2... diretório9)_

> `~$ ls -l diretório*`    
_irá imprimir todos os diretórios que começam com 'diretório'_

> `~$ ls -l ?asta*`    
_irá imprimir todos os arquivos, independente do primeiro caractere, que tenha 'asta' e qualquer coisa depois_

> `~$ ls -l * [cd] *`   
_imprime qualquer diretório que tenha 'cd' no meio_ 

## Aula 49 

### Soft e Hard Link
_inode: ponto ou número de um arquivo no 'hard disk'_ 

_soft link: link que vai ser removido se um arquivo for removido ou renomeado_

_hard link: deletando, renomeando ou movendo o arquivo original não vai afetar o 'hard link'_

- criar um hard link:

> `~$ ln 'arquivo'`

- criar um soft link:

> `~$ ln -s 'arquivo'`

- escrever dentro de um arquivo:

> `~$ echo "'qualquer coisa aqui'" > 'arquivo'`  
> `~$ echo "'comentário adicional'" >> 'arquivo'`

- imprimir o que está escrito:

> `~$ cat 'arquivo'`