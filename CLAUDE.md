# CLAUDE.md

Orientações para trabalhar neste projeto.

## O que é

Landing page de conversão para venda de embalagens descartáveis (marmitas EPS,
copos, potes, kraft, talheres, sacolas) em **Maringá-PR e região**. O objetivo
único da página é levar o visitante a **fazer o pedido no site** ou **falar no
WhatsApp**.

## Estrutura

- [index.html](index.html) — a landing page. Arquivo único e autocontido: HTML,
  CSS e JS na mesma página, sem build, sem dependências instaladas.
- [index_exemplo.html](index_exemplo.html) — referência visual (landing de uma
  barbearia) usada como base para o repertório de efeitos de scroll. **Não é a
  página do cliente e não deve ser editada nem publicada.**

- `tabela de produto.xls` — export do ERP do cliente (621 itens, 82 marcas), a
  fonte das marcas citadas no catálogo e na faixa de logos. Tem preço de custo e
  estoque, então está no `.gitignore`: **não comitar.**

Não há package.json, build step ou servidor. Para ver o resultado, basta abrir
`index.html` no navegador.

## Convenções

- **Português do Brasil** em todo o conteúdo, comentários e nomes de classe
  quando fizer sentido.
- **Sem dependências externas de código.** Fontes vêm do Google Fonts; imagens
  vêm do Unsplash via URL direta (`images.unsplash.com/photo-...`). Nada de CDN
  de JS/CSS.
- **CSS organizado por seção** com faixas de comentário (`/* ===== hero ===== */`).
  Ao adicionar uma seção, siga o mesmo padrão e mantenha a ordem do CSS igual à
  ordem das seções no HTML.
- **Tema claro único**, deliberado. Todas as cores saem das variáveis em
  `:root` (`--paper`, `--ink`, `--ember`, `--butter`, `--leaf`). Não introduza
  cores literais fora desse conjunto.
- **Tipografia:** Bricolage Grotesque (títulos), Archivo (corpo), Archivo Black
  (números e marca).
- Toda animação precisa estar coberta pelo bloco
  `@media (prefers-reduced-motion: reduce)` no fim do CSS.

## Cuidados ao editar

- A regra genérica `section{max-width:1320px;margin:0 auto}` se aplica a todos
  os `<section>`. Seções full-bleed (como `.hero`) precisam de
  `max-width:none;margin:0` explícito, ou ficam encaixotadas no meio da tela.
- Ao trocar uma imagem, **verifique a URL antes** (`curl -o` + visualizar) — IDs
  de foto do Unsplash inventados retornam 404 silenciosamente e a página fica com
  buraco.
- O efeito de foto flutuante do catálogo (`.peek`) lê `data-img` de cada
  `.item`. Ao adicionar uma linha no catálogo, inclua o `data-img`.
- O menu mobile usa `clip-path: circle()` ancorado no canto superior direito. Se
  mudar o padding do header em telas pequenas, ajuste também as coordenadas do
  `clip-path` no media query correspondente.
- As logos da faixa `.marcas` são **data URI base64 embutidas** (PNG, 72px de
  altura, ~36KB no total) — não são URL externa como as fotos do Unsplash. Foi
  o que manteve o arquivo único e a faixa funcionando offline. Ao trocar uma
  logo: baixe do site do fabricante, corte a moldura vazia, redimensione para
  72px de altura e converta para base64. Fibraform e Darnel são logos "em
  caixa" (fundo sólido, quase quadradas) e sobem para 58px via
  `.logo img[alt="..."]` para equilibrar o peso óptico das demais.
- Publicar como Artifact quebra as imagens: o CSP do Artifact bloqueia hosts
  externos. Para publicar lá, seria preciso embutir as fotos como data URI.

## Dados do cliente

Já preenchidos na página:

- Cidade: Maringá-PR e região
- Endereço: Rua João Cardoso de Lima, 676 — Jardim Nilza
- Atendimento: segunda a sexta, 8h às 17h
- URL da loja / "Fazer pedido": `https://embalagem.columbia1.com.br/catalogo/online`

Ainda são **placeholders** e precisam ser trocados quando o cliente informar
(a lista também está no comentário no topo do `index.html`):

- WhatsApp: `5511900000000`
- E-mail: `contato@embalafacil.com.br`
- Nome da empresa: `EmbalaFácil`
- Números da prova social (atributos `data-count` na barra de estatísticas)
