# Aula 14

1. Criar e executar um container usando uma imagem:

> ~$ docker run 'image name'
- exemplo: docker run hello-world

# Aula 15

1. Executar dentro do container depois que ele for inicializado 
(qualquer comando padrão incluído na imagem não será executado)

>~$ docker run 'image name' command!

- exemplo: docker run busybox echo hi there

_ls: irá aparecer todos os arquivos e pastas dentro de um determinado diretório_

- exemplo: docker run busybox ls

Irá aparecer pastas que estarão dentro do seu container

# Aula 16

1. Listar todos os diferentes containers em execução:

> ~$ docker ps

2. Listar todos os containers que já foram executados na sua máquina:

> ~$ docker ps --all

# Aula 17 

1. O que acontece quando um container é criado?

> docker run = docker create + docker start

- 'docker run' mostrará todos os logs ou todas as infos que saem do container

- 'docker create' cria e imprime o ID do container:

> ~$ docker create 'image name' 

> ~$ docker start -a 'container id'

_-a : fará com que o docker observe a saída do container e imprima no terminal_