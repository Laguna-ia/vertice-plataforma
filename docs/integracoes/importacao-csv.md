# Importação e exportação CSV

| Campo | Valor |
|---|---|
| Responsável | Helena Duarte (Engenharia de Plataforma) |
| Versão do documento | 1.6 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 30/09/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

## 1. Importação

- Upload pela interface (**Administração › Dados › Importar**), por usuário com papel Administrador.
- Arquivo UTF-8, separador vírgula ou ponto e vírgula, até **20 MB** ou **100.000 linhas** por arquivo.
- Objetos: contatos, contas, oportunidades, atividades e **objetos personalizados** (ex.: "contrato", com campos definidos pelo cliente).
- Mapeamento de colunas na tela, salvo como modelo para as próximas importações.
- Chave de deduplicação escolhida pelo administrador (ex.: código do contrato). Linhas com a mesma chave atualizam o registro existente.

## 2. Validação

- Antes de gravar, a Vértice gera um **relatório de pré-visualização**: linhas válidas, linhas com erro (e o motivo) e duplicatas.
- O administrador confirma ou cancela. Nada é gravado sem confirmação.
- A Vértice **não normaliza nomes** automaticamente (ex.: "Sérgio A." e "Sergio Andrade" viram dois valores). A limpeza do cadastro é responsabilidade do cliente; pode ser contratada como serviço adicional.

## 3. Reversão

- Cada importação recebe um identificador. Durante **7 dias**, o administrador pode desfazer a importação inteira (os registros criados são removidos e os atualizados voltam ao valor anterior).

## 4. Registro

- Cada importação gera evento de auditoria com usuário, arquivo, número de linhas e resultado.

## 5. Importação agendada (SFTP)

- **Em desenvolvimento.** Importação automática a partir de pasta SFTP, com agenda diária.
- Sem data de liberação. Não oferecer a clientes. Enquanto isso, a importação periódica é **manual** (upload pela interface).

## 6. Exportação

- Contatos, contas, oportunidades e atividades exportáveis em CSV por usuários com papel Administrador ou Gestor.
- Exportações geram evento de auditoria.
