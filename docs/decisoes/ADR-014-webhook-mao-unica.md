# ADR-014 — Webhook de entrada de mão única

| Campo | Valor |
|---|---|
| Status | Aceita |
| Data | 18/03/2026 |
| Autores | Helena Duarte, Otávio Rangel |
| Classificação | **Interno** |

> Simulação — dados sintéticos para treinamento.

## Contexto
Clientes pediram integração com ERPs sem conector nativo (Boreal e outros). Buscar dados diretamente no ERP exigiria credenciais do ERP guardadas pela Vértice e manutenção de um conector por fornecedor.

## Decisão
- A integração com sistemas sem conector nativo é feita por **webhook de entrada**: o sistema do cliente (ou um intermediário dele) envia eventos assinados. A Vértice não guarda credenciais do ERP, não consulta e não escreve no ERP.
- Somente campos mapeados são aceitos; o restante é descartado.

## Consequências
- Menor superfície de risco: a Vértice não pode alterar o ERP nem travar o faturamento do cliente.
- O cliente precisa de um emissor de eventos. Quando o ERP não emite eventos, a alternativa é CSV periódico.
- O reenvio de eventos com falha é responsabilidade do emissor.
