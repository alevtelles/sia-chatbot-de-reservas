# Funcionalidades & Mapeamento de Business APIs

O SIA atua como um orquestrador de lógica de negócio, conectando o usuário final às APIs core da empresa através de linguagem natural.

---

## 🛠️ Matriz de Funcionalidades Conversacionais

Cada intenção detectada mapeia para uma (ou mais) ações técnicas:

| Intenção | Descrição | Ação Técnica (Tool/API) |
| :--- | :--- | :--- |
| **Dúvida Institucional** | Perguntas sobre regras, documentos, etc. | `buscar_faq` (RAG Service) |
| **Cotação de Veículo** | Cálculo de preços baseado em datas e local. | `calcular_cotacao` (Pricing API) |
| **Gestão de Adicionais** | Inclusão de GPS, Cadeirinha, Proteções. | `listar_adicionais` (Addons API) |
| **Efetivar Reserva** | Confirmação e geração de ID de reserva. | `criar_reserva` (Booking API) |
| **Status de Reserva** | Verificação de agendamentos futuros. | `consultar_reserva` (Status API) |
| **Modificação/Cancel** | Alteração ou desistência da reserva. | `cancelar_reserva` (Cancellation API) |
| **Suporte Crítico** | Problemas técnicos ou reclamações. | `escalar_humano` (Escalation Queue) |

---

## 📡 Definição Técnica das APIs (Mockup Schema)

### 1. Pricing API (`POST /v1/pricing`)
**Input:**
```json
{
  "pickup_location": "GRU_AIRPORT",
  "dates": ["2025-02-01", "2025-02-05"],
  "car_category": "SUV"
}
```
**Output:**
```json
{
  "quote_id": "q_123456",
  "total_price": 850.00,
  "currency": "BRL",
  "availability": true
}
```

### 2. Booking API (`POST /v1/bookings`)
**Input:**
```json
{
  "quote_id": "q_123456",
  "customer_id": "cust_987",
  "payment_method": "CREDIT_CARD"
}
```
**Output:**
```json
{
  "booking_id": "RES-2025-9988",
  "status": "CONFIRMED",
  "voucher_url": "https://sia.rent/vouchers/..."
}
```

---

## 🛡️ Guardrails de Funcionalidade
Para garantir a integridade da operação:
1.  **Validação de Data:** O sistema bloqueia datas passadas antes mesmo de chamar a API.
2.  **Limite de Tentativas:** Proteção contra abusos no motor de preços.
3.  **Confirmação Double-Check:** Antes de efetivar qualquer reserva financeira, o agente apresenta o resumo e solicita confirmação explícita "Sim/Não".

---

[⬅ Voltar para Técnico](TECHNICAL_SOLUTIONS.md) | [Ver Blueprint de Código ⮕](../src/BLUEPRINT.md)
