# Controle de entrega de EPI · Moura Dubeux — pacote para hospedagem

Site 100% estático (HTML + JavaScript no navegador). Não precisa de servidor, banco de dados nem instalação.

## O que tem na pasta
- `index.html` — o sistema completo (logo, guia e telas já incluídos)
- `vendor/` — bibliotecas locais (PDF, captura da ficha e leitura de Excel)
- `fonts/` — fonte Inter local (o site não chama nenhum serviço externo)
- `_headers` — cabeçalhos de segurança (Netlify e Cloudflare Pages usam; GitHub Pages ignora)
- `.nojekyll` — evita processamento do GitHub Pages

> Envie a pasta **inteira**, mantendo a estrutura. O `index.html` sozinho não funciona sem `vendor/` e `fonts/`.

## Requisito obrigatório: HTTPS
O login usa recursos do navegador que só funcionam em endereço seguro (https://). Netlify, Cloudflare Pages e GitHub Pages já entregam HTTPS automático.

## Opção A — Netlify (mais simples, arrastar e soltar)
1. Crie uma conta gratuita em netlify.com e entre.
2. Em **Add new site → Deploy manually**, arraste a pasta `deploy` para a área indicada.
3. Em poucos segundos o site fica no ar em um endereço `https://nome-aleatorio.netlify.app`.
4. Em **Site configuration → Change site name**, escolha um nome (ex.: `epi-mouradubeux`).
5. Para atualizar depois: **Deploys → arraste a pasta de novo**.

## Opção B — GitHub Pages (gratuito, estável)
1. Crie uma conta em github.com e um repositório novo (ex.: `controle-epi`). No plano gratuito o repositório precisa ser **público** para usar Pages.
2. Em **Add file → Upload files**, arraste todo o conteúdo da pasta `deploy` (inclusive `vendor/` e `fonts/`) e clique em **Commit changes**.
3. Em **Settings → Pages**, em **Source** escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`, e salve.
4. Após 1–2 minutos o site abre em `https://SEU-USUARIO.github.io/controle-epi/`.

## Opção C — Cloudflare Pages (gratuito, permite restringir quem acessa)
1. Crie conta em cloudflare.com → **Workers & Pages → Create → Pages → Upload assets**.
2. Dê um nome ao projeto, envie a pasta `deploy` (ou o .zip) e clique em **Deploy**.
3. O site abre em `https://nome.pages.dev`.
4. (Opcional) Em **Zero Trust → Access**, crie uma regra para que só e-mails autorizados abram o site.

## Opção D — Hospedagem tradicional (cPanel/FTP)
1. Envie o conteúdo da pasta `deploy` para `public_html` (ou subpasta) pelo Gerenciador de Arquivos ou FTP.
2. Ative o certificado SSL gratuito (AutoSSL/Let's Encrypt) e force o redirecionamento para https.

## Domínio próprio (opcional)
Netlify: **Domain management → Add a domain**. Cloudflare Pages: **Custom domains**. GitHub Pages: **Settings → Pages → Custom domain**. Em todos, siga o passo de apontar o DNS (CNAME) e aguarde o HTTPS ser emitido.

## Teste logo após publicar (5 minutos)
1. Abra o endereço em uma aba anônima: deve aparecer **Crie seu acesso**.
2. Crie a conta, leia o guia e clique em **Entendi**.
3. Cadastre um funcionário de teste, assine a ficha e registre 2 EPIs com uma assinatura.
4. Abra **Visualizar ficha de EPI** e clique em **Exportar PDF** e **Imprimir**.
5. Digite um CA no cadastro de EPI (ex.: 10572) e confira que o nome é preenchido sozinho. Em **⚙ Configuração**, veja a data da base do CAEPI que já vem no sistema.
6. Baixe um backup. Depois apague o funcionário de teste só se ele não tiver EPI (ou restaure o backup limpo).

## Coisas importantes
- **Os dados ficam no navegador de cada pessoa**, por endereço (domínio). Trocar de endereço ou de aparelho começa do zero. Use **Configuração → Baixar backup** e **Restaurar backup** para mover dados.
- **Contas e dados são por navegador**: cada aparelho tem as próprias contas e os próprios funcionários. Não há lista compartilhada entre pessoas.
- **O login é uma barreira local**, não uma proteção de servidor. Quem tem o link pode criar conta. Para restringir o acesso à página, use Cloudflare Access (opção C).
- **A base do CAEPI já vem dentro do sistema** (42.474 CAs, dados do Ministério do Trabalho de 12/10/2026). O nome do EPI, a validade e a situação do CA são preenchidos pelo número do CA sem precisar importar nada. A consulta ao consultaCA por conector só funciona dentro do claude.ai; no site hospedado vale a base embutida.
- **Atualização da base do CAEPI**: situação e validade mudam com o tempo. Baixe o arquivo novo no site do Ministério do Trabalho e use **Configuração → Atualizar base do CAEPI** de tempos em tempos (a base atualizada fica salva no navegador de quem importou; **Voltar à base padrão** desfaz). Para trocar a base padrão para todos, peça uma nova versão do pacote.
- **LGPD**: o sistema guarda nome, matrícula e assinatura de funcionários no aparelho de quem usa. Defina quem pode usar, oriente a não usar computadores compartilhados sem sair da conta (botão de saída no topo) e faça backup periódico.
- **Validade jurídica**: o registro é eletrônico simples, com data e hora do aparelho. Para reforço de prova, exporte o PDF e arquive (de preferência também impresso e assinado).
