# Dados: localização, retenção, exclusão e subprocessadores

| Campo | Valor |
|---|---|
| Responsável | Lívia Monteiro (Privacidade/DPO) e Paulo Nogueira (Segurança) |
| Versão do documento | 1.8 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 01/10/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

## 1. Papéis na LGPD

- O **cliente é o controlador** dos dados pessoais inseridos ou coletados na Vértice. A **Vértice é operadora**.
- O tratamento segue o Acordo de Tratamento de Dados (DPA) anexo ao contrato Enterprise. Modelo disponível com o Comercial, mediante pedido.

## 2. Que dados a Vértice armazena

| Origem | Dados | Observação |
|---|---|---|
| Microsoft 365 / Gmail | Remetente, destinatários, data, assunto e **corpo** dos e-mails; título, participantes, data e descrição dos eventos | Anexos de e-mail **não** são armazenados (apenas nome do arquivo) |
| CSV | Somente as colunas mapeadas | Colunas não mapeadas são descartadas |
| Webhook | Somente os campos mapeados | Campos não mapeados são descartados |
| Uso da aplicação | Registros do CRM criados pelos usuários, logs | — |

## 3. Localização

- Dados e backups: **Brasil (região São Paulo)**.
- Inferência do assistente: **Estados Unidos**, com retenção zero no provedor (ver §6). Isso caracteriza **transferência internacional** nos termos da LGPD, coberta por cláusulas contratuais no DPA.

## 4. Retenção

| Dado | Retenção durante o contrato |
|---|---|
| E-mails e eventos coletados | Janela móvel de **24 meses** a partir da data do e-mail/evento (configurável para menos) |
| Registros do CRM | Enquanto o contrato estiver ativo, até exclusão pelo cliente |
| Logs de auditoria | 12 meses (registro de visualização em beta: 90 dias) |
| Recibos de webhook | 30 dias |
| Backups | 35 dias, cifrados, na região São Paulo |

## 5. Exclusão

- **Durante o contrato:** o administrador exclui registros, contatos ou importações; a exclusão é imediata na aplicação e os dados saem dos backups no ciclo de 35 dias.
- **Pedido de titular (LGPD):** o cliente, como controlador, atende o titular; a Vértice fornece a ferramenta de busca e exclusão por e-mail do titular.
- **Fim do contrato:** o cliente tem **30 dias** para exportar os dados. Depois disso, a Vértice exclui os dados de produção em até 30 dias e os backups expiram em até 35 dias. Certificado de exclusão emitido a pedido.

## 6. Subprocessadores

| Subprocessador (categoria) | Finalidade | Local |
|---|---|---|
| Provedor de nuvem pública | Hospedagem, banco de dados, armazenamento, backups | Brasil (São Paulo) |
| Provedor de modelos de linguagem | Inferência do assistente, **retenção zero, sem treinamento** | Estados Unidos |
| Serviço de e-mail transacional | Convites e alertas | Estados Unidos |
| Ferramenta de suporte ao cliente | Chamados de suporte | Estados Unidos |

- Lista nominal dos subprocessadores e contratos: disponível sob acordo de confidencialidade, com Segurança.
- Mudanças na lista são comunicadas com **30 dias** de antecedência aos clientes Enterprise.

## 7. Uso dos dados do cliente

- Dados de clientes **não são usados para treinar modelos**, nem pela Vértice nem pelo provedor de modelos.
- Métricas agregadas e anonimizadas de uso do produto podem ser usadas para melhoria do produto.
