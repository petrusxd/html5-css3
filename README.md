<h1 align="center">HTML5 + CSS3 é uma Linguagem de Programação</h1>

<p align="center">
  <strong>Uma prova interativa — 100% HTML5 + CSS3, zero JavaScript.</strong><br>
  Variáveis, funções, condicionais, loops, lógica booleana, aritmética e
  computação Turing-completa, rodando no motor de CSS do navegador.
</p>

<p align="center">
  <img alt="HTML5" src="https://img.shields.io/badge/HTML5-only-E34F26?logo=html5&logoColor=white">
  <img alt="CSS3" src="https://img.shields.io/badge/CSS3-only-1572B6?logo=css3&logoColor=white">
  <img alt="JavaScript" src="https://img.shields.io/badge/JavaScript-0%20linhas-success">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue">
</p>

---

## O que é

Um site com **três abas** (navegação pura, via `radio` + `:checked`) que demonstra,
na prática, que HTML5 e CSS3 sozinhos satisfazem os critérios de uma linguagem de
programação.

### 1. A Prova — 8 demonstrações
| # | Conceito | Mecanismo |
|---|----------|-----------|
| 01 | Variáveis tipadas | `@property` + custom properties + `calc()` |
| 02 | Funções | `@function` |
| 03 | Decisão (if/else) | `if()` nativo e `:checked` |
| 04 | Loops | `@keyframes` (while) + `counter-*` (for) |
| 05 | Lógica booleana | AND/OR/XOR/NAND/NOR/NOT via seletores |
| 06 | Aritmética | full-adder de 1 bit (Soma = A⊕B⊕Cin, Carry = maioria) |
| 07 | Turing-completude | autômato celular **Rule 110** |
| 08 | Máquina de estados | semáforo (FSM) com `@keyframes` |

### 2. Aplicação — To-Do funcional
Concluir, excluir, filtrar (Todas / Ativas / Concluídas) e **contador reativo** ao
vivo, com `:has()`, combinadores e `counters`.

### 3. Calculadora — funcional, de teclado único
Fluxo real: **dígito(s) → operação → dígito(s) → resultado**, com entrada
**simétrica de comprimento variável: 1 a 3 dígitos** em cada número (0–999).
Seis operações (`+  −  ×  ÷  mod  xʸ`): soma e subtração por **counters
posicionais reais**, multiplicação por **produtos parciais**
(`(Σ A_i·10^(m-1-i))·(Σ B_j·10^(n-1-j))`) e ÷/mod/^ por **tabela exata** no
subdomínio enxuto A∈0..99, B∈0..9 (com bignum exato em potências). Botão **C** =
reset nativo do `<form>`. O teclado único é uma **máquina de estados em CSS**
(`:has()`) com comprimento variável — a operação **fecha** o número atual, em
qualquer comprimento. O gerador da tabela é **autoverificável**: simula todos
os counters em Python antes de emitir o CSS, falhando se divergir.

### 4. Projetos — Wizard, BIT-4, Pomodoro, Pixel-Art, BF-MINI, MAZE, STACK-RPN, TTT-IA
Aba com **oito projetos** em abas menores:
- **Wizard:** navegação de estado sequencial.
- **BIT-4:** CPU fictícia de 4 bits — controle de ciclo (fetch, decode, execute),
  traçador de estado (trace) e saída visual.
- **Pomodoro:** temporizador 25/5 min — FSM de ciclo, animação sincronizada com
  `:checked` e display de minutos via ROM/tabela.
- **Pixel-Art:** editor 8×8 pixels com 4 cores (vermelho, verde, azul, preto) —
  paleta selecionável, grade interativa, pintura local sem ROM (cada célula é
  independente).
- **BF-MINI:** interpretador de subconjunto Brainfuck — ponteiro de instrução,
  ponteiro de dados, fita de 4 células × 3 bits. 4 comandos: `+`, `-`, `>`, `<`.
  Trace pré-computado de 9 steps; cliques em ▶ avançam a execução; células
  destacam DP; instruções destacam IP. C reinicia.
