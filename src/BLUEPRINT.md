# Blueprint de Código (Arquitetura de Software)

Esta seção descreve como o código-fonte deve ser organizado para suportar a escala e a modularidade do SIA.

---

## 🗄️ Estrutura de Diretórios Proposta

```text
/src
├── main.py                 # Entrypoint FastAPI
├── core/
│   ├── config.py           # Variáveis de ambiente e settings
│   ├── security.py         # Lógica de Guardrails e Cognito
│   └── database.py         # Conexão SQLAlchemy/pgvector
├── agents/                 # Multi-Agent Logic
│   ├── supervisor.py       # Agente Supervisor (Router)
│   ├── policy_agent.py     # Guardian/Validator layer
│   ├── rag_agent.py        # Especialista em Dúvidas/FAQ
│   ├── pricing_agent.py    # Especialista em Cotações
│   └── booking_agent.py    # Especialista em Transações
├── services/
│   ├── rag_service.py      # Lógica de Busca Vetorial (c/ Observabilidade)
│   ├── api_service.py      # Abstração de chamadas para APIs externas
│   ├── recovery_service.py # Lógica de rollback e transações
│   ├── audit_service.py    # Log imutável em TimescaleDB
│   └── eval_service.py     # Continuous Evaluation (LLM-as-a-Judge)
├── core/
│   ├── config.py           # Variáveis de ambiente e settings
│   ├── security.py         # Lógica de Guardrails e Cognito
│   ├── idempotency.py      # Middleware de X-Idempotency-Key
│   └── database.py         # Conexão SQLAlchemy/pgvector
├── middleware/
│   └── idempotency.py      # FastAPI middleware para idempotência
├── schema/
│   ├── pydantic_models.py  # Modelos de dados para validação
│   └── events.py           # Definição de eventos SQS
└── utils/
    ├── observability.py    # OpenTelemetry/LangSmith Tracing
    ├── prompts.py          # Catálogo de Prompts Versionados
    └── formatters.py       # Formatação de preços e datas
```

---

## 🛠️ Tecnologias Recomendadas (Implementação)

1.  **FastAPI:** Pela sua alta performance assíncrona (`async/await`) nativa.
2.  **LangGraph:** Para ciclos e persistência de conversa (Checkpointing).
3.  **LiteLLM:** Como proxy unificado para múltiplos modelos de IA.
4.  **Pydantic v2:** Validação rigorosa de inputs/outputs.
5.  **Pytest:** Suite de testes automatizados com mocks de LLM.

---

## 🚀 Padrão de Design: "The Clean Orchestrator"
A lógica do agente não deve estar espalhada. Seguimos o padrão onde:
- O **Orchestrator** decide *o que* fazer (IA).
- Os **Services** sabem *como* fazer (Código Determinístico).
- Os **Guardrails** garantem que seja feito de forma *segura*.

> [!NOTE]
> **Aceleração:** Esta estrutura permite que novos canais (WhatsApp, Voice, Web) sejam plugados no `main.py` sem alterar a lógica do agente.

---

[⬅ Voltar para Documentação](../docs/FUNCTIONALITIES.md) | [Ver Início](../README.md)
