# ADR-024 — SSO SAML antes de SCIM

| Campo | Valor |
|---|---|
| Status | Aceita |
| Data | 28/07/2026 |
| Autores | Helena Duarte, Paulo Nogueira |
| Classificação | **Interno** |

> Simulação — dados sintéticos para treinamento.

## Contexto
Clientes Enterprise com Microsoft Entra pediram login único e controle de quem acessa.

## Decisão
- Entregar primeiro **SAML 2.0 com provisionamento no primeiro login (JIT)**, liberado como beta em v4.9 e GA em v4.11.
- **SCIM 2.0** (provisionamento e desprovisionamento automáticos) fica para depois, em desenvolvimento, sem data.

## Consequências
- Sem SCIM, remover um usuário no IdP bloqueia novos logins, mas não encerra sessões abertas. Procedimento recomendado: desativar o usuário também na Vértice.
