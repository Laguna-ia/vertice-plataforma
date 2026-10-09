# FAQ de integrações e segurança — respostas aprovadas para uso comercial

| Campo | Valor |
|---|---|
| Responsável | Otávio Rangel (Produto), revisão de Paulo Nogueira (Segurança) |
| Versão do documento | 1.3 |
| Data de revisão | 20/08/2026 |
| Próxima revisão prevista | 20/10/2026 (atrasada) |
| Classificação | **Texto aprovado para uso comercial** |

> Simulação — dados sintéticos para treinamento.
> Use o texto das respostas como está. Se a pergunta do cliente for diferente, ou se a documentação técnica em `docs/` for mais recente e disser outra coisa, **não adapte por conta própria**: consulte Produto.

## Microsoft 365 e Entra

**A Vértice lê o e-mail de todo mundo da empresa?**
Não. Só as caixas que cada usuário conecta e autoriza. A Vértice só lê; não envia e-mails nem altera a agenda.

**A Vértice tem login único (SSO) com Microsoft Entra?**
O login único por SAML está em **beta** para clientes Enterprise selecionados. Consulte Produto antes de confirmar para um cliente.

**O administrador pode autorizar a integração em nome de todos?**
Hoje a autorização é feita por usuário. Consulte Produto sobre consentimento por administrador.

## Dados e privacidade

**Onde os dados ficam?**
Os dados e os backups ficam no Brasil, em nuvem pública na região São Paulo. O assistente de IA usa um provedor de modelos com processamento nos Estados Unidos, sem retenção e sem uso para treinamento.

**Os dados do cliente treinam a IA?**
Não.

**O que acontece com os dados no fim do contrato?**
O cliente tem 30 dias para exportar. Depois, os dados são excluídos e os backups expiram em seguida. Emitimos certificado de exclusão a pedido.

## Registros e auditoria

**A Vértice registra acessos?**
Sim. A Vértice registra logins, ações administrativas, conexões de integração e **visualizações de registros**, e o administrador consulta tudo na tela de auditoria.

## Webhook e CSV

**A Vértice tem conector para o meu ERP?**
Os conectores nativos são Gmail, Microsoft 365 e Google Calendar. Para outros sistemas, como ERPs, o caminho é webhook ou importação CSV, avaliados caso a caso. Não prometemos compatibilidade nem prazo antes da avaliação técnica.

**O webhook pode afetar meu ERP?**
O webhook de entrada é de mão única: seu sistema envia dados para a Vértice. A Vértice não escreve no seu sistema.

**Posso importar CSV automaticamente todos os dias?**
A importação é feita pela interface, por um administrador. Importação automática não está disponível.

## Implantação

**Quanto tempo leva a implantação?**
Para e-mail, agenda e CSV, a implantação padrão leva **até 30 dias** após a assinatura. Integrações via webhook não entram nesse prazo.
