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

- **Treino**: mostra o passo atual, destaca o que tocar e avisa na hora quando você pega algo errado.
- **Prática**: mostra só a fase. A dica custa 2 pontos. Só perde pontos quem inverte uma ordem que importa (ex.: puncionar antes de garrotear); pegar materiais, testar/fixar o acesso, descartar/etiquetar podem ser feitos em qualquer ordem.
- **Prova**: não mostra roteiro.

## Como jogar

- No leito, toque num material da gaveta e depois no lugar onde vai usá-lo, ou arraste-o direto até lá. O álcool pode ser arrastado até a pele e esfregado sem soltar. Mandril, ponta do equipo e seringa usada também podem ser arrastados até o destino.
- Na sala de preparo, arraste para a bancada o que vai usar. Pegou errado ou demais? Arraste de volta para a prateleira. Só perde pontos o que for esquecido na bancada ao sair.
- Nos minijogos (aspirar, puncionar, injetar), arraste os círculos azuis devagar.
- Cada caso vale 100 pontos. Cada erro tira pontos na hora, com som, vibração e a tela piscando, e o resumo explica cada erro.
- No gotejamento vale acertar o ritmo (lento, médio ou rápido), como no olhômetro do plantão. O número de gotas por minuto aparece só como referência.
- A tabela de preparo pode ser consultada a qualquer momento, sem custo.
- O botão **‹ Menu** no topo encerra o plantão e volta ao início.

## Tecnologia

Um único `index.html` com Phaser 3.80.1 (via CDN) e fontes do Google Fonts. Os sons são gerados com WebAudio, sem arquivos de áudio. O recorde e as preferências (som e tutorial visto) ficam no `localStorage` do navegador.

## Aviso

O preparo segue a tabela da unidade. Antes de usar em sala, valide o conteúdo com o enfermeiro responsável técnico e com a farmácia. A prescrição médica e o protocolo da instituição sempre prevalecem.
