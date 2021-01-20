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

### exemplo de arquivo de deploy .yaml

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

### Tipos de objetos:
_(aula 224)_
- Pods: Roda 1 ou mais contaners associados;
- Services: configura a rede no kebernetes;
    - ClusterIP: expõe um conjunto de Pods a outros objetos no cluster;
    - NodePort: Expõe um conjunto de Pods para o mundo externo.

### Exemplo de arquivo de ClusterIP .yaml
_(aula 225)_

- Criando um arquivo de configurção do tipo ClusterIP > dentro da pasta k8s 

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

Para checar se estão funcionando (aula 226):

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
é possível combinar os arquivos de deploy e de clusterID em um unico arquivo basta separá-los com '---' como feito abaixo > `.yaml`

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

#### Repply dos arquivos

> ~$ `kubectl apply -f 'nome da pasta'`

Para ver se os arquivos estão rodando normalmente: 

> ~$ `kubectl get pods`
> ~$ `kubectl get deployments`
> ~$ `kubectl get services`

> ~$ `kubectl logs 'nome'`(aparece quando rodamos kubectl get pods)
