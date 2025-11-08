# Configuração de Login Social pelo Painel

Esta documentação explica como o proprietário da plataforma (tenant) pode habilitar os logins sociais diretamente pelo painel administrativo. O processo é feito na aba **Social** dentro das configurações do tenant.

## Pré-requisitos

-   Ter acesso ao painel como dono do tenant (usuário que enxerga as abas de configurações).
-   Possuir uma conta de desenvolvedor/console nas plataformas desejadas:
    -   [Google Cloud Console](https://console.cloud.google.com/)
    -   [Meta for Developers (Facebook)](https://developers.facebook.com/)
    -   [X Developer Portal](https://developer.twitter.com/en/portal/dashboard)
-   Criar previamente o aplicativo em cada provedor para obter **Client ID** e **Client Secret**.

---

## Passo a passo no painel

1. **Acesse o painel administrativo**

    - Realize login como proprietário do tenant.
    - Abra o menu lateral e acesse `Configurações da plataforma`.

2. **Selecione a aba “Social”**

    - Na parte superior da página há as abas `Geral`, `Aparência`, `Menu lateral`, `Social` e `Outros`.
    - Clique em **Social** para abrir o formulário de credenciais sociais.

3. **Informe as credenciais de cada provedor**

    - Para cada card (Google, Facebook, X) preencha `Client ID` e `Client Secret` com os valores fornecidos pelo provedor.
    - Caso não queira habilitar um provedor específico, deixe os campos vazios.

4. **Copie e salve a Redirect URI no provedor**

    - Cada card mostra a URL de callback do tenant (ex.: `https://seu-dominio/auth/social/google/callback`).
    - Use o botão **“Copiar URI”** e cadastre a URL apropriada no console do provedor.

5. **Salve as alterações**

    - Clique em **Salvar alterações**.
    - Se houver sucesso, a badge “Credenciais configuradas” aparece no card correspondente.

6. **Recarregue se necessário**
    - Utilize o botão `Recarregar` para buscar novamente os valores gravados no backend.

---

## Tutorial por provedor

### Google

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/).
2. Crie ou selecione um projeto.
3. Vá em **APIs e serviços → Tela de permissão OAuth** e configure o tipo de usuário.
4. Em **Credenciais → Criar credenciais → ID do cliente OAuth**, escolha “Aplicativo da Web”.
5. Em **URIs autorizados de redirecionamento**, adicione a URL copiada do painel (`https://seu-dominio/auth/social/google/callback`).
6. Salve e copie o **Client ID** e o **Client Secret** gerados.
7. Volte ao painel, cole os valores nos campos do Google e salve.

### Facebook

1. Acesse o [Meta for Developers](https://developers.facebook.com/) e clique em **Meus Apps**.
2. Crie um app ou abra o existente, depois habilite **Facebook Login** no modo Web.
3. Em **Configurações → Básico**, copie o **App ID** (Client ID) e o **App Secret**.
4. Em **Facebook Login → Configurações**, defina o **URI de redirecionamento válido** com a URL copiada do painel (`https://seu-dominio/auth/social/facebook/callback`).
5. Salve as configurações e insira o App ID/Secret no painel do tenant.

### X (Twitter)

1. Acesse o [X Developer Portal](https://developer.twitter.com/en/portal/dashboard).
2. Crie ou edite um app Dentro do projeto apropriado.
3. Vá em **User authentication settings** e habilite OAuth 2.0 (Client Credentials).
4. Em **Callback URL**, informe a URL copiada do painel (`https://seu-dominio/auth/social/x/callback`).
5. Salve as alterações e gere o **Client ID** e o **Client Secret**.
6. Cole os valores no painel do tenant e salve.

---

## Como funciona após salvar

-   Assim que as credenciais estiverem preenchidas e salvas, os botões “Entrar com Google/Facebook/X” do front-end passam a redirecionar corretamente para o provedor.
-   Ao término da autenticação, o usuário retorna ao domínio do tenant via `/auth/social/{provider}/callback`, recebe o token e é logado no sistema.

## Dicas importantes

-   Cadastre exatamente o domínio público onde o tenant opera (incluindo HTTPS) nos consoles dos provedores.
-   Se possuir ambientes distintos (homologação, produção), configure cada tenant com suas respectivas URIs e credenciais.
-   Para desativar temporariamente um provedor, basta limpar os campos e salvar.
-   Sempre teste o fluxo em uma janela anônima para confirmar que o login social está funcionando de ponta a ponta.

Seguindo estes passos, o login social fica disponível sem necessidade de alterações de código, permitindo que cada tenant administre suas credenciais de forma autônoma.
