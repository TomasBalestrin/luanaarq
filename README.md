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

## Ainda a preencher

- **CAU** — o registro não está no rodapé. Se quiser exibir, incluir em
  `.rodape__legal` no `index.html`.

O WhatsApp está configurado: `5512991581917`, definido em `script.js` e nos
links do `index.html`.

## Formulário de contato

Não envia e-mail. Ele monta a mensagem e abre o WhatsApp com o texto pronto,
por isso não exige servidor. Para receber por e-mail, seria preciso plugar um
serviço externo.
