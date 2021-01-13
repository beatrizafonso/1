# Módulo 4

## Aula 53

### Remover um diretório:

> `~$ rm -r 'diretorio'/`

Para saber todas as opções que estão disponíveis dentro de um comando:

> `~$ man 'comando'`

## Aula 54

### Permissões de arquivos e diretórios

- Alterar as permissões de seus arquivos e diretórios

Há 3 tipos de permissão:  
1. `r` - read  
2. `w` - write  
3. `x` - execute  

Há 3 níveis de controle das permissões:  
1. `u` - user (vc)  
2. `g` - group (pessoas do mesmo projeto)  
3. `o` - other (todos no sistema)  

- retirar permissão de um grupo para escrever (group - write)
> `~$ chmod g-w 'arquivo'`    

- retirar permissão de um grupo para ler (group - read)
> `~$ chmod g-r 'arquivo'`  

- retirar permissão do usuário para escrever (user - write)
> `~$ chmod u-w 'arquivo'`

- adicionar permissão ao usuário para ler e escrever no arquivo (user + ler e escrever)
> `~$ chmod u+rw 'arquivo'`

_caso queira adicionar permissão para o grupo ou outros basta troca `u` por `g` ou `o`_

- Retirar a permissão de todos para entrar em um diretório:

> `~$ chmod a-x 'diretório'` 

_para dar a permissão de volta basta trocar `-` por `+`_

## Aula 55 

permissões de arquivos/diretórios usando o método numérico

> `~$ chmod ugo+r 'arquivo' = ~$ chmod 444 'arquivo'`

significado dos números:  
0 = sem permissão  
1 = x  
2 = w  
3 = x+w  
4 = r  
5 = r+x  
6 = r+w  
7 = r+w+x

ordem dos dígitos _ _ _:  
primeiro dígito: usuário  
segundo dígito: grupo  
terceiro dígito: outros

> `~$ chmod 764 'arquivo'`  
_significado: usuário pode ler, escrever e executar; grupo pode ler e escreve; outros podem apenas ler_

## Aula 56 

### Proprietário de um arquivo

- comandos para mudar o proprietário de um arquivo:

1. `chown` : muda o proprietário 
2. `chgrp` : muda o grupo proprietário

mudar o proprietário:

> `~$ chown 'novo proprietário' 'arquivo'`

mudar o grupo:

> `~$ chgrp 'novo grupo' 'arquivo'`

_obs: antes de mudar o proprietário/grupo é necessário obter autorização do su, colocando o comando `su -` e rodando antes, ou colocando `sudo` antes do comando_

## Aula 57 

### Lista de controle de acessos

É possível dar permissão a um usuário particular para ler um arquivo, sem precisar permitir para todos os outros.

**Comandos:**

1. `setfacl` : define  a maneira que vc quer que seja a permissão

2. `getfacl` : da a informação sobre as permissões existente em um arquivo

Para ver quem tem permissão:

> `~$ getfacl 'arquivo'`

Adicionar permissão ao usuário:

> `~$ setfacl -m u:'user':rwx /caminho/para/arquivo`   
_`-m` : para modificar a permissão_

Adicionar permissão ao grupo 

> `~$ setfacl -m g:'grupo':rw /caminho/para/arquivo`

Para permitir que todos os arquivos/diretórios herdem entradas do ACL do diretório em que estão 

> `~$ setfacl -rm "entry" /caminho/para/diretório`

Para remover uma entrada específica para um usuário específico

> `~$ setfacl -x u:'user' /caminho/para/arquivo`

remover todas as permissões a todos 

> `~$ setfacl -b /caminho/para/arquivo`

## Aula 58 

### Comandos de ajuda

> `~$ whatis 'comando'`  
_informações sobre o comando_  
> `~$ 'comando' --help`  
_mais detalhes sobre o comando_  
> `~$ man 'comando'`  
_manual do comando, imprime uma lista de comandos que podem ser utilizados_  

## Aula 59
