# Sala de Medicação

Simulador para técnicos de enfermagem, feito para jogar no celular em pé; no computador usa a tela deitada: roteiro ou registro ao lado e, no soro, braço e suporte lado a lado. O jogador confere o paciente, prepara a medicação, faz a punção e administra.

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
- Para agitar o frasco reconstituído ou homogeneizar a bolsa, segure e chacoalhe (arraste de um lado para o outro). Ao injetar no frasco ou na bolsa, a seringa vai até lá e o êmbolo desce.
- Enquanto você segura um material, aparece a mão do profissional: com luva depois de calçá-las, sem luva antes.
- Nos minijogos (aspirar, puncionar, injetar), arraste os círculos azuis devagar. O ângulo e o bisel começam fora do lugar: ajuste antes de avançar.
- Cada gesto tem som: esfregar o álcool, puxar e empurrar o êmbolo, chacoalhar o frasco ou a bolsa, quebrar a ampola, calçar as luvas, as gotas caindo na câmara, o descarte no coletor.
- O paciente reage: geme e reclama quando a injeção é rápida ou a punção falha, e avisa quando o álcool está gelado.
- Na câmara do equipo, aperte em cima ou ao lado e acompanhe o medidor de nível.
- Cada caso vale 100 pontos. Cada erro tira pontos na hora, com som, vibração e a tela piscando, e o resumo explica cada erro.
- No gotejamento vale acertar o ritmo (lento, médio ou rápido), como no olhômetro do plantão. O número de gotas por minuto aparece só como referência.
- A tabela de preparo pode ser consultada a qualquer momento, sem custo.
- Nos frascos com pó, a tabela mostra quanto ABD usar para reconstituir e o que fazer depois (completar a seringa, injetar na bolsa ou aplicar IM). Um quadro no topo explica quando e como reconstituir.
- No computador: **Esc** solta o material da mão, **1**/**2** alternam braço e suporte, **T** abre a tabela e **P** a prescrição.
- O botão **‹ Menu** no topo encerra o plantão e volta ao início.

## Tecnologia

Versão atual: **v9.0**. Se o motor do jogo não carregar (sem internet), a página mostra um aviso com botão para tentar de novo.


Um único `index.html` com Phaser 3.80.1 (via CDN) e fontes do Google Fonts. Os sons são gerados com WebAudio, sem arquivos de áudio. O recorde e as preferências (som e tutorial visto) ficam no `localStorage` do navegador.

## Aviso

O preparo segue a tabela da unidade. Antes de usar em sala, valide o conteúdo com o enfermeiro responsável técnico e com a farmácia. A prescrição médica e o protocolo da instituição sempre prevalecem.
