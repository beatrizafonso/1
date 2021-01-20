# Módulo 13

## Atualizar o 'Pod' gerado para usar imagem 'multi-worker'
(aula 202 - 203)

_OBS: O nome e o tipo não podem mudar ao fazer a atualização do objeto, apenas a imagem._

```
apiVersion: v1
kind: Pod 
metadata:
    name: client-pod
    labels:
        component: web 
spec:
    containers:
        - name: client
            image: beatrizafonso/multi-worker
            ports:
                - containerPort: 3000
```

- Salvar a imagem, e rodar:

> ~$ `kubectl apply -f client-pod.yaml`

- Para ver o status:

> ~$ `kubectl get pods`

### Infomação detalhada de um objeto:

> ~$ `kubectl describe 'object type' 'object name'`  
_ex: kubectl describe pods client-pod_

### Limitações na atualização de objetos
(204 - 205)

- 'containers', 'name' e 'port' não podem ser atualizados!

## Arquivos de configuração de deploy 
(aula 207 e 208)

- criar um arquivo que faça o deploy que criará um contêiner utilizando a imagem da porta 3000:

1. Criar uma pasta `client-deployment.yaml`:

```
apiVersion: apps/v1
kind: Deployment 
metadata:
    name: client-deployment
spec:
    replicas: 1
    selector:
        matchLbels:
            componet: web 
        template:
            metadata:
                labels:
                    component: web
            spec:
                containers:
                    - name: client
                        image: beatrizafonso/multi-client
                        ports:
                            - containerPort: 3000
```

- kind: tipo de obejto criado;
- template: é listada a configuração que será utilizada para todos os pods deste deploy;
- replicas: especifica o numero de 'pods' que o deploy deve criar;
- selector: oferece um identificador para o label

### Aplicando o Deploy 
(aula 209 - 210)

#### remover um objeto existente:

> ~$ `kubectl delete -f 'nome do arquivo'`

**1.** > `kubectl apply -f 'nome do arquivo'`

**2.** > `kubectl get deployments`

**3.** > `minikube ip`

**4.** > acessar no navegador com o codigo gerado

> ~$ `kubectl get pods -o wide`

### Escalando e mudando Deploys
(Aula 211)

Quando modificamos o 'port' na pasta de deploy, o contêiner antigo é deletado e se cria um outro no lugar.

Quando modificamos 'replicas', depois de realizar o deploy é possícel ver novos pods em execução.

Quando modificamos 'image' ao rodar o comando get deployments, podemos ver as mudanças feitas no processo.

### Atualizando a imagem do deploy
(aula 212 - 214)

**1.** fazer algumas modificações no arquivo de deploy;

- salvar o arquivo e fazer o 'apply';
- rodar minikube ip e copiar o código para acessar no navegador;

**2.** Reconstruindo a imagem:

- entrar no editor de texto da pasta 'client' > src > app.js
- fazer alguma modificação, ex: no titulo. Salvar a imagem e fazer o push para o docker hub:
> ~$ `docker build -t beatrizafonso/multi-client .`  
> ~$ `docker push beatrizafonso/multi-client`

**3.** Fazer o deploy recriar/atualizar os Pods com a ultima versao da imagem:

- se rodarmos o comando `Kubectl apply -f client-deployment.yaml` nos retorna uma resposta que a pasta não foi mudada;

**3 soluções para esse porblema:**

1. excluir manualmente cada Pod, e assim será recriado automaticamente com a ultima versçao da imagem.

**CUITADO!** um desses Pods pode ser o que atenda o tráfico da web, e assim por um momento o usuário não conseguirá acessar o app.

2. Colocar um tag em 'image' ex: 'beatrizafonso/multi-client:v1','beatrizafonso/multi-clientv2', etc

Após isso, salvar a pasta e fazer o apply. A desvantagem é que adiciona uma etapa extra no processo.

3. Usar um comando imperativo, para atualizar a versão:

> ~$ `kubectl client-deploy update_version v1`

_Melhor solução!_

#### Atualizando a versão da imagem
_(aula 215 - utilizando a terceira opção)_

Entrar na pasta client pelo terminal e rodar:

> ~$ `docker build -t beatrizfonso/multi-client:v5`

> ~$ `docker push beatrizafonos/multi-client:v5`

Depois de reconstruir e fazer o update explicado acima voltar a pasta 'simplek8s'

> ~$ `kubectl set image 'object_type'/'object_name' 'container_name'='new image'`  
_ex: kubectl set image deployment/client-deployment client=beatrizafonso/multi-client:v5_

- set: atualizar uma propriedade em um dos nossos obejtos
- image: especificação do que queremos atualizar, neste caso é a 'image'

para acessar basta rodar: `minikube ip`, copiar o código e pesquisar no navegador 'codigo':'nodePort' (ex: 192.168.99.100:31515) > pode demorar um pouco

Reconfigurar o Docker CLI para se comunicar com o docker server:

> ~$ `eval $(minikube docker-env)`  
_Só vai reconfigurar momentaneamente no terminal_ 