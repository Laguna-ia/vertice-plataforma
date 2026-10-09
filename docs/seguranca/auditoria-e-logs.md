# Auditoria e registros (logs)

| Campo | Valor |
|---|---|
| Responsável | Paulo Nogueira (Segurança) |
| Versão do documento | 2.2 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 12/10/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

## 1. O que é registrado

| Categoria | Exemplos de evento | Status | Planos | Retenção |
|---|---|---|---|---|
| Login e sessão | Login, falha de login, logout, encerramento de sessão | GA | Todos | 12 meses |
| Administração | Criação e desativação de usuário, mudança de papel, configuração de SSO | GA | Todos | 12 meses |
| **Conexões de integração** | Conexão, desconexão, revogação e renovação de token do Microsoft 365, Gmail e Google Calendar; criação, rotação e desativação de fontes de webhook | **GA** | Crescimento, Enterprise | 12 meses |
| Importação e exportação | Quem importou ou exportou, arquivo, linhas, resultado | GA | Todos | 12 meses |
| Recebimento de webhook | Recibo de cada evento (ver `docs/integracoes/webhook-generico.md` §5) | GA | Crescimento, Enterprise | **30 dias** |
| **Visualização de registros** ("quem viu o quê") | Abertura de conta, contato, oportunidade ou objeto personalizado; geração de briefing | **Beta** desde v4.11.0 (05/10/2026). Feature flag `audit.record_view_log`, **desligada por padrão**, ativada por cliente a pedido de Produto | Enterprise | **90 dias** (em beta) |

## 2. Conteúdo de cada evento

Data e hora (UTC, exibida no fuso do usuário), usuário, endereço IP, agente do navegador, tipo do evento, objeto afetado e resultado. O conteúdo de e-mails e campos **não** é copiado para o log.

## 3. Consulta e exportação

- Tela **Administração › Auditoria**, com filtros por usuário, período e categoria. Acesso restrito ao papel Administrador.
- Exportação em CSV (gera, ela própria, um evento de auditoria).
- **Envio contínuo para SIEM do cliente (syslog/HTTP): planejado**, sem data. Hoje, a integração com SIEM é por exportação periódica manual.

## 4. Integridade

- Os registros são somente de inclusão: nenhum usuário, inclusive Administrador, edita ou apaga eventos pela aplicação.
- Acesso de funcionários da Vértice a dados de clientes (suporte) exige autorização do cliente registrada no chamado e gera evento de auditoria visível ao administrador do cliente.

## 5. Limites conhecidos

- O registro de visualização está em beta: cobre telas da aplicação web, mas **não cobre a API REST de leitura** nem exportações (estas têm evento próprio de exportação).
- A retenção de 90 dias do registro de visualização deve subir para 12 meses na liberação GA (planejado para v4.12, sem compromisso de data).
