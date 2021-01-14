# Módulo 7

## Ferramentas de armazenamento, teste e aplicação de código: 
_(Aula 92 - 98)_

### Github  
_(aula 93)_

    - criando um repositório e fazendo o push do código para o github

### Travis CI   
_(aula 94 - 98)_

**1.** vincular com a conta do github, ativar o repositório que vc quer trabalhar no Travis CI  
    - Travis CI identifica quando vc faz um novo commit e realiza alguns trabalhos (ex: testes, implantar o projeto no AWS)  
**2.** Criar uma pasta `.travis.yml`
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

**3.** fazer o push das mudanças no github

**4.** abrir o travis CI e procurar o repositório de teste, em 'job log' o teste (que foi escrito na pasta acima) será feito.

### AWS 
_(aula 99 - 101)_

1. criar conta no AWS [aqui](https://aws.amazon.com/pt/) 

2. Em AWS services procurar: elastic beanstalk (este é ideal quando executamos 1 contêiner por vez)

3. criar uma nova aplicação  
Application name: docker > Platform: Docker > Platform branch: Docker running on 64bit Amazon Linux > create application

4. assim que criada será criada uma URL para essa aplicação. 

#### Aplicação automatica no AWS com Travis CI 
_(aula 102 - 109)_

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
access_key_id : $ AWS_ACCESS_KEY
secret_access_key : $ AWS_SECRET_KEY

```

**Para encontrar o bucket_name**:  

`site AWS > services > search s3 > buscar o nome mais parecido > copiar`

**Para encontrar o bucket_path**:  

`site AWS > services > search s3 > buscar o nome mais parecido > pasta com nome do projeto`  
_obs: pode acontecer da pasta não ser criada, nessa ocasião utilizar o nome do app_

**Gerar chaves da API**:  
_(aula 105)_

`site AWS > services > search IAM > users > add user`

* Processo para adiciociar usuário:  
_add user > colocar o nome > Programmatic Acess > Next:permissions > AttachExisting Polices Directly > Procurar por beanstalk > marcar caixa ao lado de AWSElasticBeanstalkFullAcess > Next:tags > Next:review > create user_

* Depois que as chaves são geradas é preciso escondê-las e não utiliza-las direto na pasta, para isso:  
Travis dashboard > more options > settings > enviroment variables

- Após isso, fazer o push para o GitHub e observar o programa rodando no Travis CI

_Obs: se o 'AWS build' estiver falhando fazer o seguinte_

Para o Travis CI mapear a porta de entrada, adicionar o `EXPOSE` a `Dockerfile`:

```
FROM node:alpine  
WORKDIR '/app'  
COPY package.json .  
RUN npm install  
COPY . .  
RUN npm run build  
 
FROM nginx  
EXPOSE 80
COPY --from=0 /app/build /usr/share/nginx/html

```

### Trabalhando com uma equipe  
_(Aula 110 - 111)_

1. Criar um branch no GitHub para fazer o push das mudanças no código

2. Após o push entrar no repositório do gitHub > 'Compare & pull request' > 'Create Pull Request'

3. Depois do código passar pelas verificações > 'Merge pull request'

4. Verificar o Travis CI e se AWS foi atualizado