# Aula 67

- instalar a ferramenta para o 'react project'

> ~$ npm install -g create-react-app

> create-react-app 'nome do projeto'

# Aula 68

comandos para interagir com o projeto:

> ~$ npm run start  
> ~$ npm run test  
> ~$ npm run build  

# Aula 70

- para especificar o arquivo que será usado para criar a imagem:

> ~$ docker build -f Dockerfile.dev .

Depois desse processo, já foi instalada todas as dependencia no diretório do porjeto, então para tornar o processo mais rápido, podemos apagar a pasta 'node_modules'.

# Aula 71 

Para rodar o contêiner 

> ~$ docker run -it -p 3000:3000 CONTAINER_ID

# Aula 73 - 75

Para as mudanças feitas no código atualizarem automaticamente:

> ~$ docker run -it -p 3000:3000 -v /app/node_modules -v $(pwd):/app 'image ID'

Comandos adicionais

- _-v$(pwd):/app : para obter o diretório de trabalho atual ou o caminho para ele, pegar tudo que está dentro da pasta e mapear para a pasta do aplicativo em execução_

- _-v /app/node_modules : como apagamos a pasta 'node_modules' é necessário colocar esse comando_

# Aula 77 - 78 

Para facilitar o código acima vamos usar dockercompse.yml

- 
version: '3'  
services:  
  web:   
    build:   
      context: .  
      dockerfile: Dockerfile.dev  
    ports:  
     - "3000:3000"  
    volumes:   
     - /app/node_modules  
     - .:/app  
  
- 

Assim, basta rodar:

> ~$ docker-compose up

# Aula 81

> ~$ docker build -f Dockerfile.dev .

> ~$ docker run -it 'image ID' npm run test

# Aula 82

em um terminal:

> ~$ docker-compose up 

em outro terminal:

> ~$ docker exec -it 'conteiner ID' npm run test

Assim nós podemos manipular os testes feitos no nosso contêiner

# Aula 83

Uma segunda solução, para não precisar realizar os testes manualmente:

Criar um segundo serviço para executar nossos testes dentro da 'dockercompose.yml'

- 
tests:  
    build:  
      context: .  
      dockerfile: Dockerfile.dev  
    volumes:  
      - /app/node_modules  
      - .:/app  
    command: ["npm", "run", "test"]  

- 

Para reconstruir: 

> ~$ docker-compose up --build

# Aula 86

Para conseguirmos executar comandos dentro do contêiner iremos abrir em um segundoterminal o seguinte comando (para descobri o ID basta colocar docker ps):

> ~$ dokcer attach 'container ID'

abrir um terceiro terminal:

> ~$ docker exec -it 'container ID' sh

A partir daí você conseguirá executar comando dentro desse contêiner em execução.

# Aula 87 - 90

Para criar uma compilação de múltiplas etapas dentro da 'dockerfile'

- 

FROM node:alpine  
WORKDIR '/app'  
COPY package.json .  
RUN npm install  
COPY . .  
RUN npm run build  
 
FROM nginx  
COPY --from=0 /app/build /usr/share/nginx/html

- 

# Aula 91

executar NginX

> ~$ docker build .

> ~$ docker run -p 8080:80 'image ID'

agora é possivel acessar no navegador
