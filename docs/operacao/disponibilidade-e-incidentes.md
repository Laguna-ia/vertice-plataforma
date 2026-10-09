# Disponibilidade, continuidade e incidentes

| Campo | Valor |
|---|---|
| Responsável | Helena Duarte (Plataforma) e Paulo Nogueira (Segurança) |
| Versão do documento | 1.2 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 10/09/2026 |
| Classificação | **Interno**. §2 é compartilhável com cliente. Os números de §1 e §3 são metas e procedimentos internos: só podem ser apresentados ao cliente como compromisso se constarem do contrato |

> Simulação — dados sintéticos para treinamento.

## 1. Metas de disponibilidade

- Meta interna de disponibilidade mensal: **99,5%** (excluídas janelas de manutenção comunicadas com 72 h de antecedência).
- **O SLA contratual e o nível de suporte do Enterprise não são definidos por este documento.** Eles estão em revisão pelo Comercial (ver `comercial/guia-escopo-comercial-e-implantacao.md` §6). Não oferecer números de SLA sem aprovação comercial.
- Página de status pública: `status.vertice.example`.

## 2. Continuidade e recuperação

| Item | Valor |
|---|---|
| Backups | Diários completos + contínuos (point-in-time), retidos por 35 dias, região São Paulo |
| RPO (perda máxima de dados) | 1 hora |
| RTO (tempo para restabelecer) | 8 horas |
| Teste de restauração | Trimestral; último em 08/2026 |
| Redundância | Duas zonas de disponibilidade na região São Paulo; **sem região secundária** |

## 3. Incidentes de segurança

- Procedimento de resposta a incidentes revisado anualmente (última revisão 03/2026).
- Notificação ao cliente afetado: em até **48 horas** após a confirmação de um incidente que envolva seus dados, com atualização a cada 24 h até o encerramento.
- A comunicação à ANPD e aos titulares é do controlador (cliente); a Vértice apoia com as informações necessárias.

## 4. Falhas de integração

- Falha de conexão Microsoft 365 (token expirado, consentimento revogado): conexão marcada como "erro" e alerta ao usuário e ao administrador; nenhum dado é perdido no Microsoft 365.
- Falha de webhook: ver `docs/integracoes/webhook-generico.md` §4. O reenvio é responsabilidade do emissor.
