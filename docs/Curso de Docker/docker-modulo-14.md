# Módulo 14

# Criação de um app multi-containers com o Kubernetes

## Caminho 

1. Criar os arquivos de configuração e de deploy;
2. Testar localmente no minikube;
3. Criar um repo no githhub > Travis CI para construir as imagens e fazer o deploy;
4. Fazer o deploy para o provedor de nuvem.

- Depois de entrar na pasta do projeto, para checar se está tudo funcionando:

> ~$ `docker-compose up --build`

> ~$ `docker-compose up` 

A partir daí é possivel acessar no navegador: `localhost:3050`

_obs: antes de começar as modificações é bom fazer uma cópia da pasta para que sirva como backup_

1. Limpar alguns arquivos criados anteriormente que não são mais necessários: `travis.yml` ; `docker-compose.yml` ; `dockerrun.aws.jason .` ; pasta `NginX` .

2. Criar um nova pasta `k8s`; dentro dela criar 1 arquivo para cada objeto que estará dentro do nó:

## exemplo de arquivo de deploy .yaml

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: client-deployment
spec:
    replicas: 3
    selector:
        matchLabels:
            component: web
    template:
        metabase:
            label:
                componet: web
        spec: 
            containers:
                - name: client
                    image: beatrizafonso/multi-client
                    ports:
                        - containerPort: 3000
```

## Tipos de objetos:
_(aula 224)_
- Pods: Roda 1 ou mais contaners associados;
- Services: configura a rede no kebernetes;
    - ClusterIP: expõe um conjunto de Pods a outros objetos no cluster;
    - NodePort: Expõe um conjunto de Pods para o mundo externo.

## Exemplo de arquivo de ClusterIP .yaml
_(aula 225)_

- Criando um arquivo de configurção do tipo ClusterIP > dentro da pasta k8s

`client-cluster-ip-service.yaml`:

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: client-cluster-ip-service
spec:
    type: ClusterIP
    selector:
        component: web
    ports:
        - port: 3000
            targetPort: 3000
```
 _selector: especifica o seletor que o deploy usará para encontrar de pods que vai controlar._


_obs: quando o arquivo não precisar ser associado a nenhum outro arquivo, não é necesssário especificar a porta_

### Checar se o arquivo criado está funcionando
_(aula 226)_

_deletar todos os deployments_:
> ~$ `kubectl get deployments`  
> ~$ `kubectl delete 'tipo de objeto' 'nome'`

_deletar todos os serviços:_
> ~$ `kubectl get services`  
    _deixar apenas o tipo clusterIP:_   
> ~$ `kubectl delete 'tipo' 'nome'`

> ~$ `kubectl apply -f 'nome da pasta'`

Para ver se os arquivos estão rodando normalmente: 

> ~$ `kubectl get pods`
> ~$ `kubectl get deployments`
> ~$ `kubectl get services`

> ~$ `kubectl logs 'nome'`(aparece quando rodamos kubectl get pods)


### Combinar arquivos em 1 único arquivo
é possível combinar os arquivos de deploy e de clusterID em um unico arquivo basta separá-los com '---' como feito abaixo > `server-deployment.yaml`

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: server-deployment
spec:
    replicas: 3
    selector:
        matchLabels:
            component: server
    template:
        metabase:
            labels:
                componet: server
        spec: 
            containers:
                - name: server
                    image: beatrizafonso/multi-server
                    ports:
                        - containerPort: 5000
---
apiVersion: apps/v1 
kind: Service
metadata: 
    name: server-cluster-ip-service
spec:
    type: ClusterIP
    selector:
        component: server
    ports:
        - port: 5000
            targetPort: 5000
