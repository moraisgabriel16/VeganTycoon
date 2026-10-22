# Raiz — Vegan Tycoon

Um jogo de gestão de restaurante vegano inspirado na ideia de construção isométrica do DevTycoon. Interface em português, arte original e crescimento no mesmo endereço.

## Jogar

Abra `index.html` no Edge, Chrome ou Firefox. Não precisa instalar nada para jogar. A fonte on-line é opcional; o jogo usa fontes locais se estiver sem internet.

Para usar um endereço local estável para os salvamentos:

```sh
npm start
```

Abra http://localhost:4173. O progresso fica no navegador e no endereço usado; para transferi-lo, use **Configurações → Exportar / Importar progresso**.

## Experiência mobile

Até 800 pixels de largura, o jogo usa uma interface própria para toque. O restaurante ocupa a tela, com navegação inferior em **Casa, Construir, Cardápio, Serviço e Mais**. Equipe, Gestão, Bairro, Ateliê, Festival, metas e diário ficam em Mais.

Gestão abre em painéis inferiores com rolagem própria. O jogo pausa enquanto o painel está aberto e volta à velocidade anterior ao fechar. O botão de abrir/encerrar serviço permanece acessível acima da navegação. Arraste o cenário para explorar e use dois dedos para ampliar; o botão de centralizar restaura a câmera.

Ao construir ou vender, o primeiro toque no piso apenas mostra a prévia. Só o botão **Colocar** ou **Vender** confirma a transação. O botão ✕ cancela. Arrastar e pinçar não confirmam compras. O cenário preserva as proporções dos sprites, inclusive em telas altas. O layout respeita as áreas seguras de aparelhos com recorte e mantém o zoom da página disponível.

Verificado com eventos nativos de toque no Edge via Playwright, em larguras de 320 a 430 pixels e em orientação horizontal. Essa verificação em navegador não substitui uma avaliação em aparelhos físicos.

## O que está implementado

- Restaurante isométrico com clientes e funcionários animados, zoom e construção em grade.
- 14 móveis e equipamentos; 6 pratos pesquisáveis; personagens com variações de aparência.
- Mesas de 2 ou 4 lugares, fogões, forno, geladeira, pia, bancada, balcão, sucos, decoração, horta e compostagem.
- Clientes com chegada, espera, preparo e refeição. Fila limitada aos lugares disponíveis.
- Cozinheiros, atendentes e auxiliares; salários, energia, treinamento e demissão.
- Estoque, reposição manual e automática, higiene, desperdício, custos, balanço, crédito e juros.
- Preços ajustáveis, satisfação, gorjetas, reputação, marketing e eventos do bairro.
- 5 níveis de expansão no mesmo terreno, metas remuneradas e continuação livre após a última expansão.
- Pausa, velocidades, áudio opcional, salvamento automático, exportação e importação.
- Horta interativa com colheita, crescimento e temperos especiais.
- Ateliê para criar uma receita autoral com 27 combinações de ingredientes.
- Cinco vizinhos com histórias, pedidos e recompensas; estações com pratos favoritos.
- Três vocações para a casa, combos de serviço e Festival de Sabores.
- Entardecer, luzes, vapor, vaga-lumes, bicicleta, flores e gato no quintal.
- Comandas com prioridade e mimos; encomendas de bicicleta que dividem a cozinha com o salão.
- Críticos gastronômicos, avaliações persistentes e desafios a cada serviço.
- Reorganização gratuita dos móveis, três opções de piso e varanda com guarda-sol e floreiras.

## Controles

Selecione um móvel em **Construir** e clique no piso livre. **Esc** cancela a seleção. Use **Vender móveis** para recuperar metade do investimento. Clique no piso de um móvel sem ferramenta para inspecionar. **Espaço** pausa; a roda do mouse ou os botões ajustam o zoom. Em telas menores, os painéis de gestão ficam abaixo do restaurante.

Abra o serviço no botão abaixo do cenário. A operação é automática; use as abas para tomar decisões. O serviço fecha após os últimos clientes, e você recebe um balanço antes do próximo dia.

## Arquivos

- `index.html`, `style.css`: interface e layout responsivo.
- `sprites.js`: fábrica original de sprites em canvas; o jogo não precisa carregar arquivos de imagem.
- `game.js`: simulação, economia, progressão, renderização e persistência.
- `life.js`: bairro, horta, pratos autorais, vocações, festival e atmosfera.
- `service.js`: comandas, entregas, críticos, desafios, reorganização e estilos do restaurante.
- `mobile.js`, `mobile.css`: navegação por toque, painéis, câmera e confirmação de construção.
- `assets/sprites/`: 30 sprites PNG exportados para reutilização.
- `assets/spritesheet.png`: catálogo visual dos sprites.
- `DESIGN.md`: regras e decisões de design implementadas.

## Verificação

```sh
npm install
npm test
```

Os testes usam Playwright com Microsoft Edge instalado. Verificam construção por clique, colisão, cardápio, equipe, expansão, serviço completo, salvamento, horta, receita autoral, festival, bairro, entregas, capacidade compartilhada, críticos, prioridades, mimos, desafios e layout móvel. Também exportam os sprites e capturam as telas em `test-results/`.

O indicador de CO₂ é uma regra fictícia do jogo, sem pretensão de calcular impacto ambiental real. A distribuição dos móveis é livre: esta versão simula capacidade e atendimento, sem colisão física ou busca de caminhos entre os móveis.
