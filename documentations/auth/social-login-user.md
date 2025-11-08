# Configuração de Login Social pelo Painel

Esta documentação explica como o proprietário da plataforma (tenant) pode habilitar os logins sociais diretamente pelo painel administrativo. O processo é feito na aba **Social** dentro das configurações do tenant.

## Pré-requisitos
- Ter acesso ao painel como dono do tenant (usuário que enxerga as abas de configurações).
- Já possuir as credenciais (Client ID e Client Secret) geradas em cada provedor:
  - **Google**: Console do Google Cloud → OAuth 2.0.
  - **Facebook**: Painel de Developers → Facebook Login.
  - **X (Twitter)**: Developer Portal → App OAuth 2.0.

## Passo a passo

1. **Acesse o painel administrativo**
   - Realize login como proprietário do tenant.
   - Abra o menu lateral e entre em `Configurações da plataforma`.

2. **Selecione a aba “Social”**
   - Na parte superior da página há as abas `Geral`, `Aparência`, `Menu lateral`, `Social` e `Outros`.
   - Clique em **Social** para abrir o formulário de credenciais.

3. **Informe as credenciais de cada provedor**
   - Para cada card (Google, Facebook, X) preencha os campos `Client ID` e `Client Secret` com os valores fornecidos pelo provedor.
   - Caso não queira habilitar um provedor específico, deixe os campos vazios.

4. **Copie a URI de Redirect**
   - Cada card exibe, na parte inferior, a URI de callback que deve ser configurada no provedor.
   - Utilize o botão “Copiar URI” para copiar o endereço e cadastre-o no painel do provedor (Google, Facebook ou X).
   - A estrutura da URI é sempre `https://SEU_DOMINIO_DO_TENANT/auth/social/{provider}/callback`.

5. **Salve as alterações**
   - Após preencher todos os dados necessários, clique em **Salvar alterações**.
   - O sistema exibirá uma mensagem de sucesso quando as credenciais forem gravadas.

6. **Recarregue se necessário**
   - Caso tenha dúvidas sobre o que foi salvo, use o botão `Recarregar` para buscar novamente os valores registrados no backend.

## Como funciona após salvar
- Assim que houver uma credencial válida (`Client ID` e `Client Secret`) para o provedor, o botão correspondente na tela de login do front-end passa a funcionar.
- Quando um usuário clica em “Entrar com Google/Facebook/X”, o frontend abre o fluxo OAuth usando as credenciais informadas. Ao final da autenticação, o usuário é redirecionado de volta ao domínio do tenant.
- Sem credenciais, os botões ainda aparecem, mas o fluxo retornará erro (o que serve como validação de configuração).

## Dicas importantes
- Cadastre sempre o domínio completo do tenant (incluindo protocolo HTTPS) nas configurações do provedor para evitar erros no callback.
- Caso o provedor exija ambientes distintos (produção vs. homologação), utilize tenants específicos para cada ambiente e cadastre as credenciais correspondentes.
- Se precisar revogar um provedor temporariamente, basta limpar os campos e salvar.
- Lembre-se de testar o login social em uma aba anônima para confirmar que o fluxo completo está funcionando.

Seguindo esses passos, o login social fica disponível sem necessidade de deploys adicionais, permitindo que cada tenant gerencie suas credenciais diretamente pelo painel.
