# Sala de Medicação

Simulador para técnicos de enfermagem, feito para jogar no celular em pé (no computador, aparece numa moldura de celular). O jogador confere o paciente, prepara a medicação, faz a punção e administra.

Para jogar, abra o `index.html` num navegador. Para publicar, ative o GitHub Pages na branch `main`.

## Procedimentos

- **Soroterapia**: conferência, equipo sem ar, punção e gotejamento.
- **EV em seringa**: diluição na sala de preparo, punção e injeção lenta.
- **EV em bolsa**: medicação diluída em soro, com gotejamento.
- **Intramuscular**: reconstituição, troca de agulha, local, ângulo e injeção lenta.
- **Plantão misto**: 3 procedimentos diferentes, sorteados.

## Níveis

- **Treino**: mostra o passo atual, destaca o que tocar e bloqueia escolhas erradas.
- **Prática**: mostra só a fase. A dica custa 2 pontos e passos fora de ordem custam 2.
- **Prova**: não mostra roteiro.

## Como jogar

- Toque num material para pegar e toque no lugar onde vai usá-lo.
- Nos minijogos (aspirar, puncionar, injetar), arraste os círculos azuis devagar.
- Cada caso vale 100 pontos. Cada erro tira pontos na hora, com som, vibração e a tela piscando, e o resumo explica cada erro.
- Durante o caso, consultar a tabela de preparo custa 5 pontos.

## Tecnologia

Um único `index.html` com Phaser 3.80.1 (via CDN) e fontes do Google Fonts. Os sons são gerados com WebAudio, sem arquivos de áudio. O recorde e as preferências (som e tutorial visto) ficam no `localStorage` do navegador.

## Aviso

O preparo segue a tabela da unidade. Antes de usar em sala, valide o conteúdo com o enfermeiro responsável técnico e com a farmácia. A prescrição médica e o protocolo da instituição sempre prevalecem.
