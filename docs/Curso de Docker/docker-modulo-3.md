# Módulo 3

## Aula 30

### Criando imagens no docker 

**1.** criar um diretório:

> `~$ mkdir 'nome do diretorio'`

**2.** mudar para o diretório criado 

> `~$ cd 'nome do diretório'`

**3.** iniciar o editor de código dentro dessa pasta

> `~$ code .`

**4.** criar uma pasta (Dockerfile) sem extensão no seu editor de texto e começar a criar a imagem

Dentro da pasta: 

**1.** Usar uma imagem existente como base (utilizar uma imagem de acordo com as suas nessecidades, 'alpine' tem as configurações desejadas para o que queremos executar) 

> FROM 'nome da imagem' (from alpine)

**2.** baixar e instalar uma dependencia (rodar um comando que existe dentro da imagem) 

> RUN apk add --update redis 

**3.** falar à imagem o que fazer quando inicializar o contêiner 

> CMD ["redis-server"]

**4.** salvar o arquivo e ir para o terminal

> `~$ docker build .`

> `~$ docker run 'id criado'` 

_obs: se precisar apagar a imagem que foi criada rodar  

> `~$ docker system prune`_

## Aula 33

usamos o `build` para obter um arquivo do docker e gerar uma imagem a partir dele; o `.` está especificando o que deve ser construido

## Aula 35

### Reconstruindo a imagem

Ao reconstruir uma imagem (caso tenha colocado um comando adicional) tentar colocar sempre em ordem, para que não tenha que instalar tudo de novo. 

## Aula 36

### Imagem com tag 

Para colocar uma tag em uma imagem e não precisar colocar o ID sempre que quiser rodar ela:

> `~$ Docker build -t 'docker ID'/'nome do projeto':'versão' .`  
_(a versão será quase sempre a mais recente - 'latest'; meu docker ID: beatrizafonso)_

Depois disso, para rodar a imagem basta:

> `~$ docker run 'docker ID'/'nome do projeto'`

## Aula 38 

### Gerar uma imagem manualmente

**1.** 

> `~$ docker run -it alpine sh` 
> `/# apk add --update redis`

**2.** abrir um segundo terminal:

> `~$ docker ps`  
_(para ver os contêiners que estão rodando)_

> `~$ docker commit -c 'CMD ["redis-server"]' 'container id'`  
_(o ID do contêiner irá estar impresso depois do 'docker ps')_

Depois disso irá aparece o id da imagem.

> `~$ docker run 'id da imagem'` 

_obs: ninguém cria uma imagem manualmente, é muito mais facil com um arquivo do docker 'dockerfile'_