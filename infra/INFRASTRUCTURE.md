# Infraestrutura como Código (IaC)

Esta pasta contém as definições de infraestrutura para o SIA, seguindo os padrões enterprise da AWS.

---

## 🛠️ Stack de Infraestrutura

1.  **Terraform:** Provedor principal para gerenciamento de recursos (VPC, RDS, EKS).
2.  **Helm:** Para deploy de aplicações dentro do Kubernetes.
3.  **ArgoCD:** Para automação GitOps.

---

## 🏗️ Estrutura de Arquivos Proposta

```text
/infra
├── terraform/
│   ├── main.tf             # Definição principal (Providers, Region)
│   ├── vpc.tf              # Rede isolada, Subnets, Gateways
│   ├── eks.tf              # Cluster Kubernetes Amazon EKS
│   ├── rds_postgresql.tf   # Banco de dados com pgvector
│   ├── redis.tf            # Cache e Session management
│   └── iam_roles.tf        # Permissões de segurança para pods
├── kubernetes/
│   ├── manifests/
│   │   ├── api-deployment.yaml
│   │   ├── rag-deployment.yaml
│   │   └── hpa-autoscaling.yaml
│   └── helm/
│       └── sia-app/        # Chart customizado para deploy simplificado
└── scripts/
    ├── setup_cluster.sh    # Script de bootstrapping
    └── seed_database.sql   # Inicialização de tabelas e vetores
```

---

## 🛡️ Segurança de Infra
- **Private Subnets:** O banco de dados e pods não têm IP público.
- **KMS:** Todas as secrets e dados em repouso são criptografados.
- **Security Groups:** Tráfego permitido apenas nas portas estritamente necessárias.

---
[⬅ Voltar para Início](../README.md)
