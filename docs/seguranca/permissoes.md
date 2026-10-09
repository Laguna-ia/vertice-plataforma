# Papéis e permissões

| Campo | Valor |
|---|---|
| Responsável | Helena Duarte (Plataforma) |
| Versão do documento | 1.4 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 15/08/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

## 1. Papéis padrão

| Papel | Pode |
|---|---|
| Administrador | Tudo, inclusive integrações, SSO, importação, exportação, auditoria e usuários |
| Gestor | Ver e editar contas das suas equipes; exportar; ver painéis |
| Vendedor | Ver e editar as contas das quais é dono ou membro; usar o assistente |
| Leitura | Ver contas das suas equipes, sem editar nem exportar |

Papéis personalizados: **planejado**, sem data.

## 2. Escopo de visibilidade

- A visibilidade é por **equipe** e por **propriedade da conta**. Uma conta pode ser compartilhada com outras equipes.
- E-mails coletados de uma caixa ficam visíveis para quem tem acesso à conta associada. O dono da caixa pode marcar um e-mail como privado (fica visível só para ele e não entra no briefing).

## 3. Restrição por campo

- **Não suportado.** Não é possível esconder um campo específico (ex.: "valor do contrato") de um papel e mostrar o resto do registro.
- Alternativa recomendada: **não enviar** o campo sensível à Vértice. No webhook e no CSV, só entram os campos mapeados; um campo que não é enviado não existe na Vértice.

## 4. Assistente e permissões

- O briefing e as sugestões de um usuário usam apenas dados que esse usuário já pode ver.
- O assistente não altera estágio, valor ou dono de oportunidade sozinho. Atualizações assistidas são **rascunhos** que um usuário autorizado aprova.
