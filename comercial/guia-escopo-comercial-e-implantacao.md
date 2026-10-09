# Guia de escopo comercial e implantação

| Campo | Valor |
|---|---|
| Responsável | Otávio Rangel (Produto) e Rodrigo Sampaio (Comercial) |
| Versão do documento | 2.0 |
| Plataforma de referência | v4.11 |
| Data de revisão | 06/10/2026 |
| Classificação | **Interno** |

> Simulação — dados sintéticos para treinamento.

## 1. O que cada plano inclui

| Item | Essencial | Crescimento | Enterprise |
|---|---|---|---|
| Preço de referência | R$ 149/usuário/mês (mín. 5) | R$ 249/usuário/mês (mín. 15) | A partir de R$ 18.000/mês por unidade operacional |
| Usuários | Por usuário | Por usuário | Até 60 por unidade |
| Memória da conta, briefing, próximo passo, atualização assistida | Sim | Sim | Sim |
| Handoff para CS e colaboração | Não | Sim | Sim |
| Gmail, Microsoft 365, Google Calendar | Não | Sim | Sim |
| Importação CSV | Sim | Sim | Sim |
| Webhook de entrada | Não | Sim | Sim |
| Webhook de saída e API REST de leitura | Não | Não | Sim |
| SSO SAML (Entra, Okta, Google) | Não | Não | Sim (GA desde 05/10/2026) |
| Consentimento por administrador Microsoft 365 | Não | Não | Beta |
| Registro de visualização | Não | Não | Beta |
| Implantação | Não incluída | Não incluída | Cobrada à parte (referência R$ 12.000 por unidade) |

Funcionalidades em **beta** podem ser oferecidas como beta, sem prazo para GA e sem cláusula contratual que dependa delas. Liberação por cliente exige pedido a Produto.

## 2. Unidade operacional (Enterprise)

- Uma unidade operacional é uma operação do cliente com gestão comercial própria (ex.: sede, filial regional), com até 60 usuários.
- Unidade adicional: negociada. Cada unidade tem implantação própria (referência R$ 12.000), salvo aprovação diferente do Diretor Comercial.
- Usuários acima de 60 numa unidade: **sem preço de tabela**. Exige aprovação do Diretor Comercial.

## 3. Implantação padrão (Enterprise, por unidade)

Incluído na referência de R$ 12.000:
1. Configuração inicial do ambiente, equipes e papéis.
2. Configuração de SSO SAML (quando o cliente pedir) e da integração Microsoft 365 ou Gmail.
3. Uma importação inicial de dados por CSV (contatos, contas e até um objeto personalizado), a partir de arquivo **limpo** entregue pelo cliente.
4. Treinamento: duas sessões ao vivo para usuários e uma para administradores.
5. Acompanhamento de 30 dias após a ativação.

Não incluído:
- Limpeza ou padronização de cadastro do cliente (serviço adicional).
- Desenho, mapeamento e homologação de webhook com sistemas do cliente (escopo separado, após avaliação técnica).
- Desenvolvimento do emissor de eventos no sistema do cliente (responsabilidade do cliente ou do fornecedor dele).
- Integrações fora do catálogo.

## 4. Prazos de referência

| Escopo | Prazo típico, após assinatura e com dependências do cliente atendidas |
|---|---|
| Microsoft 365 + SSO + CSV inicial (1 unidade) | **4 a 6 semanas** |
| Unidade adicional, mesmo escopo | 3 a 4 semanas, em paralelo ou em sequência |
| Integração via webhook com ERP | 2 a 4 semanas do lado da Vértice, **depois** que o emissor do cliente estiver funcionando. Prazo do emissor não é estimado pela Vértice |

Prazos são referência, não garantia. Nunca comprometer data de início sem as dependências do §5 atendidas.

## 5. Dependências do cliente

- Assinatura do contrato e do DPA.
- Lista nominal de usuários por unidade.
- Administrador do Entra disponível (SSO e, se usado, consentimento por administrador).
- Aprovação de TI/segurança do cliente para o desenho de dados.
- Arquivo CSV limpo, com responsável do lado do cliente.
- Para webhook: emissor de eventos, definição de campos, ambiente de teste com dados fictícios.

## 6. Condições que exigem aprovação

| Situação | Quem aprova |
|---|---|
| Vigência diferente de 24 meses | Diretor Comercial |
| Desconto sobre referência ou condição especial por unidade | Diretor Comercial |
| Usuários acima de 60 por unidade | Diretor Comercial |
| Reajuste, rescisão antecipada, nível de suporte e SLA contratual | Diretor Comercial + Jurídico (**texto padrão em revisão; não há versão aprovada em 06/10/2026**) |
| Compromisso com funcionalidade beta, em desenvolvimento ou planejada | **Não permitido.** Produto pode registrar o pedido no roadmap |
| Escopo de integração via webhook | Produto (após avaliação técnica) + Diretor Comercial (preço) |
| Respostas a questionários de segurança | Rascunho pelo arquiteto de soluções; revisão de Segurança antes do envio |

## 7. Serviços adicionais

| Serviço | Referência |
|---|---|
| Limpeza e padronização de cadastro | Sob orçamento, após amostra do arquivo |
| Avaliação técnica de integração via webhook | Sem custo até 2 reuniões técnicas; acima disso, sob orçamento |
| Mapeamento e homologação de webhook | Sob orçamento, após avaliação técnica |
| Treinamento adicional | Sob orçamento |
