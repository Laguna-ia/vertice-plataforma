# Integração Microsoft 365 (e-mail e calendário)

| Campo | Valor |
|---|---|
| Responsável | Helena Duarte (Engenharia de Plataforma) |
| Versão do documento | 2.1 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 14/10/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

## 1. O que a integração faz

- Lê e-mails (Outlook) e eventos de calendário das **caixas autorizadas** e os associa às contas e contatos do CRM.
- Alimenta a memória da conta e o briefing, sempre com a origem visível (remetente, data, assunto).
- Busca incremental a cada 10 minutos. Na primeira conexão, importa os últimos **12 meses** de e-mails e eventos (configurável pelo administrador entre 3 e 24 meses).

## 2. O que a integração não faz

- Não envia e-mails, não responde, não cria nem altera eventos.
- Não lê arquivos do OneDrive/SharePoint nem chats do Teams.
- Não lê transcrições de reuniões do Teams (planejado, sem data).
- Não lê caixas compartilhadas, a menos que um usuário com acesso a ela conecte explicitamente.

## 3. Permissões solicitadas (Microsoft Graph, delegadas)

Fonte: `config/integracoes/microsoft365.yaml`.

| Permissão | Para quê |
|---|---|
| `User.Read` | Identificar o usuário conectado |
| `Mail.Read` | Ler e-mails da caixa do usuário |
| `Calendars.Read` | Ler eventos do calendário do usuário |
| `offline_access` | Manter a conexão sem novo login a cada busca |

Todas as permissões são **delegadas e de leitura**. A Vértice não solicita permissões de aplicativo (application permissions), nem `Mail.Send`, `Mail.ReadWrite` ou `Calendars.ReadWrite`.

### Filtros de privacidade
- O administrador pode excluir pastas (ex.: "Pessoal", "RH") e domínios (ex.: e-mails internos `@empresa`) da coleta.
- E-mails marcados como "Particular" (sensitivity = private) no Outlook são ignorados por padrão.

## 4. Modos de autorização

| Modo | Como funciona | Status | Planos |
|---|---|---|---|
| **Por usuário** | Cada usuário conecta a própria caixa e aceita as permissões. | GA | Crescimento, Enterprise |
| **Consentimento por administrador do tenant** | Um administrador global do Entra concede o consentimento em nome da organização. Combinado com a opção "atribuição de usuário obrigatória" do aplicativo empresarial no Entra, **só os usuários ou grupos atribuídos pelo administrador conseguem conectar**. Cada usuário ainda precisa clicar em "Conectar" na Vértice, mas não vê a tela de consentimento. | **Beta** desde v4.10 (08/09/2026). Feature flag `m365.admin_consent`. GA planejado para v4.12. | Enterprise |

Notas sobre o consentimento por administrador:
- A lista de usuários permitidos é **gerida no Entra** (atribuição de usuários e grupos ao aplicativo), não na Vértice.
- Uma lista de permissão gerida dentro da Vértice está **planejada**, sem data.
- Em beta, a ativação é feita por Engenharia a pedido de Produto, por cliente.

## 5. Revogação e desligamento

- O usuário pode desconectar a própria caixa a qualquer momento (efeito imediato; tokens apagados).
- O administrador da Vértice pode desconectar todas as caixas de uma vez em **Administração › Integrações › Microsoft 365 › Desconectar todos**.
- O administrador do Entra pode revogar o consentimento ou remover o aplicativo empresarial; a próxima busca falha e a conexão é marcada como "revogada".
- Dados já coletados permanecem na memória da conta até exclusão (ver `docs/seguranca/dados-retencao-exclusao.md`).

## 6. Registros

- Conexão, desconexão, renovação de token e revogação geram eventos de auditoria (ver `docs/seguranca/auditoria-e-logs.md`).

## 7. Pré-requisitos do cliente

- Contas corporativas do Microsoft 365 (contas pessoais não são suportadas).
- Para consentimento por administrador: administrador global ou administrador de aplicativos de nuvem do Entra disponível na implantação.
- Liberação do domínio `*.vertice.example` em políticas de acesso condicional, quando houver.
