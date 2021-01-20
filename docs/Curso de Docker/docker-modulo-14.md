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

- `client-deployment.yaml`

```
apiVersion: apps/v1 
kind: Deployment
metadata: 
    name: client-deployment
spec:
    replicas: 3
    selector
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

ClusterIP: 