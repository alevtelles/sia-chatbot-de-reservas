# Observabilidade de RAG

Para garantir um sistema 10/10, a busca vetorial (RAG) não pode ser uma "caixa preta". Precisamos de métricas claras de performance e qualidade.

## 🛠️ Stack Recomendada
- **LangSmith / Arize Phoenix:** Rastreamento de traces e spans de LLM.
- **OpenTelemetry:** Para exportação de métricas customizadas para CloudWatch/Datadog.

## 📈 Métricas de Qualidade (RAG Triad)

1.  **Context Relevance (Recall):**
    - O contexto recuperado realmente contém a resposta para a pergunta do usuário?
2.  **Groundedness (Faithfulness):**
    - A resposta gerada pela IA é baseada *apenas* no contexto fornecido (sem alucinações)?
3.  **Answer Relevance:**
    - A resposta atende diretamente à necessidade do usuário?

## 🔍 Tracing de Pipeline
Cada requisição de RAG deve registrar:
- `retrieval_latency`: Tempo de busca no banco vetorial.
- `top_k_documents`: Lista de documentos recuperados.
- `reranker_score`: Score de relevância após o reranking.
- `token_usage`: Custo da requisição.

---
[⬅ Voltar para Início](../README.md)
