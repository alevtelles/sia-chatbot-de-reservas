# Soluções Técnicas & Arquitetura de Software

O SIA foi construído sob princípios de **Resiliência**, **Segurança** e **Performance**. Abaixo detalhamos as soluções que tornam esta arquitetura 10/10.

---

## 🧠 Estratégia de IA & RAG

### 1. Multi-Agent Orchestration (Supervisor Pattern)
O sistema não é um monólito de IA. Ele utiliza múltiplos agentes especializados coordenados por um Supervisor. Isso garante que o agente de cobrança nunca interfira na lógica do agente de RAG, permitindo prompts menores e mais focados.

### 2. Multi-Provider Fallback
Não dependemos de um único fornecedor. Utilizamos o **Amazon Bedrock** como gateway, permitindo alternar entre modelos em tempo real baseados em custo, latência ou falha.

### 2. Pipeline RAG (Retrieval Augmented Generation)
Para garantir que a IA fale apenas a "verdade" da empresa:
- **Indexação:** Documentos (PDF/MD) são "quebrados" em chunks semânticos.
- **Embeddings:** Modelos de alta dimensão (Cohere/Titan) convertem texto em vetores.
- **Reranking:** Uma segunda camada de IA re-avalia os top resultados para garantir máxima relevância antes da resposta.

---

## 🛡️ Camadas de Segurança (Defense in Depth)

| Camada | Tecnologia | Função |
| :--- | :--- | :--- |
| **Perímetro** | AWS WAF + Shield | Proteção contra DDoS e SQL Injection. |
| **Identidade** | Amazon Cognito | Autenticação via JWT e controle de MFA. |
| **App Guardrails** | Python Logic | Regex e LLM-check para detectar "Prompt Injection". |
| **Dados** | PostgreSQL RLS | Row Level Security garante que um tenant nunca veja dados de outro. |
| **Audit Log** | TimescaleDB | Logs imutáveis para conformidade LGPD. |

---

## 🏢 Arquitetura Multi-Tenant
O sistema é **White-label nativo**. Uma única instância atende múltiplas marcas:
- **Shared Cluster:** O processamento é compartilhado para otimização de custo.
- **Isolated Data:** Filtros de `tenant_id` em nível de banco de dados e namespaces no cache.
- **Persona Config:** Cada marca tem seu tom de voz e regras de negócio carregadas dinamicamente via `config_table`.

---

## ⚡ Otimização de Performance & Custos

1.  **Cache Semântico:** Perguntas similares não geram novas chamadas de LLM. O Redis armazena o "sentido" da pergunta e a resposta gerada anteriormente.
2.  **Tiered Logic:** Perguntas simples (Ex: "Oi") são classificadas por modelos ultraleves (300ms) para economizar processamento caro.
3.  **Batch Jobs:** Atualização da base de conhecimento ocorre de forma assíncrona, não impactando a API em runtime.

---

[⬅ Voltar para Fluxo](FLOW.md) | [Ver Funcionalidades & APIs ⮕](FUNCTIONALITIES.md)
