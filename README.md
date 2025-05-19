FROM python:3.9
🐳 Deploy de App Flask com Docker, EKS e Terraform (Free Tier)
Este projeto faz o deploy de uma aplicação Flask em um cluster EKS (Amazon Kubernetes Service) usando Docker e Terraform, tudo dentro do AWS Free Tier.

📁 Estrutura do Projeto
aws-container-k8s/
├── app.py
├── requirements.txt
├── Dockerfile
├── deployment.yaml
├── main.tf
└── README.md

🚀 Tecnologias Utilizadas

AWS EKS (Kubernetes gerenciado)

Docker

Terraform

Amazon ECR

Python + Flask

⚙️ Pré-requisitos
Conta AWS com Free Tier ativo

AWS CLI configurado (aws configure)

Docker instalado e funcionando

Terraform instalado

kubectl instalado

📦 1. Build e Push da Imagem para o ECR
# Build da imagem
docker build -t vini1321-eks-repo .

# Login no ECR
aws ecr get-login-password --region sa-east-1 | docker login --username AWS --password-stdin <SEU_ID>.dkr.ecr.sa-east-1.amazonaws.com

# Tag e push
docker tag vini1321-eks-repo:latest <SEU_ID>.dkr.ecr.sa-east-1.amazonaws.com/vini1321-eks-repo:latest
docker push <SEU_ID>.dkr.ecr.sa-east-1.amazonaws.com/vini1321-eks-repo:latest

🌐 2. Criar infraestrutura com Terraform
terraform init
terraform apply

☸️ 3. Conectar ao Cluster EKS
aws eks --region sa-east-1 update-kubeconfig --name vini1321-eks-cluster

📥 4. Aplicar o deployment no Kubernetes
kubectl apply -f deployment.yaml

🌍 5. Acessar aplicação
Após aplicar, rode:
kubectl get svc
Quando o campo EXTERNAL-IP do serviço hello-service estiver disponível, acesse via navegador:
http://EXTERNAL-IP

📌 Observações
As subnets foram configuradas com map_public_ip_on_launch = true para permitir acesso externo.
O projeto usa apenas recursos do Free Tier.

Repositório do Projeto: https://github.com/viniciushrq-dev/aws-container-k8s
