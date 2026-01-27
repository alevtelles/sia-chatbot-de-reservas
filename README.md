# SIA - Chatbot de Reservas com IA Generativa

## 🚀 Visão Geral

O **SIA (Sistema de Inteligência para Atendimento)** é uma plataforma enterprise de locação de veículos que utiliza IA Generativa para automatizar o ciclo completo de reservas. Ele resolve o gargalo de atendimento humano em tarefas repetitivas, garantindo precisão determinística em operações financeiras e flexibilidade natural na interação com o usuário.

![Arquitetura do SIA](assets/sia.png)

#### [Baixar PDF](assets/sia_arquitetura.pdf)

---

## 🎯 Problemas que o SIA Resolve (A Ponte)

O SIA não é apenas um chatbot; é uma solução estratégica para 5 pilares críticos do setor de locação:

1.  **Eliminação do Gargalo de Atendimento Humano:**
    Automatiza tarefas repetitivas (cotações, FAQ, disponibilidade), liberando a equipe de suporte para focar em casos complexos de alto valor, reduzindo drasticamente o tempo de espera do cliente.

2.  **Redução de Atrito no Ciclo de Reserva:**
    Substitui formulários extensos e menus complexos por uma conversa natural e fluida. O cliente pode cotar e reservar em instantes via WhatsApp ou Web, aumentando as taxas de conversão (Conversational Commerce).

3.  **Precisão Determinística vs. Alucinação de IA:**
    Chatbots comuns falham em tarefas financeiras. O SIA utiliza uma arquitetura que separa a "criatividade" da IA da "rigidez" das APIs de negócio, garantindo que preços e reservas sejam sempre exatos e baseados em dados reais.

4.  **Eficiência para Grupos Multi-Marca (White-label):**
    Resolve a fragmentação sistêmica de grandes grupos. Uma única arquitetura atende múltiplas marcas, mantendo identidades visuais, tons de voz, regras de negócio e dados de clientes totalmente isolados e seguros.

5.  **Modernização de Sistemas Legados:**
    Atua como uma camada de inteligência sobre sistemas de frota antigos. Ele conecta o usuário final a tecnologias complexas através de linguagem simples, sem a necessidade de reescrever todo o core business da empresa.

---

## 🏗️ Stacks & Plataformas

### Core Infra

- **Cloud:** AWS (Enterprise Ready)
- **Orquestração:** Kubernetes (Amazon EKS)
- **Database:** PostgreSQL 16 + `pgvector` (HNSW indexing)
- **Cache:** Redis Cluster (Sessão & Cache Semântico)

### AI & Intelligence

- **LLM Backbone:** Amazon Bedrock (Multi-provider: Claude 3.5, Llama 3.1)
- **Orchestration:** LangGraph (Agente de Estado Determinístico)
- **RAG:** Custom Pipeline com Reranker (Cohere/Voyage AI)

### Backend

- **Framework:** Python 3.11 + FastAPI
- **Security:** AWS WAF + Cognito + Guardrails Customizados

---

## 📈 Funcionalidades Chave

- **Cotações Dinâmicas:** Cálculo preciso via APIs determinísticas.
- **RAG Service:** Esclarecimento de dúvidas sobre políticas e termos.
- **Gestão de Reservas:** Criação, consulta e cancelamento 100% via chat.
- **Multi-tenant:** Arquitetura White-label para múltiplas marcas de locação.
- **Escalação Humana:** Hand-off inteligente para atendentes via Zendesk/SQS.

---

## 📂 Estrutura do Projeto

- [/docs](docs/): Detalhamento técnico, fluxos, segurança e [Multi-Agentes](docs/MULTI_AGENT.md).
- [/infra](infra/): Blueprints de infraestrutura (IaC).
- [/src](src/): Arquitetura de código e boilerplate.

---

[Saiba mais sobre o Fluxo de Atendimento ⮕](docs/FLOW.md)
