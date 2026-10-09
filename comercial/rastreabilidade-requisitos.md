# Rastreabilidade: requisitos comuns de clientes → capacidades → evidência

| Campo | Valor |
|---|---|
| Responsável | Otávio Rangel (Produto) |
| Versão do documento | 1.1 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 14/10/2026 |
| Classificação | **Interno** |

> Simulação — dados sintéticos para treinamento.

| Requisito típico do cliente | Capacidade | Status | Evidência técnica | Liberado por |
|---|---|---|---|---|
| "Quero login único com Entra" | SSO SAML 2.0 | GA (Enterprise) | `docs/seguranca/autenticacao-sso.md`; CHANGELOG v4.11.0 | `sso.saml` (default ligado no Enterprise) |
| "Só usuários autorizados pela TI podem conectar o e-mail" | Consentimento por administrador + atribuição de usuários no Entra | Beta (Enterprise) | `docs/integracoes/microsoft-365.md` §4 | `m365.admin_consent` (desligado por padrão) |
| "Quero desligar o acesso de quem sair" | Desativação no IdP + na Vértice | GA; SCIM em desenvolvimento | `autenticacao-sso.md` §2; ADR-024 | — |
| "Log de quem conectou o quê" | Auditoria de conexões | GA | `docs/seguranca/auditoria-e-logs.md` §1 | — |
| "Log de quem viu o quê" | Registro de visualização | Beta (Enterprise), 90 dias | `auditoria-e-logs.md` §1 e §5 | `audit.record_view_log` (desligado por padrão) |
| "Mandar logs para o nosso SIEM" | Exportação CSV manual; streaming planejado | Parcial | `auditoria-e-logs.md` §3 | — |
| "Dados no Brasil" | Hospedagem e backups em São Paulo; inferência nos EUA | Parcial | `docs/arquitetura/visao-geral.md` §2; ADR-021 | — |
| "Integração com nosso ERP sem conector" | Webhook de entrada ou CSV | GA (mecanismo); escopo caso a caso | `docs/integracoes/webhook-generico.md`; ADR-014 | `webhook.inbound` |
| "A integração não pode afetar o ERP" | Webhook de mão única | GA | ADR-014; `webhook-generico.md` §4 | — |
| "Esconder valor do contrato de alguns usuários" | Restrição por campo | **Não suportado**; alternativa: não enviar o campo | `docs/seguranca/permissoes.md` §3 | — |
| "Importação automática diária" | CSV via SFTP | Em desenvolvimento | `docs/integracoes/importacao-csv.md` §5 | `csv.sftp_scheduled_import` |
| "Desligar a integração rapidamente" | Desconectar todos (M365); desativar fonte (webhook) | GA | `microsoft-365.md` §5; `webhook-generico.md` §3 | — |
| "A IA não pode ser manipulada por texto nos dados" | Conteúdo tratado como dado; sem escrita direta | GA | `docs/seguranca/ia-e-tratamento-de-conteudo.md` §2 | — |
