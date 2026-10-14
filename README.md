# Menu de Navegação Morphing

> Botão hambúrguer que se transforma em menu full-screen com SVG path morphing e efeitos de máscara.

## Tecnologias

- **Vue 3** com `<script setup>` (JavaScript)
- **Vite** como bundler
- **SVG path morphing** via CSS `d: path()` com `transition`
- **clip-path: circle()** para máscara circular animada
- **CSS puro** — sem pré-processador

## Requisitos

- Node.js 18+

## Como executar

```bash
npm install
npm run dev
```

Abra http://localhost:5173 no navegador.

## Scripts

| Script | Descrição |
| --- | --- |
| `npm run dev` | Servidor de desenvolvimento (Vite) |
| `npm run build` | Build de produção |
| `npm run preview` | Serve o build de produção |

## Estrutura

```
src/
  main.js              entry: cria o app e importa o CSS
  App.vue              botão hambúrguer, overlay, menu, links em cascata
  styles.css           botão, path morph, overlay, clip-path, links
```

### Funcionalidades

- Botão hambúrguer desenhado como subpaths SVG com a mesma estrutura de comandos do X (mesmo número/tipo de segmentos) — o morph flui sem pulos
- Alternância por CSS: `path { transition: d 0.4s ease }`
- Menu full-screen revelado por máscara circular: `clip-path: circle(0px → 150%)` saindo da posição do botão
- `--x`/`--y` = posição do botão calculada no clique
- Links grandes com entrada em cascata: `translateY(20px)` + `opacity`, `transition-delay` incremental
- `aria-expanded` no botão; Esc fecha; `overflow: hidden` no body enquanto aberto
- Clique num link fecha o menu


## Rodando no StackBlitz

Basta importar o repositório e rodar normalmente:

```
https://stackblitz.com/github/lucasfpds/morphing-menu-stackblitz
```

O projeto não depende de binários nativos — Vite é JavaScript puro, então
sobe sem bindings nativos no WebContainer do StackBlitz.
