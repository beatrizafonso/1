# Aula 14

1. Criar e executar um contêiner usando uma imagem:

> ~$ docker run 'image name'
- exemplo: docker run hello-world

# Aula 15

1. Executar dentro do contêiner depois que ele for inicializado 
(qualquer comando padrão incluído na imagem não será executado)

>~$ docker run 'image name' command!

- exemplo: docker run busybox echo hi there

_ls: irá aparecer todos os arquivos e pastas dentro de um determinado diretório_

- exemplo: docker run busybox ls

Irá aparecer pastas que estarão dentro do seu contêiner

# Aula 16

1. Listar todos os diferentes contêiners em execução:

> ~$ docker ps

2. Listar todos os contêiners que já foram executados na sua máquina:

> ~$ docker ps --all

# Aula 17 

1. O que acontece quando um contêiner é criado?

> docker run = docker create + docker start

- 'docker run' mostrará todos os logs ou todas as infos que saem do contêiner

- 'docker create' cria e imprime o ID do contêiner:

> ~$ docker create 'image name' 

> ~$ docker start -a 'container id'

_-a : fará com que o docker observe a saída do contẽiner e imprima no terminal_

# Aula 19

1. Remover todos os contêiners:

> ~$ docker system prune

# Aula 20

> ~$ docker logs 'container id'

_logs: utilizado para examinar um contêiner e recuperar todas as informações que foram emitidas a partir dele_

# Aula 21

1. parar um cantêiner que está sendo executado:

> ~$ docker stop 'container id'

_stop: dá um tempo para o contêiner encerrar e fazer uma limpeza (ideal)_

> ~$ docker kill 'container id'

_kill: encerra imediatamente o contêiner sem fazer nenhum trabalho adicional (utilizar quando o 'stop' não funcionar)_

# Aula 23

1. Como executar comandos dentro de um contêiner em execução?

> ~$ docker exec -it 'container id' 'command'

_exec: executar um comando adicional dentro de um contêiner_

_-it = '-i' + '-t' : permite digitar a entrada diretamente no contêiner_

# Aula 24

_-i: garante que qualquer coisa quer vocẽ digite seja direcionado ao comando digitado_

_-t: garante que o comando apareça bem formatado_

# Aula 25 

1. Como abrir um prompt de comando dentro de um contêiner (para não precisar digitar 'docker exec' seguidamente)

Depois que o contêiner estiver rodando abrir um segundo terminal e colocar:

> ~$ docker exec -it 'container id' sh

_sh: é um programa que nos permite digitar comando e executá-los dentro de uma contêiner_

Para sair do prompt de comando: 'ctrl + D' ou 'exit'

# Aula 26 

1. Executar e abrir o prompt de comando dentro do contêiner:
S
> ~$ docker run -it 'image name' sh 

# Aula 27 

