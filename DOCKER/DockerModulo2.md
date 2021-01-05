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


