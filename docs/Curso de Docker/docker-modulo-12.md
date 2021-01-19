# Módulo 12 

Neste módulo será iniciado os estudo de Kubernetes.

## O que é Kubernetes?

É um programa que permite escalar o aplicativo com máquinas adicionais exacutando cada um dos contêiners da aplicação.  
Para isso é utilizada a clusteirização de aplicações: 1 ou mais nós (máquinas virtuais) controlados por um 'master'.

## Por quê usar Kubernetes?

Quando vc precisa rodar diferentes contêiners com diferentes imagens

minikube status 
kubectl cluster-info

## Gerando uma imagem 'multi-client'
(Aula 193 -)

**1.** A imagem deve estar hospedada no docker hub;   
_(aula 159 - seção 10)_

**2.** Fazer um arquivo para criar o contêiner;  

- criar um diretório 'simplek8s'
- entrar no diretório e abrir o editor de texto (code .)
- criar uma pasta 'client-pod.yaml'

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
            image: beatrizafonso/multi-client
            ports:
                - containerPort: 3000
```

**3.** Fazer um arquivo para configurar a rede.  

- no mesmo diretório do tópico acima criar um arquivo 'client-node-port.yaml'

```
apiVersion: v1
kind: Service 
metadata:
    name: client-node-port
spec:
    type: NodePort
    ports:
        - port: 3050
            targetPort: 3000
            nodePort: 31515
    selector:
        component: web
```

 ### Pod
 _(aula 197)_

 Não podemos implantar contêiners individuais, Pod é o menor coisa que podemos implantar.  
 Um Pod pode ser criado para rodar um único contêiner.

 ### Service
_(aula 198)_

Configura a rede no Kubernetes.  
- Subtipos: (especificados na pasta em 'type')
1. ClusterIP
2. NodePort
3. LoadBalancer
4. Ingress

### Acessando um contêiner em execução 
_(aula 199)_

- Criando os objetos

> ~$ `kubectl apply -f 'nome do arquivo'`

- Status do objeto 

> ~$ `kubectl get 'tipo de objeto'`  
_ex: `kubectl get pods`_

- Acessando no navegador

> ~$ `minikube ip`

_Utilizar o IP gerado para acessar no navegador_

