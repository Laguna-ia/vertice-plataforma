# Autenticação e login único (SSO)

| Campo | Valor |
|---|---|
| Responsável | Paulo Nogueira (Segurança) e Helena Duarte (Plataforma) |
| Versão do documento | 2.0 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 07/10/2026 |
| Classificação | **Compartilhável com cliente** |

> Simulação — dados sintéticos para treinamento.

## 1. Métodos de login

| Método | Status | Planos |
|---|---|---|
| E-mail e senha com MFA (aplicativo autenticador TOTP) | GA | Todos |
| Login com Google | GA | Todos |
| **SSO SAML 2.0** (Microsoft Entra ID, Okta, Google Workspace e outros IdPs compatíveis) | **GA desde v4.11.0 (05/10/2026)**. Beta entre v4.9 (11/08/2026) e v4.11. | **Enterprise** |
| SSO OpenID Connect (OIDC) | Planejado | — |
| Provisionamento automático de usuários via SCIM 2.0 | **Em desenvolvimento** | — |

## 2. SSO com Microsoft Entra ID

- Configuração por metadados SAML (URL de metadados ou arquivo XML) na tela **Administração › Segurança › SSO**.
- Atributos esperados: `emailaddress` (obrigatório), `givenname`, `surname`; `groups` opcional, para mapear grupos do Entra a equipes da Vértice.
- **Provisionamento no primeiro login (JIT):** usuário atribuído ao aplicativo no Entra é criado na Vértice no primeiro acesso, com o papel padrão definido pelo administrador. Disponível.
- **Desprovisionamento:** sem SCIM, remover o usuário no Entra **impede novos logins**, mas sessões já abertas continuam válidas até expirar (máximo definido pela política de sessão, §4). Para efeito imediato, o administrador também deve desativar o usuário na Vértice.
- **SSO obrigatório:** o administrador pode bloquear login por senha para o domínio do cliente. Contas de emergência ("break-glass") podem ser mantidas com MFA.
- MFA: quando o SSO está ativo, o MFA é o do IdP (ex.: políticas de acesso condicional do Entra). A Vértice não aplica um segundo fator adicional.

## 3. Relação com a integração Microsoft 365

SSO (login na Vértice) e a integração Microsoft 365 (leitura de e-mail e agenda) são **configurações separadas**, com aplicativos empresariais distintos no Entra. Ter SSO ativo não conecta caixas, e conectar caixas não exige SSO. Ver `docs/integracoes/microsoft-365.md`.

## 4. Sessão

- Duração padrão da sessão: 8 horas; configurável pelo administrador entre 15 minutos e 12 horas.
- Encerramento por inatividade: 60 minutos (configurável).
- O administrador pode encerrar todas as sessões de um usuário.

## 5. Política de senha (login sem SSO)

- Mínimo de 12 caracteres, verificação contra senhas vazadas conhecidas, bloqueio temporário após 10 tentativas.
- MFA pode ser exigido pelo administrador para todos os usuários.

## 6. Restrição de acesso por rede

- **Lista de IPs permitidos para acesso à interface: não suportado.** Recomenda-se usar as políticas de acesso condicional do IdP quando o SSO estiver ativo.
