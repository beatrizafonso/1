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

# Aula 76