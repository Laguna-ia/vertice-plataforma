# Vértice Plataforma — documentação técnica e de produto

> **Simulação — dados sintéticos para treinamento.** A Vértice, seus clientes, pessoas, versões e números são fictícios. Este repositório não contém o código real de nenhum produto: ele **simula as evidências** que um time de Engenharia e Produto manteria junto ao código (arquitetura, manifestos de integração, feature flags, contratos de API, changelog e decisões técnicas).

Repositório de referência da plataforma Vértice (CRM com memória da conta e briefing assistido). Mantido por Engenharia e Produto. Serve de fonte para o time comercial, pré-venda e o **Agente Arquiteto de Soluções**.

## Como ler este repositório

| Pergunta | Onde procurar | O que a fonte prova |
|---|---|---|
| Como o produto é construído? | `docs/arquitetura/` | Componentes, fluxos de dados, hospedagem |
| O que cada integração faz e não faz? | `docs/integracoes/`, `config/integracoes/`, `api/` | Escopos, direção do dado, limites, erros |
| Login, permissões, logs, dados, IA | `docs/seguranca/` | Controles implementados e seus limites |
| Disponibilidade, backup, incidentes | `docs/operacao/` | Metas operacionais e procedimentos |
| O que está liberado para qual plano? | `config/feature-flags.yaml`, `config/planos.yaml` | Estado da liberação (GA, beta, desligado) |
| O que mudou e quando? | `CHANGELOG.md` | Versão e data de cada mudança |
| Por que foi feito assim? | `docs/decisoes/` | Decisões de arquitetura (ADR) |
| O que posso vender e implantar? | `comercial/` | Escopo por plano, implantação, FAQ aprovado |

## Status de capacidade (vale para todos os documentos)

| Status | Significado | Pode ser afirmado ao cliente? |
|---|---|---|
| **GA** | Disponível em produção para os planos indicados | Sim, nas condições descritas |
| **Beta** | Implementado, liberado por feature flag para clientes selecionados | Só como beta, sem compromisso de prazo para GA |
| **Em desenvolvimento** | Em construção, sem liberação | Não. Encaminhar a Produto |
| **Planejado** | No roadmap, sem código | Não. Roadmap não é promessa |
| **Não suportado** | Não existe e não está no roadmap | Sim, com clareza |

## Regras de uso das fontes

1. **Código e configuração respondem "existe e como funciona".** Não respondem se a capacidade está liberada para um cliente, nem o que foi contratado.
2. **Feature flag responde "está liberado para quem".** Uma capacidade implementada pode estar desligada para o plano ou para o cliente.
3. **Contrato e proposta respondem "o que foi vendido".** Ficam fora deste repositório.
4. **Material comercial (`comercial/`) responde "o que podemos dizer".** Quando divergir da documentação técnica, vale a versão mais recente da fonte técnica, e a divergência deve ser reportada ao responsável do documento comercial.
5. Toda afirmação ao cliente deve citar o documento e a versão de onde veio.

## Responsáveis

| Área | Responsável | Contato |
|---|---|---|
| Produto | Otávio Rangel (Head de Produto) | otavio.rangel@vertice.example |
| Engenharia de Plataforma | Helena Duarte (Tech Lead de Plataforma) | helena.duarte@vertice.example |
| Segurança da Informação | Paulo Nogueira (Security Lead) | seguranca@vertice.example |
| Privacidade (Encarregado/DPO) | Lívia Monteiro | privacidade@vertice.example |
| Comercial | Rodrigo Sampaio (Diretor Comercial) | rodrigo.sampaio@vertice.example |

Versão atual da plataforma: **v4.11.2** (14/10/2026). Próxima versão planejada: v4.12 (planejada para 03/11/2026, sem compromisso de data).
