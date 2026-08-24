# Luana Toledo — Arquitetura e Design de Interiores

Site institucional de página única. HTML, CSS e JavaScript puros, sem dependências
e sem etapa de build: basta servir a pasta.

## Rodar localmente

```sh
python3 -m http.server 8899
```

Abra <http://localhost:8899>.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `index.html` | Todas as seções da página |
| `styles.css` | Estilos e paleta (variáveis CSS no `:root`) |
| `script.js` | Menu mobile, filtro de projetos, lightbox e envio do formulário |
| `assets/hero/` | Banner do primeiro bloco (desktop e mobile, `.jpg` + `.webp`) |
| `assets/projetos/` | 11 projetos, 100 fotos no total |
| `assets/luana.jpg` | Retrato usado na seção "A arquiteta" |
| `assets/logo*.png`, `assets/marca*.png` | Logo e símbolo com fundo transparente |

As imagens originais enviadas pela cliente não são versionadas (ver `.gitignore`);
`assets/` contém as versões já redimensionadas que o site usa.

## Paleta

Extraída da logo (`logo.jpg`) por amostragem de pixel:

| Variável | Cor | Uso |
|---|---|---|
| `--logo` | `#61371F` | marrom da logo — filtro ativo, selos |
| `--nude` | `#D0AA97` | nude da logo — acento sobre fundo escuro |
| `--noite` | `#2B180E` | fundos escuros (processo, rodapé, lightbox) |
| `--marrom` | `#3E2415` | bloco de contato |
| `--terra` | `#8A5233` | acento sobre fundo claro |
| `--papel` | `#F8F3ED` | fundo padrão |

Todos os pares de texto/fundo passam de 4,5:1 de contraste (WCAG AA).

## Galerias

Cada projeto é um `<figure class="obra">` com:

- `data-fotos` — array JSON com o caminho de todas as fotos, na ordem do carrossel
- `data-antes` — quantas fotos do **final** do array são do estado original.
  O lightbox marca essas com o selo "Antes", e a capa ganha o selo "Antes e depois".

Para trocar a capa de um projeto, basta substituir o `cover.jpg` da pasta
(recorte 4:5, 1000×1250).

## Atendimento

Não há espaço físico. O site não exibe endereço nem link de mapa: a referência é
"Taubaté/SP · Vale do Paraíba e on-line para todo o Brasil", no bloco de contato
e no rodapé. A cidade também está no `<title>` e na `meta description`, que é o
que sustenta a busca local sem um endereço cadastrado.

## Dados estruturados

O `index.html` traz um bloco `application/ld+json` do tipo `ProfessionalService`
que liga o site ao Perfil da Empresa no Google: telefone, horário, áreas de
atendimento e os quatro serviços. Como não há endereço público (empresa com
área de atendimento), o `address` fica só em cidade/estado e o alcance real
é declarado em `areaServed`.

Ao editar, mantenha telefone, horário e nome **idênticos** ao que aparece no
Perfil da Empresa e no rodapé. Divergência entre as três fontes enfraquece o
sinal local. Validar em <https://search.google.com/test/rich-results>.

## Publicação

No ar em <https://luanaarq.vercel.app/>, com deploy automático a cada push
no `main`.

O domínio aparece em quatro lugares do `index.html`, todos no `<head>`:

| Onde | Por quê |
|---|---|
| `<link rel="canonical">` | evita conteúdo duplicado entre domínios |
| `og:url` e `og:image` | prévia ao compartilhar no WhatsApp e Instagram |
| `url`, `@id`, `logo`, `image` no JSON-LD | identidade da empresa para o buscador |

Ao migrar para o domínio próprio, troque nos quatro e mantenha o antigo
redirecionando com 301 para não perder o que já foi indexado.

`og:image` precisa de URL **absoluta**: com caminho relativo as redes sociais
não carregam a imagem da prévia.

## Search Console

O domínio é um subdomínio do Vercel, então **não dá para criar propriedade
do tipo "Domínio"** — esse tipo exige registro TXT no DNS, e o DNS de
`vercel.app` é da Vercel. Use propriedade **"Prefixo do URL"**, com
`https://luanaarq.vercel.app/`, verificada por arquivo HTML na raiz ou por
meta tag no `<head>`.

`robots.txt` e `sitemap.xml` estão na raiz. Ao trocar de domínio, atualize
a URL nos dois.

## Analytics

O site **não tem** nenhuma ferramenta de medição instalada. O container do
Google Tag Manager que veio junto com a estrutura reaproveitada era de outro
cliente e foi removido. Para medir acessos, criar um container ou uma
propriedade do GA4 no nome da Luana e instalar do zero.

## Ainda a preencher

- **Nome no Perfil da Empresa** — o JSON-LD declara "Luana Toledo Arquitetura".
  Se o perfil usar outro nome, alinhar os dois.
- **CAU** — o registro não está no rodapé. Se quiser exibir, incluir em
  `.rodape__legal` no `index.html`.

O WhatsApp está configurado: `5512991581917`, definido em `script.js` e nos
links do `index.html`.

## Formulário de contato

Não envia e-mail. Ele monta a mensagem e abre o WhatsApp com o texto pronto,
por isso não exige servidor. Para receber por e-mail, seria preciso plugar um
serviço externo.
