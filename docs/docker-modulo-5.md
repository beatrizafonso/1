## Aula 53

Para imprimir a quantidade de visitas, foi feito o codio em node.js e a 'dockerfile' ficou da seguinte maneira que já foi ensinado antes:

>FROM node:alpine

>WORKDIR '/app'

>COPY package.json .
>RUN npm install
>COPY . .

>CMD ["npm","start"]

Depois vamos contruir a imagem com uma tag 

> `~$ docker build -t beatriz/visits .`

## Aula 54

Para o aplicativo rodar é necessário registrar um segundo contêiner para executar o servidor (redis utilizado no exemplo)

> `~$ docker run redis`

- vamos utilizar **docker compose**.  
_funciona da mesma maneira que docker CLI, mas permite que vc emite vários comandos mais rapidamente._

## Aula 55

Para utilizar o docker compose, vamos executar os mesmos comandos de antes, porém vamos coduficá-los  em um arquivo do diretório do projeto (`docker-compose.yml`).

A pasta ficará da seguinte maneira:

`version: '3'
services:
  redis-server:
    image: 'redis'
  node-app:
    build: .
    ports:
      - '4001:8081'`

## Aula 56

Para conectar essa nova pasta ao código fonte deverá ser colocar dentro da pasta index.js (no local que está especificando o redis):

`{  
  host: 'redis-server',  
  port: 6379  
}`

## Aula 57

para criar nossa imagem:

1. rodar docker compose

> `~$ docker-compose up`  
_se precisar reconstruir: docker-compose up --build_

> `~$ docker run 'imagem'`

para reconstruir a imagem

> `~$ docker build .` 

> `~$ docker run 'imagem'`

## Aula 58 

Iniciar um grupo de contêiners em segundo plano:

> `~$ docker-compose up -d`

Parar contêiners

> `~$ docker-compose down`

## Aula 59 

Para evitar que o cntêiner trave, é possivel adicionar os seguintes codigos dentro do codigo fonte da pasta index.js:
Assim o servidor sairá automaticamente sempre que algo de errado ocorrer.

const process = require('process');  
e  
process.exit(0);

## Aula 60 

Para o contêiner reiniciar automaticamente:

`version: '3'  
services:  
  redis-server:  
    image: 'redis'  
  node-app:  
    restart: on-failure  
    build: .  
    ports:  
      - '4001:8081'`  

- Algumas mensagens para reiniciar  
_- `no` : não reiniciar_  
_- `always` : sempre reiniciar_  
_- `on-failure`: apenas reinicia se o contêiner para com um código de erro_  
_- `unless-stopped`: sempre reiniciar a não ser que alguém o force a parar_  

## Aula 61 

- status dos contêiners que estão em execução dentro do docker:

> `~$ docker-compose ps`