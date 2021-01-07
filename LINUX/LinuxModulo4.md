# Aula 53

Remover um diretório:

> ~$ rm -r 'diretorio'/

Para saber todas as opções que estão disponíveis dentro de um comando:

> ~$ man 'comando'

# Aula 54

- Alterar as permissões de seus arquivos e diretórios

Há 3 tipos de permissão:
1. r - read
2. w - write
3. x - execute

Há 3 níveis de controle das permissões:
1. u - user (vc)
2. g - group (pessoas do mesmo projeto)
3. o - other (todos no sistema)

- retirar permissão de um grupo para escrever (group - write)
> ~$ chmod g-w 'arquivo'    

- retirar permissão de um grupo para ler (group - read)
> ~$ chmod g-r 'arquivo'  

-retirar permissão do usuário para escrever (user - write)
> ~$ chmod u-w 'arquivo'

- adicionar permissão ao usuário para ler e escrever no arquivo (user + ler e escrever)
> ~$ chmod u+rw 'arquivo'

_caso queira adicionar permissão para o grupo ou outros basta troca 'u' por 'g' ou 'o'_

Retirar a permissão de todos para entrar em um diretório:

> ~$ chmod a-x 'diretório' 

_para dar a permissão de volta basta trocar '-' por '+'_

# Aula 55 

permissões de arquivos/diretórios usando o método numérico

> ~$ chmod ugo+r 'arquivo' = ~$ chmod 444 'arquivo'

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

> ~$ chmod 764 'arquivo'  
_significado: usuário pode ler, escrever e executar; grupo pode ler e escreve; outros podem apenas ler_

# Aula 56 

