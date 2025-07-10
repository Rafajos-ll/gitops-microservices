# 🚀 Projeto GitOps na Prática com Kubernetes

Este projeto foi desenvolvido como parte do Programa de Bolsas - DevSecOps e tem como objetivo aplicar práticas modernas de entrega contínua usando GitOps em um ambiente Kubernetes local. Utilizamos ferramentas como Rancher Desktop, ArgoCD, e o repositório de microserviços da **Online Boutique**.

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

- Realizei o fork do repositório oficial:
  [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo)
- Criei um novo repositório com apenas o arquivo `release/kubernetes-manifests.yaml`
- Estrutura utilizada:
 gitops-microservices/  
  └── k8s/ 
   └── online-boutique.yaml 
   