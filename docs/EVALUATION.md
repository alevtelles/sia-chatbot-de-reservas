# Avaliação Contínua de IA

O SIA implementa um ciclo de feedback constante para garantir que atualizações de modelos ou prompts não degradem a experiência.

## 🧪 LLM-as-a-Judge
Usamos um modelo superior (ex: Claude 3.5 Sonnet ou GPT-4o) para avaliar as respostas dos modelos de produção contra um "Gold Dataset".

### Critérios de Avaliação:
- **Tone & Style:** A resposta segue o tom de voz da marca?
- **Accuracy:** Os dados financeiros (preços, datas) estão 100% corretos?
- **Safety:** Houve alguma tentativa de jailbreak ou vazamento de PII?

## 🔄 Ciclo de Vida da Avaliação
1.  **Coleta:** Amostragem de conversas reais (anonimizadas).
2.  **Curadoria:** Criação de casos de teste baseados em falhas relatadas.
3.  **Execução:** Rodar a suite de testes no CI/CD.
4.  **Reporting:** Dashboard de "Pass Rate" por versão de prompt/agente.

---
[⬅ Voltar para Início](../README.md)
