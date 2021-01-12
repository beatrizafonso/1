## Aula 39

passos para criar um projeto:  
1. criar um app em node.js  
2. criar um 'dockerfile'  
3. construir a imagem dentro do 'dockerfile'  
4. executar a imagem como um contêiner  
5. conectar o app com o navegador  

## Aula 41 - 44

Há um erro comum na nova versão do Node, e pode aparecer a seguinnte mensagem quando construimos 'build' nossa 'dockerfile'

_npm: not found_

Para resolver esse problema:

1. Encontrar uma nova imagem de base no site: https://hub.docker.com/search?q=&type=image


## Aula 45 

Depois de construir (docker build .) a 'dockerfile' corrigindo os erros acima, irá aparece um novo erro.  

Para resolvê-lo irá adicionar a seguinte instrução na 'dockerfile':

> COPY ./ ./  
_É utilizada para mover arquivos e pastas do nosso sitema de arquivos local para o sistema de arquivos dentro do contêiner (criado temporariamente durante o processo de construção da pasta)_

Depois disso, a imagem é criada porém não conseguimos acessá-la no navegador: http://localhost:8080/

## Aula 47

para conseguir acessar pelo navegador:

> ~$ docker run -p 8080:8080 'imageID'  
_obs: '8080' foi especificado dentro da pasta com o código_

O que significa 8080:808O?  
_Encaminhar solicitações 8080 de entrada do host local para 8080 dentro do contêiner (as solicitações sem sempre são inguais)_

## Aula 48

Não é uma boa prática copiar tudo que está no seu sistema de arquivos local para o sistema de arquivos do contêiner temporário, já que alguma pasta pode conflitar.  
Para isso adicionar após FROM: 

> WORKDIR /usr/app

## Aula 49 - 50

Quando fizer uma alteração no código fonte do seu projeto, para não baixar todas as dependências novamente no processo de contrução `build`:

para isso especificar na etapa incial de COPY a única coisa que quer copiar (arquivo não modificado)

> COPY ./package.json ./

> RUN npm install

> COPY ./ ./