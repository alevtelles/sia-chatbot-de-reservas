# Recovery e Idempotência

Em sistemas de locação (SIA), falhas transacionais podem causar prejuízos financeiros ou insatisfação crítica.

## 🔄 Estados de Recovery (LangGraph)
Nossa arquitetura utiliza grafos de estado com persistência:

- **Checkpointing:** O estado da conversa é salvo após cada interação. Se o sistema cair, ele retoma exatamente de onde parou.
- **Node Rollback:** Se um nó (ex: `BookingNode`) falhar na API externa, o grafo transiciona para um `RecoveryNode` que:
  - Tenta uma estratégia alternativa.
  - Ou solicita intervenção humana (Handoff).
  - Ou desfaz ações parciais (Saga Pattern).

## 🔑 Idempotência Explícita
Para evitar cobranças ou reservas duplicadas:

1.  **X-Idempotency-Key:** Todas as chamadas POST/PATCH devem incluir uma chave única no cabeçalho.
2.  **Storage:** Usamos Redis (TTL de 24h) para armazenar os resultados das chaves processadas.
3.  **Middleware Logic:**
    - Se a chave já existe e o processo terminou: retorna o resultado em cache.
    - Se a chave está "In Progress": retorna 409 Conflict.
    - Se a chave é nova: processa e salva.

---
[⬅ Voltar para Início](../README.md)
