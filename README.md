# Raiz — Vegan Tycoon

Um jogo de gestão de restaurante vegano inspirado na ideia de construção isométrica do DevTycoon. Interface em português, arte original e crescimento no mesmo endereço.

## Jogar

Abra `index.html` no Edge, Chrome ou Firefox. Não precisa instalar nada para jogar. A fonte on-line é opcional; o jogo usa fontes locais se estiver sem internet.

Para usar um endereço local estável para os salvamentos:

```sh
npm start
```

Abra http://localhost:4173. O progresso fica no navegador e no endereço usado; para transferi-lo, use **Configurações → Exportar / Importar progresso**.

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

## Controles

Selecione um móvel em **Construir** e clique no piso livre. **Esc** cancela a seleção. Use **Vender móveis** para recuperar metade do investimento. Clique no piso de um móvel sem ferramenta para inspecionar. **Espaço** pausa; a roda do mouse ou os botões ajustam o zoom. Em telas menores, os painéis de gestão ficam abaixo do restaurante.

Abra o serviço no botão abaixo do cenário. A operação é automática; use as abas para tomar decisões. O serviço fecha após os últimos clientes, e você recebe um balanço antes do próximo dia.

## Arquivos

- `index.html`, `style.css`: interface e layout responsivo.
- `sprites.js`: fábrica original de sprites em canvas; o jogo não precisa carregar arquivos de imagem.
- `game.js`: simulação, economia, progressão, renderização e persistência.
- `assets/sprites/`: 23 sprites PNG exportados para reutilização.
- `assets/spritesheet.png`: catálogo visual dos sprites.
- `DESIGN.md`: regras e decisões de design implementadas.

## Verificação

```sh
npm install
npm test
```

O teste usa Playwright com Microsoft Edge instalado. Verifica construção por clique, colisão, cardápio, equipe, expansão, serviço completo, salvamento, falta de estoque e layout móvel. Também exporta os sprites e captura as telas em `test-results/`.

O indicador de CO₂ é uma regra fictícia do jogo, sem pretensão de calcular impacto ambiental real. A distribuição dos móveis é livre: esta versão simula capacidade e atendimento, sem colisão física ou busca de caminhos entre os móveis.
