# Vetoriza.

Traçado de imagem no navegador — converta PNG/JPG/WEBP em SVG com qualidade Potrace, com controles no espírito do *Image Trace* do Illustrator. 100% client-side: nenhuma imagem sai do seu computador.

## Como funciona

O motor combina três etapas, a mesma arquitetura de vetorizadores profissionais:

1. **Quantização de cores** — median cut sobre os pixels opacos, com fusão automática de tons quase iguais (logos de 1 cor viram 1 camada, sem chuvisco entre tons).
2. **Máscaras empilhadas** — cada cor gera uma máscara binária cumulativa; camadas maiores ficam embaixo, eliminando frestas entre cores adjacentes.
3. **Potrace (WASM)** — cada máscara é traçada pelo Potrace, o algoritmo de referência para bitmap→Bézier, com controle de cantos (`alphamax`), simplificação (`opttolerance`) e ruído (`turdsize`).

A transparência do original é preservada no SVG.

## Funcionalidades

- Upload por clique ou arrastar-e-soltar
- Modos: Cor, Tons de cinza e Preto & branco (com limiar)
- Reamostragem automática (imagens pequenas são ampliadas antes do traçado → curvas suaves)
- Anti-halo: binariza o canal alfa para não contaminar a paleta com o serrilhado das bordas
- Paleta detectada exibida em tempo real
- Comparador antes/depois com divisor arrastável
- Download do `.svg` nas dimensões originais, ou cópia do código

## Como usar

Abra `index.html` no navegador. Sem build, sem dependências, sem servidor.

## Publicar no GitHub Pages

1. Crie um repositório e envie estes arquivos
2. Em **Settings → Pages**, selecione *Deploy from a branch* → `main`, pasta `/ (root)`
3. O app fica em `https://SEU-USUARIO.github.io/NOME-DO-REPO/`

## Dicas

| Tipo de imagem | Preset |
|---|---|
| Logo / lettering | **Logo / marca** |
| Ilustração flat | **Pôster / flat** |
| Foto | **Alta fidelidade** (SVG de foto sempre pesa) |
| Assinatura, nanquim | **Traço técnico** ou **Silhueta** |

## Créditos e licença

- Motor: [Potrace](https://potrace.sourceforge.net/) © Peter Selinger, via [esm-potrace-wasm](https://github.com/tomayac/esm-potrace-wasm) (Thomas Steiner) — **GPL-2.0**, empacotado em `lib/potrace.js`
- Por depender do Potrace, este projeto é distribuído sob **GPL-2.0** (veja `LICENSE`)
