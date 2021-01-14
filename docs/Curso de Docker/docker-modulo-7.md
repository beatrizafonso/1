## Aula 92 - 98

### Ferramentas de armazenamento e teste de código: 

#### Github  
_(aula 93)_
    - criando um repositório e fazendo o push do código para o github

#### Travis CI   
_(aula 94 - 98)_

1. vincular com a conta do github, ativar o repositório que vc quer trabalhar no Travis CI  
    - Travis CI identifica quando vc faz um novo commit e realiza alguns trabalhos (ex: testes, implantar o projeto no AWS)  
2. Criar uma pasta `.travis.yml`
    - Nesta pasta terá os comandos que o Travis irá executar:

```
language: generic
sudo: required 
services:
 - docker

before_install:
 - docker build -t 'nome da tag' -f Dockerfile.dev .

script:
  - docker run -e CI=true 'nome da tag' npm run test

```

3. fazer o push das mudanças no github

4. abrir o travis CI e procurar o repositório de teste, em 'job log' o teste (que foi escrito na pasta acima) será feito.

#### AWS 
_(aula 99 - 101)_

1. criar conta no AWS [aqui](https://aws.amazon.com/pt/) 

2. Em AWS services procurar: elastic beanstalk (este é ideal quando executamos 1 contêiner por vez)

3. criar uma nova aplicação, assim que criada será criada uma URL para essa aplicação.

##### Aplicação automatica no AWS com Travis CI 
_(aula 102)_

A aplicação é feita depois de passar por todos os testes.

Modificações no `.travis.yml`:

```
language: generic
sudo: required 
services:
 - docker

before_install:
 - docker build -t 'nome da tag' -f Dockerfile.dev .

script:
  - docker run -e CI=true 'nome da tag' npm run test

deploy:
 provider: 'AWSservice'
 region: "'região da aplicação'"
 name: "'nome do app'"
 env: "'nome do ambiente'"
 bucket_name: "'bucket_name'"
 bucket_path: "'bucket_path'"
 on: 
  branch: master

```

Exemplo com URL: 
Docker-env.qbtbvwcxmh.us-west-2.elasticbeanstalk.com 

```
deploy:
 provider: elasticbeanstalk
 region: "us-west-2"
 name: "docker"
 env: "Docker-env"
 bucket_name: "bucket_name"
 bucket_path: "docker"
 on: 
  branch: master

```

**Para encontrar o bucket_name**:  
site AWS > services > search s3 > buscar o nome mais parecido > copiar

**Para encontrar o bucket_path**:  
site AWS > services > search s3 > buscar o nome mais parecido > pasta com nome do projeto
_obs: pode acontecer da pasta não ser criada, nessa ocasião utilizar o nome do app_