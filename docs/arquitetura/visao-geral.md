# Arquitetura da plataforma Vértice — visão geral

| Campo | Valor |
|---|---|
| Responsável | Helena Duarte (Engenharia de Plataforma) |
| Versão do documento | 3.2 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 12/10/2026 |
| Classificação | **Interno** (trechos marcados com [C] são compartilháveis com cliente) |

> Simulação — dados sintéticos para treinamento.

## 1. Componentes

| Componente | Responsabilidade | Dados que manipula |
|---|---|---|
| **app-web** | Interface do usuário (navegador). Não guarda dados localmente além da sessão. | Sessão do usuário |
| **api-gateway** | Ponto único de entrada da API e dos webhooks. Autenticação, limite de requisições, assinatura de webhooks. | Requisições, tokens de sessão |
| **identidade** | Login próprio (e-mail + senha + MFA), SSO SAML 2.0, papéis e permissões. | Usuários, papéis, grupos |
| **conectores** | Conexões nativas com Gmail, Microsoft 365 e Google Calendar. Busca periódica de e-mails e eventos autorizados. | Tokens OAuth (cifrados), metadados e corpo de e-mails, eventos de agenda |
| **ingestao** | Recebe webhooks e arquivos CSV, valida, normaliza e grava. Mantém o registro de recebimento. | Payloads de webhook, arquivos CSV, recibos |
| **memoria-da-conta** | Linha do tempo da conta: contatos, reuniões, e-mails, atividades, oportunidades e campos importados. | Dados do CRM |
| **assistente** | Briefing, sugestão de próximo passo, atualização assistida e handoff. Chama o provedor de modelo de linguagem. | Trechos da memória da conta enviados para inferência |
| **auditoria** | Registro de eventos administrativos, de conexão e de acesso. | Logs de auditoria |
| **notificacoes** | E-mails transacionais (convites, alertas). | Endereços de e-mail, conteúdo do aviso |

## 2. Hospedagem e localização [C]

- Toda a aplicação, bancos de dados, armazenamento de arquivos e backups ficam em **nuvem pública, região São Paulo (Brasil)**, em duas zonas de disponibilidade.
- **Exceção:** a inferência do assistente (briefing, próximo passo, atualização assistida) é feita por um **provedor de modelo de linguagem com processamento nos Estados Unidos**. Apenas os trechos necessários para a tarefa são enviados, por conexão cifrada. O contrato com o provedor prevê **retenção zero** (o provedor não armazena entradas nem saídas após a resposta) e **proibição de uso para treinamento**. Ver `docs/seguranca/dados-retencao-exclusao.md` (subprocessadores).
- Não há opção de inferência no Brasil na versão atual. Ver ADR-021.

## 3. Fluxos de dados principais

### 3.1 Microsoft 365 (e-mail e calendário)
```
Microsoft 365 (Graph API) --leitura--> conectores --> memoria-da-conta --> assistente --> usuário
```
- Direção: **somente leitura** a partir do Microsoft 365. A Vértice não envia e-mails, não cria eventos e não altera caixas.
- Frequência: busca incremental a cada 10 minutos por caixa conectada.
- Detalhes: `docs/integracoes/microsoft-365.md`.

### 3.2 Webhook de entrada (ex.: ERP do cliente)
```
Sistema do cliente (ou intermediário) --HTTPS POST assinado--> api-gateway --> ingestao --> memoria-da-conta
```
- Direção: **de mão única, do sistema do cliente para a Vértice.** A Vértice não consulta nem escreve no sistema de origem. Ver ADR-014.
- Detalhes: `docs/integracoes/webhook-generico.md`.

### 3.3 Importação CSV
```
Usuário (upload na interface) --> ingestao (validação + relatório) --> memoria-da-conta
```
- Detalhes: `docs/integracoes/importacao-csv.md`.

### 3.4 Assistente
```
memoria-da-conta --trechos selecionados--> assistente --> provedor de modelo (EUA, retenção zero) --> assistente --> usuário
```
- O texto vindo de e-mails, transcrições, campos importados ou webhooks é tratado como **conteúdo**, nunca como instrução. Ver `docs/seguranca/ia-e-tratamento-de-conteudo.md`.

## 4. Separação entre clientes

- Arquitetura multi-inquilino com isolamento lógico: cada registro carrega o identificador do inquilino e todas as consultas são filtradas na camada de acesso a dados.
- Não há opção de instância dedicada (single-tenant) na versão atual.

## 5. Criptografia [C]

| Onde | Como |
|---|---|
| Em trânsito | TLS 1.2 ou superior em todas as conexões externas |
| Em repouso | AES-256 em bancos, arquivos e backups |
| Tokens OAuth e segredos de webhook | Cifrados com chaves do serviço de gestão de chaves da nuvem, rotacionadas anualmente |
| Chaves gerenciadas pelo cliente (BYOK) | **Não suportado** |

## 6. Limites conhecidos

- Não há instância dedicada nem chaves gerenciadas pelo cliente.
- Inferência do assistente fora do Brasil (ver §2).
- Permissões são por objeto e por equipe, não por campo (ver `docs/seguranca/permissoes.md`).
