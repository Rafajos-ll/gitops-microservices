# 🚀 Projeto GitOps na Prática com Kubernetes

Este projeto foi desenvolvido para afiar nossas habilidades e tem como objetivo aplicar práticas modernas de entrega contínua usando GitOps em um ambiente Kubernetes local. Utilizamos ferramentas como Rancher Desktop, ArgoCD, e o repositório de microserviços da **Online Boutique**.

## 🎯 Objetivo

Implantar um conjunto de microserviços (Online Boutique) em Kubernetes local usando GitOps com ArgoCD, a partir de um repositório público hospedado no GitHub.

---

## 🛠️ Pré-requisitos

- ✅ Rancher Desktop instalado (com Kubernetes habilitado)
- ✅ Kubectl configurado e funcional
- ✅ ArgoCD instalado no cluster
- ✅ Conta no GitHub com repositório público
- ✅ Git instalado
- ✅ Docker funcional localmente

---

## 📂 Etapas do Projeto

### 1️⃣ Fork e estrutura do repositório GitHub

- Realize o fork do repositório oficial:
  [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo)
- Crie um novo repositório com apenas o arquivo `release/kubernetes-manifests.yaml`
- Estrutura utilizada:
 gitops-microservices/  
  └── k8s/ 
   └── online-boutique.yaml 


### 2️⃣ Instalação do ArgoCD no cluster Kubernetes

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```

### 3️⃣ Acesso à interface web do ArgoCD
 
 - Faremos o port-forward para acesso local:

 ```bash
 kubectl port-forward svc/argocd-server -n argocd 8080:443

 ```
- Interface acessada via: https://localhost:8080

- Usuário e senha padrões utilizados para login.

🔎 A senha inicial do usuário admin está armazenada como um secret no namespace argocd. Para obtê-la, basta rodar:

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```

- Esse comando retorna a senha em texto plano. Depois do primeiro login, é recomendável trocá-la diretamente pela interface web ou via CLI.

### 4️⃣ Criação do App no ArgoCD Para implantar os microserviços da Online Boutique via GitOps, criei um novo App diretamente na interface web do ArgoCD. Eis os passos essenciais:

1.Clique em "NEW APP" na interface principal.

2.Preencha os campos da seguinte forma:

- Application Name: online-boutique

- Project: default

- Sync Policy: manual (ou automática, conforme desejado)

- Repository URL: URL do repositório Git com os manifests

- Revision: HEAD

- Path: caminho para o arquivo YAML (ex: k8s)

- Cluster URL: https://kubernetes.default.svc

- Namespace: default

3.Após configurar, clique em Create.

4.Com o App criado, clique em Sync para iniciar o deploy dos microserviços no cluster.

- ✅ O ArgoCD lê os arquivos diretamente do GitHub e aplica as configurações no Kubernetes automaticamente — garantindo rastreabilidade e controle via GitOps.

### 5️⃣ Acesse o front-end da aplicação, o serviço front-end é do tipo ClusterIP, então utilize:

```bash
kubectl port-forward svc/frontend -n default 8081:80
```
- 🧩 Ajuste no Número de Réplicas dos Microserviços Após o deploy inicial, é possível personalizar a quantidade de réplicas de cada serviço para testar escalabilidade ou distribuir melhor o tráfego.
 
✍️ Exemplo: alterar réplicas do ''productcatalogservice''
 
 1.No arquivo YAML:

 ```yaml
 apiVersion: apps/v1
kind: Deployment
metadata:
  name: productcatalogservice
spec:
  replicas: 3  # Altere este valor conforme desejado
  ...
```

-📌 Etapas para aplicar a alteração,edite o manifest .yaml no seu repositório Git.

2.Faça o commit e o push:

```bash
git add .
git commit -m "Ajuste: aumentar réplicas para productcatalogservice"
git push origin main
```

3.Acesse o ArgoCD e clique em Refresh ou aguarde a sincronização automática.

4.Verifique os novos pods:
 
```bash
kubectl get pods | grep productcatalogservice
```

📦 Entregas Realizadas:

- ✅ Repositório Git público com estrutura de manifests

- ✅ Deploy completo do ArgoCD

- ✅ App criado e sincronizado com sucesso no ArgoCD

- ✅ Verificação de pods em execução

- ✅ Acesso ao front-end da aplicação

- ✅ Ajuste opcional no número de réplicas de microserviços