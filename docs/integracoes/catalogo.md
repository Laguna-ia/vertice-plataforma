# Catálogo de integrações — status por capacidade

| Campo | Valor |
|---|---|
| Responsável | Otávio Rangel (Produto) |
| Versão do documento | 2.4 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 14/10/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

| Integração / capacidade | Status | Planos | Direção do dado | Documento |
|---|---|---|---|---|
| Gmail (e-mail) | GA | Crescimento, Enterprise | Leitura | — |
| Microsoft 365 — e-mail (Outlook) | GA | Crescimento, Enterprise | Leitura | `microsoft-365.md` |
| Microsoft 365 — calendário | GA | Crescimento, Enterprise | Leitura | `microsoft-365.md` |
| Microsoft 365 — consentimento por administrador do tenant | **Beta** (desde v4.10) | Enterprise | — | `microsoft-365.md` §4 |
| Microsoft Teams — transcrições de reunião | **Planejado** | — | — | — |
| Google Calendar | GA | Crescimento, Enterprise | Leitura | — |
| Importação CSV (upload manual) | GA | Todos | Entrada | `importacao-csv.md` |
| Importação CSV agendada via SFTP | **Em desenvolvimento** | — | Entrada | `importacao-csv.md` §5 |
| Exportação CSV | GA | Todos | Saída (download) | `importacao-csv.md` |
| Webhook de entrada | GA | Crescimento, Enterprise | Entrada | `webhook-generico.md` |
| Webhook de saída (eventos da Vértice) | GA | Enterprise | Saída, para URL do cliente | `webhook-generico.md` §6 |
| API REST de leitura | GA | Enterprise | Saída (consulta) | — |
| Conector ERP Boreal | **Não suportado** (sem conector nativo; avaliação caso a caso via webhook/CSV) | — | — | `webhook-generico.md` §8 |
| Aplicativos de mensagem (WhatsApp etc.) | **Não suportado** | — | — | — |

## Observações

- "Nativa" significa conector pronto, ativado pela autorização do usuário. Webhook e CSV **não** são conectores prontos: dependem de desenho de campos e, no caso do webhook, de um emissor do lado do cliente.
- O catálogo descreve o produto. Se uma integração está **incluída** em um contrato é definido pela proposta e pelo contrato.
