# Changelog — Vértice Plataforma

> Simulação — dados sintéticos para treinamento. Datas no fuso America/Sao_Paulo.
> Responsável: Engenharia de Plataforma. Status: GA, beta (feature flag), desenvolvimento.

## v4.12 — planejada para 03/11/2026 (sem compromisso de data)
- Planejado: consentimento por administrador Microsoft 365 passa de beta para GA.
- Planejado: registro de visualização ("quem viu o quê") passa de beta para GA, com retenção de 12 meses.
- Itens planejados não são promessa e podem mudar de versão.

## v4.11.2 — 14/10/2026
- Correção: renovação de token Microsoft 365 falhava para usuários com política de acesso condicional que exige dispositivo gerenciado. Agora a conexão é marcada como "erro" com mensagem clara ao administrador.
- Correção: recibos de webhook exportados em CSV mostravam horário em UTC sem indicação.

## v4.11.0 — 05/10/2026
- **GA:** SSO SAML 2.0 (Microsoft Entra ID, Okta, Google Workspace) no plano Enterprise, com provisionamento no primeiro login (JIT) e opção de SSO obrigatório.
- **Beta:** registro de visualização de registros (`audit.record_view_log`), desligado por padrão, Enterprise, retenção de 90 dias.
- Novo: alerta ao administrador quando a taxa de rejeição de webhook passa de 5% em 1 hora.
- Testes de injeção de instruções no assistente ampliados para 140 casos.

## v4.10.0 — 08/09/2026
- **Beta:** consentimento por administrador do tenant Microsoft 365 (`m365.admin_consent`), Enterprise, combinado com atribuição de usuários no Entra.
- Novo: filtros de coleta por pasta e domínio no Microsoft 365.
- Novo: reversão de importação CSV em até 7 dias.

## v4.9.0 — 11/08/2026
- **Beta:** SSO SAML 2.0 para clientes Enterprise selecionados.
- Novo: rotação de segredo de webhook com convivência de 24 h.

## v4.8.0 — 14/07/2026
- Novo: webhook de saída (Enterprise).
- Novo: objetos personalizados (ex.: "contrato") na importação CSV e no webhook de entrada.

## v4.7.0 — 09/06/2026
- Novo: assinatura HMAC-SHA256 obrigatória no webhook de entrada (antes opcional). Fontes antigas tiveram 30 dias para migrar.
- Novo: recibos de webhook visíveis ao administrador.

## v4.6.0 — 12/05/2026
- Novo: MFA obrigatório configurável pelo administrador.
- Teste de intrusão externo anual concluído (ver docs/seguranca/certificacoes-e-testes.md).
