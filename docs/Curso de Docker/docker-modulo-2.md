# Módulo 2

## Aula 14

### Criar e executar um contêiner usando uma imagem

> `~$ docker run 'image name'`
- exemplo: `docker run hello-world`

## Aula 15

### Executar um comando dentro do contêiner
(qualquer comando padrão incluído na imagem não será executado)

> `~$ docker run 'image name' command!`

- exemplo: `docker run busybox echo hi there`

_`ls`: irá aparecer todos os arquivos e diretórios dentro de um determinado diretório_

- exemplo: `docker run busybox ls`

Irá aparecer diretórios que estarão dentro do seu contêiner

## Aula 16

### Listar todos os diferentes contêiners em execução

> `~$ docker ps`

### Listar todos os contêiners que já foram executados na sua máquina

> `~$ docker ps --all`

## Aula 17 

### O que acontece quando um contêiner é criado?

> docker run = docker create + docker start

- `docker run` mostrará todos os logs ou todas as infos que saem do contêiner

- `docker create` cria e imprime o ID do contêiner:

> `~$ docker create 'image name'` 

> `~$ docker start -a 'container id'`

_`-a` : fará com que o docker observe a saída do contẽiner e imprima no terminal_

## Aula 19

## Remover todos os contêiners

> `~$ docker system prune`

## Aula 20

### Examinar o contêiner

> `~$ docker logs 'container id'`

_logs: utilizado para examinar um contêiner e recuperar todas as informações que foram emitidas a partir dele_

## Aula 21

### Parar um contêiner que está sendo executado

> `~$ docker stop 'container id'`

_`stop`: dá um tempo para o contêiner encerrar e fazer uma limpeza (ideal)_

> `~$ docker kill 'container id'`

_`kill`: encerra imediatamente o contêiner sem fazer nenhum trabalho adicional (utilizar quando o 'stop' não funcionar)_

## Aula 23

### Comandos dentro de um contêiner em execução

> `~$ docker exec -it 'container id' 'command'`

_`exec`: executar um comando adicional dentro de um contêiner_

_`-it` = `-i` + `-t` : permite digitar a entrada diretamente no contêiner_

## Aula 24

### Flag -i e -t

_`-i`: garante que qualquer coisa quer vocẽ digite seja direcionado ao comando digitado_

_`-t`: garante que o comando apareça bem formatado_

## Aula 25 

### Prompt de comando dentro de um contêiner 
(para não precisar digitar 'docker exec' seguidamente)

Depois que o contêiner estiver rodando abrir um segundo terminal e colocar:

> `~$ docker exec -it 'container id' sh`

_`sh`: é um programa que nos permite digitar comando e executá-los dentro de uma contêiner_

Para sair do prompt de comando: 'ctrl + D' ou 'exit'

## Aula 26 

- Executar e abrir o prompt de comando dentro de um contêiner

> `~$ docker run -it 'image name' sh` 

## Aula 27 

Tomar cuidado ao abrir o prompt de comando de um cantêiner específico em dois terminais, as mudanças que serão feitas em um não parecerá no outro.