```

## Repply dos arquivos

> ~$ `kubectl apply -f 'nome da pasta'`

Para ver se os arquivos estão rodando normalmente: 

> ~$ `kubectl get pods`
> ~$ `kubectl get deployments`
> ~$ `kubectl get services`

> ~$ `kubectl logs 'nome'`(aparece quando rodamos kubectl get pods)

## PVC (Persistent Volume Claim)

É importante ter esses volumes com bancos de dados para que não haja perda de dados, caso o Pod ou Contêiner travar.

obs: Se você quiser aumentar o número de replicas, é preciso adicionar algumas configurações adicionais,e não apenas modificar o numero no arquivo.

### Volume em Kubernetes

É um objeto que permite o contêiner armazenar dados, podemos criar um arquivo de configuração para ele. 

### Persistent Volume

Um objeto aonde criamos algum tipo de armazenamento durável que não é vinculado a nenhum Pod ou contêiner. Assim se algo travar, os dados estarão seguros e será recriado o contêiner ou Pod.

### Persistent Volume Claim
(238 - 241)

Nada é armazenado no PVC, ele apenas tem informações dos dados disponíveis que você pode solicitar dentro do arquivo de configuração do Pod. Assim, o Kubernetes irá 'procurar' nos _Persistent Volumes_ existentes ou tentará criá-lo em tempo real.

arquivo PVC dentro de k8s:
`database-persistent-volume-claim.yaml`:

```
apiVersion: v1 
kind: PersistentVolumeClaim
metadata:
    name: database-persistent-volume-claim
spec:
    acessModes:
        - ReadWriteOnce
    resources:
        requests:
            storage: 2Gi
```

- acessModes: 
    - ReadWriteOnde: Lê e grava as infos no volume e pode ser usada por um único nó de cada vez;
    - ReadOnlyMany: Apenas lê a informação e pode ser usado pozr múltiploa nós;
    - ReadWriteMany: Lê e grava a info e pode ser usado por múçtiplos nós.


- Storage: fala o espaço que as infos recebidas tem que ter.

#### Designando o PVC a um arquivo
_(aula 242)_

Pegaremos um arquivo de deploy que exemplificamos anteriormente para adicionar a aba 'volumes':

`postgres-deployment.yaml`:

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: postgres-deployment
spec:
    replicas: 1
    selector:
        matchLabels:
            component: postgres
    template:
        metabase:
            label:
                componet: postgres
        spec: 
            volumes: 
                - name: postgres-storage
                    persistentVolumeClaim
                        claimName: database-persistent-volume-claim
            containers:
                - name: postgres
                    image: postgres
                    ports:
                        - containerPort: 5432
                    volumeMounts:
                        - name: postgres-storage
                            mountPath: /var/lib/postgresql/data
                            subPath: postgres
```

#### Apply do PVC

> ~$ `kubectl apply -f 'nome da pasta'`

> ~$ `kubectl get pods`

> ~$ `kubectl get pv`  
_(persistent volume)_

> ~$ `kubectl get pvc`  
_(persistent volume claim)_

## Enviroment Variables

adicionando em um arquivo de exemplo:

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: worker-deployment
spec:
    replicas: 1
    selector:
        matchLabels:
            component: worker
    template:
        metabase:
            labels:
                componet: worker
        spec: 
            containers:
                - name: worker
                    image: beatrizafonso/multi-worker
                    env: 
                        - name: REDIS_HOST
                            value: redis-cluster-ip-service
                        - name: REDIS_PORT
                            value: '6379'
```

Outro Exemplo:

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: server-deployment
spec:
    replicas: 3
    selector:
        matchLabels:
            component: server
    template:
        metabase:
            labels:
                componet: server
        spec: 
            containers:
                - name: server
                    image: beatrizafonso/multi-server
                    ports:
                        - containerPort: 5000
                    env: 
                        - name: REDIS_HOST
                            value: redis-cluster-ip-service
                        - name: REDIS_PORT
                            value: '6379'
                        - name: PGUSER
                            value: postgres
                        -name: PGHOST
                            value: postgres-cluster-ip-service
                        - name: PGPORT
                            value: '5432'
                        - name: PGDATABASE
                            value: postgres
```

### PGPASSWORD
(aula 246 - 248)

Para armazenar com segurança algumas infos vamos utilizar um novo tipo de objeto: **Secrets**.

> ~$ `kubectl create secret generic 'nome do segredo' --from-literal 'nome do segredo'='senha'`  
_(kubectl - comando imperativo - tipo de objeto - tipo de segredo - nome do segredo - escrever infos no comando - colocar senha)_

Para verificar se foi criado: 

> ~$ `kubectl get secrets`

Conectar o Secret com a pasta de deployment: 

no final da pasta criada acima, dentro de env: 

```
- name: 'nome do segredo'
    valueFrom:
        secretKeyRef: 
            name: 'nome do segredo'
            key: 'nome do segredo'
```
 na outra pasta de deployment:


```
 env: 
    - name: 'nome do segredo'
        valueFrom:
            secretKeyRef:
                name: 'nome do segredo'
                key: 'nome do segredo'
```
            
Após isso, aplicar as mudanças!