- **MAZE:** labirinto 7×7 — grafo 4-conectado com 33 vértices caminháveis.
  BFS pré-computa 25 pares (origem, destino); caminho ótimo highlighted via
  `:has(#src_S:checked):has(#dst_D:checked) .cell-K`. Modo Origem/Destino
  controla qual label recebe `pointer-events: auto`. Fronteira honesta: espaço
  completo (1089 pares) geraria ~1.5 MB; 25 pares selecionados = ~23 KB;
  pares fora do subconjunto exibem aviso. C reinicia.
- **STACK-RPN:** calculadora RPN de dois operandos (`a, b ∈ {0..9}`, operações
  `+`, `−`, `×`). FSM de modo (`name="rpn-mode"`) alterna entre entrada do
  primeiro e do segundo operando; ROM de 300 resultados em `css/rpn-ops.css`
  exibe o resultado via seletor composto `:has(#rpn-a:checked):has(#rpn-b:checked)`.
  Pilha visual de 4 linhas. Fronteira honesta: sem encadeamento (read-modify-write
  não é expressável em CSS). C reinicia.
- **TTT-IA:** Jogo da Velha contra IA minimax — tabuleiro 3×3, 9 células ternárias
  (∅/X/O). ROM de 2097 estados em `css/ttt-ai.css` mapeia cada posição onde é a vez
  de O ao movimento ótimo via `pointer-events: auto; z-index = nº peças`. O nunca
  perde. Fronteira honesta: sem enforcement de turno. C reinicia.

---

## Uso

Abra `index.html` no navegador. Sem build, sem servidor, sem dependências.

Recomendado um navegador atual. Para `@function` e `if()` nativos, Chrome/Edge 139+
(os recursos novos têm fallback via `@supports`). To-Do e Calculadora usam `:has()`.

---

## Como funciona

O estado vive nos `<input>`; a lógica vive nos seletores CSS.

- **Decisão:** `#porta:checked ~ .saida::after { content: "LIBERADO" }`
- **Loop/contagem:** `counter-increment` + `counter()`
- **Lógica booleana:** `#a:checked ~ #b:checked ~ .and` acende um AND
- **Máquina de estados:** `:has()` no ancestral que contém os inputs
- **Aritmética:** soma/subtração por `counters` (valor posicional), multiplicação por
  produtos parciais, e ÷/mod/^ por tabela de decisão exata
- **Turing-completude:** Rule 110 (Cook, 2004) computado célula a célula por seletores

---

## Estrutura

```
index.html                       documento único, múltiplas abas
css/style.css                    lógica e estilo base
css/calc-table.css               aritmética da calculadora
css/wizard.css                   navegação sequencial
css/bit4.css                     CPU fictícia BIT-4
css/bit4-trace.css               traçador do BIT-4
css/pomodoro.css                 temporizador Pomodoro (FSM, animações)
css/pomodoro-rom.css             ROM/display do Pomodoro
css/pixel.css                    editor pixel 8×8 com 4 cores
css/bf.css                       interpretador BF-MINI (layout, fita, FSM)
css/bf-trace.css                 trace do interpretador BF-MINI
css/maze.css                     labirinto MAZE (layout, modo FSM)
css/maze-paths.css               ROM de caminhos MAZE
css/rpn.css                      calculadora STACK-RPN (layout pilha, teclado FSM)
css/rpn-ops.css                  ROM de operações STACK-RPN
css/ttt.css                      Jogo da Velha TTT-IA
css/ttt-ai.css                   ROM de movimentos ótimos TTT-IA
```

---

## Referências

- [MDN — `if()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/if)
- [Chrome for Developers — CSS conditionals `if()`](https://developer.chrome.com/blog/if-article)
- [MDN — `@function`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@function)
- [W3C — CSS Functions and Mixins Module L1](https://www.w3.org/TR/css-mixins-1/)
- [W3C — CSS Values and Units Module L5](https://www.w3.org/TR/css-values-5/)
- [MDN — `@property`](https://developer.mozilla.org/en-US/docs/Web/CSS/@property)
- M. Cook (2004), *Universality in Elementary Cellular Automata* — Rule 110.

---

## Licença

[MIT](LICENSE) © Petrus
