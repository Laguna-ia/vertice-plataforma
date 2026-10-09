# Webhook genérico (entrada e saída)

| Campo | Valor |
|---|---|
| Responsável | Helena Duarte (Engenharia de Plataforma) |
| Versão do documento | 3.0 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 06/10/2026 |
| Classificação | **Compartilhável com cliente** (§8 é interno) |

> Simulação — dados sintéticos para treinamento.

## 1. Resumo

O webhook genérico permite que um sistema do cliente **envie eventos** à Vértice (entrada). Não é um conector pronto: o cliente, ou um intermediário contratado por ele, precisa **emitir** os eventos. A Vértice **não busca** dados no sistema de origem e **não escreve** nele. Ver ADR-014.

Há também um webhook de **saída** (§6), em que a Vértice envia eventos dela para uma URL do cliente. Os dois são independentes.

## 2. Entrada — como funciona

- Endpoint por inquilino: `POST https://hooks.vertice.example/v1/in/{tenant_id}/{fonte}`.
- Formato: JSON, até **256 KB** por evento. Contrato em `api/webhook-entrada.openapi.yaml`.
- Tipos de evento aceitos: `registro.criado`, `registro.atualizado`, `registro.removido`, aplicados a um **objeto mapeado** (ex.: "contrato") com os campos definidos no mapeamento.
- Os campos aceitos são os definidos no **mapeamento** configurado na implantação. Campos não mapeados são **descartados e não armazenados**.
- Idempotência: cabeçalho `Idempotency-Key` obrigatório; eventos repetidos com a mesma chave em 24 h são ignorados.
- Limite: 50 requisições por segundo por inquilino.

## 3. Segurança

| Controle | Detalhe |
|---|---|
| Transporte | Somente HTTPS (TLS 1.2+) |
| Assinatura | HMAC-SHA256 do corpo, no cabeçalho `X-Vertice-Signature`, com segredo por fonte. Requisição sem assinatura válida é rejeitada (HTTP 401, código `WEBHOOK_AUTH_401`). |
| Proteção contra repetição | Cabeçalho `X-Vertice-Timestamp`; eventos com mais de 5 minutos são rejeitados |
| Rotação de segredo | Pelo administrador, com período de convivência de 24 h entre segredo antigo e novo |
| Lista de IPs de origem | Opcional, configurável por fonte |
| Desligamento | Administrador desativa a fonte em **Administração › Integrações › Webhooks**; efeito imediato (HTTP 410 para novos eventos) |

## 4. Falhas e reenvio

- A Vértice responde `202` quando aceita o evento, `4xx` quando o evento é inválido e `5xx` quando há falha temporária do lado dela.
- **Quem reenvia é o emissor.** A Vértice não busca eventos perdidos. Recomendamos reenvio com espera exponencial por até 24 h.
- Uma falha do lado da Vértice **nunca** gera escrita ou erro no sistema de origem: o webhook é de mão única.
- Tempo máximo de resposta: 10 s. Acima disso, o emissor recebe tempo esgotado (`WEBHOOK_TIMEOUT` no registro, quando a Vértice chega a registrar a tentativa).

## 5. Registro de recebimento

- Cada evento recebido gera um **recibo**: data e hora, fonte, tipo, chave de idempotência, resultado (aceito, rejeitado, duplicado) e código de erro.
- O administrador consulta os recibos em **Administração › Integrações › Webhooks › Recebimentos**, com filtro por período e resultado, e pode exportar em CSV.
- Retenção dos recibos: **30 dias**. O conteúdo (payload) não é exibido no recibo; apenas os metadados.
- Alerta por e-mail ao administrador quando a taxa de rejeição passa de 5% em 1 hora.

## 6. Saída (eventos da Vértice para o cliente)

- Disponível no Enterprise. Eventos: `oportunidade.estagio_alterado`, `conta.atualizada`, `atividade.criada`.
- Assinados com HMAC-SHA256. A Vértice tenta reenviar até 8 vezes em 24 h.
- O webhook de saída é configurado pelo cliente e só envia para URLs que ele cadastrar. Ele não é usado no desenho de integração com ERP descrito no §8.

## 7. Pré-requisitos do cliente

- Um emissor de eventos (o próprio sistema de origem ou um intermediário) capaz de fazer POST HTTPS assinado.
- Definição dos campos a enviar e do responsável pela manutenção do emissor.
- Ambiente de teste com dados fictícios para a homologação.

## 8. Interno — integrações de ERP via webhook (ex.: Boreal)

- Não existe conector nativo do Boreal e **não há conector no roadmap** (decisão de produto de 02/2026, revisada em 09/2026).
- Clientes com Boreal integrados hoje usam webhook de entrada com emissor mantido por eles ou por terceiro. Há falhas registradas nesses casos (tempo esgotado e assinatura inválida), em geral do lado do emissor; ver tickets de CS.
- Esforço típico observado do lado da Vértice: **mapeamento de campos e homologação, de 2 a 4 semanas** após o cliente ter um emissor funcionando. O esforço do emissor é do cliente ou do fornecedor do ERP e não é estimado pela Vértice.
- Esse esforço **não faz parte da implantação padrão** (ver `comercial/guia-escopo-comercial-e-implantacao.md`).
- Para campos simples (ex.: vigência e gestor do contrato), o CSV periódico é alternativa válida enquanto o emissor não existir.
