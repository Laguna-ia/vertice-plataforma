# ADR-021 — Região da inferência do assistente

| Campo | Valor |
|---|---|
| Status | Aceita |
| Data | 22/06/2026 |
| Autores | Otávio Rangel, Paulo Nogueira, Lívia Monteiro |
| Classificação | **Interno** |

> Simulação — dados sintéticos para treinamento.

## Contexto
Clientes Enterprise perguntam se todo o processamento ocorre no Brasil. Os modelos de linguagem usados pelo assistente não estão disponíveis, com a qualidade necessária, em região brasileira.

## Decisão
- Manter a inferência nos Estados Unidos, com contrato de **retenção zero** e **proibição de treinamento** no provedor.
- Enviar ao modelo apenas os trechos necessários à tarefa.
- Cobrir a transferência internacional no DPA.
- Reavaliar quando houver modelo equivalente em região brasileira. **Não há data** para essa reavaliação.

## Consequências
- Clientes que exigem processamento 100% no Brasil podem usar a Vértice com o assistente desligado (memória da conta e CRM continuam no Brasil), perdendo briefing e sugestões.
