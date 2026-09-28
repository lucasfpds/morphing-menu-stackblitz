# Menu de Navegação "Morphing"

> Botão hambúrguer que se transforma em menu full-screen com SVG path morphing e efeitos de máscara.

## Stack

- Vite + Vue 3 (`<script setup>`, JavaScript) — sem TypeScript, sem lint/test, zero libs extras
- CSS puro em `src/styles.css`
- Arquivos: `index.html`, `package.json` (deps: `vue`), `vite.config.js`, `.stackblitzrc`, `src/main.js`, `src/App.vue`, `src/styles.css`
- App.vue único — um boolean `aberto` controla tudo

## Implementação

### 1. Botão hambúrguer com morphing de path

- `<svg><path>` único: o hambúrguer desenhado como subpaths **com a mesma estrutura de comandos** do X (mesmo número/tipo de segmentos) — requisito para o morph fluir sem pulos
- Alternância por CSS:
  ```css
  path { transition: d 0.4s ease; d: path("… hambúrguer …"); }
  .aberto path { d: path("… X …"); }
  ```
- Suporte a `d` via CSS: Chrome/Edge/Safari e Firefox ≥ 97 — suficiente para o StackBlitz moderno

### 2. Menu full-screen com máscara

- Overlay `position: fixed; inset: 0` revelado por máscara circular saindo do botão:
  `clip-path: circle(0px at var(--x) var(--y))` → `circle(150% at var(--x) var(--y))`, com `transition: clip-path 0.5s`
- `--x`/`--y` = posição do botão (calculada no clique)
- Links grandes (nav fictícia) com entrada em cascata: `translateY(20px)` + `opacity`, um `transition-delay` incremental por item

### 3. Comportamento

- `aria-expanded` no botão; Esc fecha; `overflow: hidden` no body enquanto aberto
- Clique num link fecha o menu (demo: apenas fecha)

## Checklist — 100% da descrição

- [ ] Hambúrguer ↔ X via SVG path morphing
- [ ] Menu full-screen revelado por máscara circular animada
- [ ] Links com entrada em cascata
- [ ] Fechar por Esc / botão / link
