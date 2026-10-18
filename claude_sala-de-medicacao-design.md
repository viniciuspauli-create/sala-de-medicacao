# Sala de Medicação — design (v9.1, mobile em retrato + layout próprio no PC)

> **Estado (17/out/2026):** `claude/sala-de-medicacao-index.html` = **v8.8 (v8.7 polida + sons de procedimento)**, publicada no artifact "Sala de Medicação" (https://claude.ai/artifact/GXmqm8cxJfBWhuc4aT1a86). O GitHub `main` tem a v8.2 (`400078a`); a v8.8 aguarda upload manual do `index.html`. Link do Pages: https://viniciuspauli-create.github.io/sala-de-medicacao/

Público: técnico de enfermagem. Stack: Phaser 3.80.1 (2D), canvas 720×1120 em retrato; prescrição fixa, cartão de objetivo e roteiro em HTML acima do canvas.

## Decisões (out/2026)
- Foco mobile, tela em pé; no computador vira moldura de celular.
- **Toda interação aceita toque OU arraste.** Leito: tocar no material da gaveta e depois no destino, ou arrastar direto (álcool arrastado até a pele já começa a esfregar; cateter arrastado até a veia abre o seletor e punciona ali). Garrote, mandril, ponta do equipo e seringa usada também arrastáveis. Réguas de ângulo e do gotejamento: tocar/arrastar em qualquer ponto.
- Sala de preparo: tocar ou arrastar. Pegar errado ou a mais é permitido; devolve-se arrastando para a prateleira (ampola aberta → coletor). **Só penaliza o que fica esquecido na bancada ao sair** (item errado −3, excedente −2). No Treino, sair com sobra é bloqueado com aviso.
- **A ordem só conta quando importa.** Roteiro com dependências: grupos sem ordem (pegar materiais; testar/fixar; descartar/etiquetar/homogeneizar/agulha IM; algodão/coletor) e cadeias paralelas (preparo do soro × punção). "Fora de ordem" (−2) só quando falta uma dependência real; higiene/luvas têm nota própria. No Treino a câmera só troca de vista (braço/suporte) quando não há passo na vista atual.
- **Gotejamento no "olhômetro"**: cobra-se o ritmo (lento/médio/rápido). Macrogotas <40 / 40–62 / >62 gts/min; microgotas <120 / 120–186 / >186. Acerto = mesma faixa ou até 10% do cálculo; faixa vizinha −6, oposta −10. Número só como referência; no Treino, marca "prescrição" na régua.
- **Cor do cateter** visível: etiqueta "na mão" com a cor, ícone da gaveta muda para o calibre escolhido, identificação colorida junto ao acesso após a fixação.
- Avisos (toasts) no leito do soro ficam abaixo das abas Braço/Suporte (`placeToasts`).
- Tabela de preparo grátis. Botão **‹ Menu** com confirmação.
- **Tabela com reconstituição (v8.5)**: cada frasco em pó mostra "frasco · pó" e dois passos (reconstituir com X ml de ABD e agitar; depois completar a 20 ml / injetar na bolsa / volume final IM). Quadro no topo: quando e como reconstituir. Números vindos de `reconMl` (`recon`, `reconB`, `im.vol`), os mesmos que o jogo cobra.
- **v8.6 (feedback do autor):**
  - Com Tabela/prescrição/roteiro abertos, o jogo não recebe toques (`syncInput` desliga `GAME.input.enabled`; o Phaser escuta mouseup/touchend na janela inteira e repassava o toque).
  - **Chacoalhar**: frasco reconstituído (agitar) e bolsa com medicação (homogeneizar) só se completam segurando e arrastando de um lado para o outro (6 vaivéns, barra de progresso); tocar só mostra a instrução. `shakeOn(C,canShake,done)`; soltar depois de chacoalhar não devolve o item à prateleira (`C._shook`).
  - **Animação de injeção** (`injAnim`): a seringa vai até a bolsa (de lado) ou até o frasco (de cima), o êmbolo desce e gotas entram; bloqueia toques durante (`_anim`).
  - **Paciente reage**: `groan()` (gemido sintetizado, mais agudo se mulher) + `say()` (balão): injeção rápida ("Ai! Mais devagar…"), punção perdida e agulha IM fora do músculo ("Ai! Doeu!"), álcool ("Tá gelado!", uma vez por caso), injeção lenta ("Nem senti.").
  - **Câmara do equipo**: área de toque 320×260 em volta (aperta ao lado), medidor "nível" à esquerda para o dedo não esconder; ponta do equipo deixa de ser tocável depois de perfurar.
  - **Ângulo inicial aleatório**: punção começa fora de 13–32° e o bisel às vezes para baixo; IM começa entre 15° e 64°.
  - **Mão do profissional** (`nurseHand`/`handUpdate`/`handPos`): aparece segurando o material selecionado ou arrastado (com luva azul-clara depois das luvas; sem luva antes e na sala de preparo), segura o algodão ao esfregar e "pega" objetos arrastados. Na gaveta, o fantasma do arraste fica invisível e a mão leva o item (`useHand`, `_ghostKey`).
  - **Crianças: testadas e retiradas a pedido** (fórmulas diferentes confundiriam). Não reintroduzir sem tabela pediátrica da unidade.
- **v8.7 (polimento final):**
  - Código morto removido (minijogos da versão paisagem, texturas não usadas como prepBg/clip/poster/pole/wrist/crossIM/armBg/proneBg, PAC, funções duplicadas): ~10% menor e boot mais rápido.
  - Tela "Preparando a sala…" enquanto o jogo carrega; se o Phaser não carregar (sem internet), aviso com botão "Tentar de novo" em vez de tela branca. Tempo do caso começa quando a cena aparece.
  - Canvas reajusta quando o cartão de objetivo muda de altura (`fit`: ResizeObserver + MutationObserver em `#objCard`, refresh no quadro seguinte e de novo após 250 ms). Celulares baixos (≤720 px de altura) usam topo compacto e cabem sem rolar.
  - Sala de preparo do soro: rótulos das bolsas/equipos não invadem a prateleira; nome dentro da bolsa encolhe para caber (`fitW`); bolsas guardam `o.sol`/`o.vol`.
  - Mão do profissional fica acima do aviso "Na mão" (`handPos` → DRAWER_Y-190). Punção: título/instruções sempre visíveis sobre o cateter; rótulos 5°/60° e 10°/90° fora do botão.
  - Toque no celular: sem realce azul, sem lupa/menu ao segurar, sem zoom em toque duplo. Ícone, descrição e metas de app. Pontos escondidos no menu inicial; tag "novo" virou "sorteados"; versão no rodapé.
  - Robô: 15 rodadas (5 modos × Treino/Prática/Prova + frascos com pó forçados) = 45 casos com 100 pontos e zero erros de console; punção testada com mouse real.
- **v8.8 (sons de procedimento):** motor `nz()` (ruído filtrado) + `tn()` (tom) + `SND`/`snd(k,gap,arg)` com intervalo mínimo por som; respeita o botão de som. Sons: esfregar álcool (`rub`, braço e IM), aspirar (`suck`, mais agudo conforme enche; `air` quando acaba o conteúdo), empurrar o êmbolo (`push`, mais forte quando rápido), chacoalhar (`slosh` + `tink` de vidro no frasco), quebrar ampola (`crack`), lacre/perfurar bolsa/agulha entrando (`pop`), luvas e garrote (`snap`), lavar as mãos (`water`), gota na câmara (`drip`, só na vista do suporte), aperto da câmara (`squeeze`), coletor (`clunk`), curativo/etiqueta (`rip`), encaixes e rolete (`click`), gancho (`clink`), líquido entrando no frasco/bolsa (`stream`).
  - IM: arrastar o álcool da gaveta e esfregar já funcionava; corrigido o local escolhido — agora conta os vaivéns por local e fica com o mais esfregado (antes pegava o primeiro ponto que o dedo cruzava no caminho, ex.: dorsoglúteo em vez de ventroglúteo).
- **v8.9 (feedback do Vini, 17/out):**
  - Mandril: com o mandril na mão, o garrote pode ser solto (`solta` aceita `sel==='mandril'`); tocar no mandril de novo solta-o; aviso explica a ordem se o garrote ainda estiver apertado. Antes travava no Treino (coletor recusava e o garrote ignorava o toque).
  - Câmara: área de toque 300×170 (antes 320×260) e só ativa entre perfurar e encher (`chZ.input.enabled`). Antes cobria o topo do rolete e impedia "Feche o rolete".
  - Legibilidade: fontes maiores na conferência (pulseira/ficha com `fitW`), preparo (medicamentos, seringas, agulhas sem a palavra "agulha", equipos, bancada), abas e gaveta (ícones ~15% maiores) e topo HTML. Aumento global testado e descartado (encavalava a conferência).
  - Bolsas por volume: `BAG_SC` (100 .62 · 250 .8 · 500 .98 · 1000 1.18) na prateleira, bancada e suporte; no suporte a saída fica fixa em y=330 e uma alça liga a bolsa ao gancho.
  - Computador (≥1000 px, deitado): grid com coluna esquerda (prescrição, passo, `#side` com roteiro sempre aberto no Treino e atalhos) e cena na altura toda (`aspect-ratio:720/1120`). Atalhos: Esc solta o material, 1/2 braço/suporte, T tabela, P prescrição. Menu em 2 colunas.
  - Robô: rolete fechado com mouse real, câmara ao lado, equipo sem ar, mandril com garrote apertado (pegar, soltar, soltar garrote, descartar) em 390×844 e 1440×900; atalhos; capturas em 1280×720 e 1920×1080. Zero erros de console.
- **v8.10 (nitidez):** o canvas desenha em `RES`× (1–2, conforme densidade e tamanho da tela) sem mudar as coordenadas do jogo: `hiResGL` embrulha o contexto WebGL num Proxy que multiplica `viewport`/`scissor` do quadro principal e devolve `drawingBuffer*` em 720×1120; textos com `resolution:RES`. Toque, posições e cenas inalterados; sem WebGL cai no modo normal. **v8.11:** imagens SVG também em `HIRES`× (`svgTex` gera em HIRES× e o quadro volta ao tamanho lógico com `setSize(w,h)` + `setUVs(...,0,0,1,1)`), então ícones da gaveta e materiais ficam nítidos sem mudar tamanhos. `HIRES` só >1 quando o Proxy WebGL está ativo. Ficha: "FOTO DO CADASTRO" → "FOTO".
- **v9.0 (feedback: PC na horizontal e paciente errado):**
  - Paciente errado = outra pessoa (`issue:'outro'`, `otherPatient`): no leito e na pulseira está alguém com outro nome, outro sobrenome, ≥8 anos de diferença e aparência diferente; ficha e prescrição são do paciente certo. Sumiram as pegadinhas de nome parecido, data trocada e só foto diferente. Alergia como divergência continua.
  - PC em tela larga (fase 1): canvas por cena via `setW(scene,w,h)` (`GAME.scale.setGameSize` + `--ar/--arn` no `.gstage`; o Proxy WebGL acompanha o tamanho). Conferência 1440×640 (paciente à esquerda, ficha e botões à direita, deslocando os objetos criados depois de `n0`); preparo do soro 1440×640 (prateleiras à esquerda, bandeja à direita: `toTray=p.x>730`); leito do soro/bolsa 1440×1120 com braço e suporte lado a lado (`this.wide`, sem abas, `goView` só troca `view`). Painéis (cateter, punção, aspirar, injetar) centralizados com `container(s.wide?360:0)`; régua da punção usa `p.x-C.x`.
  - **Ainda em pé no PC:** sala de preparo EV/IM (`PrepEV`), leito EV seringa (`BedEV`) e IM (`BedIM`). Próxima fase.
  - Barra lateral em cartões: Treino mostra o roteiro; Prática e Prova mostram o **Registro** (só o que já foi feito); atalhos sem 1/2 (no PC o leito já mostra as duas vistas).
- **v9.1 (feedback do Vini no celular):**
  - Cartão do passo com altura fixa (122 px; 108 px em celular baixo): o canvas não muda de tamanho entre passos. Textos dos passos reescritos curtos (≤ ~55 caracteres; títulos encurtados); fase em uma linha (`1/17 · Fase`); prescrição do topo em no máximo 2 linhas. `fitCard()` reduz a fonte só como último recurso; grupos mostram só o que falta e, se não couber, "+N". Robô percorreu ~300 passos em 360×640 e 390×844: altura do cartão e do palco constantes, sem estouro.
  - Régua do gotejamento sem o texto "prescrição" (fica só a marca amarela no Treino).
  - Toque acidental: um objeto só recebe o "clique" se o toque começou nele (patch em `GameObject.emit`: `pointerup` exige o mesmo `downTime` do `pointerdown`). Corrige ângulo da punção → botão do bisel e todos os casos parecidos (arrastar e soltar sobre itens da gaveta, botões dos painéis de aspirar/injetar/ângulo IM, Confirmar do gotejamento, prateleiras).
- Níveis: Treino (passo atual + destaque; grupos como lista; avisa ao pegar errado), Prática (só a fase; dica −2), Prova (sem roteiro).
- Conferência estilo "Papers, Please". Divergências raras (~12% outro paciente + 3% alergia); ~30% com alergia que não conflita.

## Modos
1. **Soroterapia**: Check → PrepS → BedS (braço + suporte).
2. **EV em seringa**: Check → PrepEV → BedEV.
3. **EV em bolsa**: Check → PrepEV (modo bolsa) → BedS.
4. **Intramuscular**: Check → PrepEV (modo IM) → BedIM.
5. **Plantão misto**: 3 tipos diferentes sorteados.

## Implementação
- `Guide` com `deps`: tupla `[fase,id,título,como,vista,{g,short,after}]`; `after:'*'` = depois de todos; `ready()`; `cur()` prefere passo da vista atual.
- `dragify(scene,obj,onTap,onDrop)`: toque e arraste no mesmo objeto (`dragDistanceThreshold=12`); grava `scene._dragT`/`scene._dragging`; `justDragged(scene)` evita o toque duplicado logo após soltar.
- Gaveta (`makeDrawer`): se a cena define `dStart/dMove/dDrop`, os itens são arrastáveis; guarda `s.drawerDefs`.
- `handsFX` (higiene/luvas), câmara por apertos com faixa verde, antissepsia IM esfregando.
- Reuso de cena: tudo que é guardado em `this` é zerado em `create()` (BedS, BedIM, PrepEV — inclusive `hand`, `_anim`, `_dragging`, `_cold`).
- Tabela: `prepSteps(d,via)` + `RECON_BOX` em `showProto()`.

## Testes
- Robô Playwright (scripts em sessão, não versionados): conferência → preparo → leito por chamadas de cena + mouse real para chacoalhar, esfregar, câmara ao lado e injeção rápida; Tabela aberta não deixa o toque chegar à prateleira.
- Em headless, forçar `GAME.loop.inFocus=true`; recalcular a posição do canvas antes de cada arrasto.
- Na nuvem o CDN do jsdelivr é bloqueado: instalar `phaser@3.80.1` via npm e servir com `page.route('**/phaser.min.js')`; bloquear fonts.googleapis.

## Pendências para validar com RT/farmácia
- Volumes de ampola fictícios; biperideno "em 3 minutos"; **limites das faixas lento/médio/rápido**.
- Reconstituição (visível na tabela): tenoxicam 2 ml e ceftriaxona 10 ml (EV seringa, completar a 20 ml); hidrocortisona 20 ml, amoxicilina+clavulanato 20 ml e azitromicina 5 ml (bolsa); IM tenoxicam 2 ml, hidrocortisona e Benzetacil 3 ml → 4 ml. Técnica do quadro (ABD pela parede, agitar em círculos; Benzetacil é suspensão).
- Tempos mínimos de injeção EV e IM; agulha IM por peso; lista de alergias "neutras".
