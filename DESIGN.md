# Raiz — regras de jogo implementadas

## Ideia e direção

Transformar um pequeno restaurante em um refúgio do bairro. Todo crescimento acontece no mesmo endereço, ampliando o perímetro do piso e preservando os móveis existentes. A campanha termina em uma casa de 16 × 16; a simulação continua livremente.

Pixel art isométrica com verdes sálvia, madeira, linho e terracota. Os personagens, pratos e móveis são desenhados localmente em canvas. Os clientes se movem até suas mesas; funcionários do salão circulam pela casa. Árvores, piso, janelas e fachada são elementos do renderizador.

## Ciclo principal

1. Antes do serviço: planejar compras, equipe, preços, pesquisa, construção e expansão.
2. Abrir às 10h: clientes chegam automaticamente, ocupam uma cadeira livre e escolhem um prato ativo.
3. Produzir: um cozinheiro e uma vaga de fogão iniciam um pedido, consumindo uma porção de estoque e o custo da receita.
4. Servir: o restaurante recebe o preço do prato, eventuais gorjetas e o adicional de sucos.
5. Clientes comem por 11 segundos e liberam os lugares. Espera excessiva causa desistência.
6. Às 20h cessam as chegadas; os últimos clientes podem ficar até 21h. Fechamento manual também é possível, com cancelamento dos pedidos pendentes.
7. Cobrar salários, despesas e juros; aplicar desperdício; mostrar o balanço e avançar o dia.

O relógio avança 3 minutos por segundo em velocidade 1×. Pausa e janelas modais interrompem a simulação. Ao ocultar a aba, o jogo salva e pausa; não há ganhos ou despesas offline.

## Construção e progressão

| Nível | Terreno | Investimento para alcançar |
|---|---|---|
| Semente | 8 × 8 | Inicial |
| Broto | 10 × 10 | R$ 1.800 |
| Copa | 12 × 12 | R$ 4.800 |
| Jardim | 14 × 14 | R$ 10.000 |
| Refúgio verde | 16 × 16 | R$ 22.000 |

Cada móvel ocupa um piso. Não é possível sobrepor objetos nem construir fora do terreno. Vendas devolvem 50% do preço; uma mesa ocupada não pode ser vendida. Equipamentos de preparo só podem ser vendidos fora do serviço, e o último fogão deve ser preservado.

| Objeto | Preço | Efeito |
|---|---:|---|
| Mesa bistrô | R$ 180 | 2 lugares |
| Mesa de família | R$ 420 | 4 lugares; desbloqueada no Broto |
| Fogão artesanal | R$ 360 | 1 vaga de preparo |
| Forno profissional | R$ 1.000 | 2 vagas de preparo; desbloqueado na Copa |
| Bancada | R$ 240 | +12% de velocidade de preparo por unidade |
| Balcão | R$ 220 | +8% de velocidade de operação por unidade |
| Geladeira | R$ 320 | +35 porções de capacidade por unidade |
| Pia | R$ 180 | Recuperação passiva de higiene |
| Planta | R$ 65 | 2 de aconchego |
| Luminária | R$ 95 | 3 de aconchego |
| Quadro | R$ 120 | 4 de aconchego |
| Horta | R$ 280 | Reduz o custo da receita em 5%; limite de redução: 30% |
| Composteira | R$ 350 | Perda de estoque cai de 5% para 2,5% no fechamento |
| Sucos | R$ 650 | +R$ 5 por pedido; efeito não acumula; nível Broto |

A circulação dos personagens é visual. A posição dos equipamentos não altera seu alcance, e corredores não são obrigatórios nesta versão.

## Cardápio

| Receita | Venda base | Custo ao preparar | Tempo base | Pesquisa | Reputação mínima |
|---|---:|---:|---:|---:|---:|
| Bowl da casa | R$ 26 | R$ 6 | 11s | Inicial | — |
| Salada da estação | R$ 23 | R$ 5 | 9s | R$ 100 | — |
| Burger de cogumelos | R$ 36 | R$ 9 | 15s | R$ 350 | 3,8 |
| Curry de grão-de-bico | R$ 39 | R$ 9 | 17s | R$ 600 | 4,0 |
| Massa ao pesto | R$ 44 | R$ 11 | 19s | R$ 900 | 4,2 |
| Torta de cacau | R$ 32 | R$ 7 | 12s | R$ 1.200 | 4,4 |

Além do custo da receita, cada porção de estoque custa R$ 2 na compra. Essa divisão representa a despensa básica e os insumos específicos do prato. Receita ativa tem a mesma chance de ser escolhida que as outras receitas ativas. Ao menos uma deve permanecer no menu.

O jogador ajusta preços em passos de R$ 2, entre custo base + R$ 3 e o dobro do preço base. Cobrar acima do preço base reduz a satisfação. Alterações não cancelam pratos que já começaram a ser preparados.

## Pessoas e atendimento

| Cargo | Contratação | Salário base diário | Função |
|---|---:|---:|---|
| Cozinheiro | R$ 140 | R$ 42 | Um pedido por vez, limitado às vagas dos fogões |
| Atendente | R$ 100 | R$ 32 | +16s de paciência por cliente |
| Auxiliar | R$ 90 | R$ 28 | Recuperação contínua de higiene |

Treinamento custa R$ 150 × nível atual. O máximo é nível 5. Cada nível acrescenta R$ 5 ao salário; níveis de cozinha melhoram a velocidade média de preparo em 16% por nível adicional. Funcionários têm energia que cai durante o serviço; sua queda diminui a velocidade da cozinha. Todos descansam entre os dias. Máximo de 18 funcionários.

Cliente: chegada → espera → preparo → refeição → saída. Paciência base: 65s, acrescida do atendimento e de até 30 pontos de decoração. A falta de mesa conta como procura perdida e reduz levemente a reputação. A desistência de um cliente sentado afeta mais a reputação. Não há fila física na calçada.

## Satisfação e economia

A satisfação considera preço, espera, decoração e higiene. Reputação varia de 1 a 5 e se aproxima gradualmente das avaliações recebidas. Acima de 4,5 de satisfação, o cliente deixa gorjeta de aproximadamente 10%. Mais reputação e expansões geram mais procura.

O restaurante começa com R$ 2.200, 45 porções, 4 lugares, 1 cozinheira e 4 equipamentos de cozinha/atendimento, além de decoração. Capacidade inicial da despensa: 80 porções, incluindo a geladeira inicial.

Despesas fixas diárias = R$ 30 + R$ 18 por expansão + R$ 1,10 por móvel. A soma dos salários é cobrada mesmo com atendimento fraco. Crédito único em aberto: R$ 1.500, com juros de 2% ao dia. Quitação é integral.

O balanço mostra vendas menos ingredientes consumidos, salários, despesas e juros. Compras de despensa, investimentos e recompensas de metas aparecem diretamente no caixa e não entram no resultado operacional.

Higiene cai ao servir pratos e com o tempo. Pias e auxiliares recuperam-na; limpeza completa custa R$ 45. Reputação sofre quando a higiene fica ruim. Estoque vazio impede novos pedidos; com reposição automática ligada, o jogo compra lotes de 10 porções quando o estoque cai abaixo de 8 e há caixa. Ao fechar, tenta completar o estoque conforme o dinheiro disponível.

## Metas e eventos

Metas sequenciais: servir 5 pratos (+R$ 200), atingir 8 lugares (+R$ 250), aprender 3 receitas (+R$ 350), ampliar para Broto (+R$ 500), servir 100 pratos (+R$ 800) e alcançar Refúgio verde (+R$ 3.000).

Marketing pago: R$ 180 por três serviços com +40% de procura. Nos dias múltiplos de 5, indicação gratuita do guia do bairro concede ao menos um serviço de campanha. No terceiro dia e nos múltiplos de 7, uma cooperativa oferece até 25 porções por R$ 25, limitada à capacidade disponível.

Melhoria permanente de fluxo: R$ 800 por +20% de velocidade. O indicador ambiental soma 1,8 kg fictícios de CO₂ evitado por prato servido; é uma estatística lúdica, sem base de cálculo ambiental real.

## Persistência e limites

Salvamento em `localStorage`, com arquivo JSON para exportar e importar. A entrada de importação é validada antes de substituir o jogo. O nome do restaurante pode ser personalizado; um novo jogo exige confirmação.

Não há troca de prédio, andares, franquias, ingredientes de origem animal ou necessidade de microgerenciar cada pedido. O foco está no equilíbrio entre capacidade, caixa, qualidade e expansão. A primeira versão privilegia uma operação compreensível; colisão física, carregamentos de prato e animações direcionais não fazem parte desta implementação.

## A casa ganha vida — segunda versão

### Horta do quintal

Três canteiros externos ao terreno principal podem ser colhidos por clique no cenário ou pelos botões sobrepostos. Cada colheita dá um tempero especial e duas porções de estoque, respeitando a capacidade da despensa. Começam maduros; depois de colhidos, precisam de 42 segundos de serviço para crescer novamente. O crescimento respeita a velocidade e a pausa. Temperos são guardados para o Ateliê e para o Festival, criando uma decisão entre receita permanente e celebração temporária.

### Ateliê de sabores

O jogador dá nome ao prato e combina uma entre três bases (quinoa, lentilha ou cogumelos), um entre três molhos (tahine, pesto ou manga) e uma entre três finalizações (castanhas, flores ou chips). São 27 combinações, com preços, custos e tempos derivados dos ingredientes. Criar custa R$ 280 e três temperos. A receita entra automaticamente no cardápio e recebe +0,15 de satisfação. Existe um espaço de receita autoral; recriá-la substitui a anterior. A substituição é bloqueada enquanto houver clientes com esse pedido.

### Vocações

- **Casa de afeto:** +0,2 de satisfação por prato.
- **Cozinha criativa:** +10% de velocidade de preparo.
- **Da terra à mesa:** desperdício reduzido pela metade, acumulando com compostagem.

A primeira escolha pode ser feita a qualquer momento. Trocas posteriores só acontecem entre os serviços. A vocação é gratuita e não modifica a planta do restaurante.

### Histórias do bairro

Dona Celina pede oito pontos de aconchego; Ravi quer 25 pratos servidos; Maya incentiva a primeira receita autoral; Seu Bento acompanha 12 colheitas; Luna sonha com dois festivais. São objetivos paralelos às metas principais. Recompensas únicas variam de R$ 240 a R$ 900, mais 0,08 de reputação. O mural indica progresso e registra a amizade após a recompensa ser coletada.

### Estações e festivais

A cada quatro dias de jogo muda a estação. Primavera favorece salada; verão, bowl; outono, curry; inverno, massa. O prato favorito rende R$ 3 adicionais quando servido.

O **Festival de Sabores** custa seis temperos e só pode começar durante o serviço. Dura 45 segundos de simulação, concede +35% de velocidade de preparo e +40% de procura e muda o cenário com bandeirinhas e partículas luminosas. Esse aumento de procura acumula com o marketing. Encerrar um dia encerra a contagem enquanto as portas estiverem fechadas; o tempo restante é preservado até o próximo serviço.

Servir pratos com intervalo máximo de 22 segundos mantém o combo **Cozinha em sintonia**. A cada cinco pratos consecutivos, a casa ganha um bônus igual a duas vezes o tamanho do combo. O combo é transitório e não é preservado ao recarregar; o recorde é salvo.

### Atmosfera

A luz muda gradualmente após as 16h20 do relógio do jogo. Lâmpadas e equipamentos projetam brilho quente; aparecem vaga-lumes. Fogões trabalhando soltam vapor e clientes satisfeitos deixam corações ou pequenas estrelas. O quintal tem canteiros, uma bicicleta, flores e um gato. Folhas e pequenas partículas se movem. Os elementos são desenhados em canvas; não há imagens externas nem arquivos de áudio obrigatórios.

## Mais decisões durante o serviço — terceira versão

### Comandas reais

A aba Serviço mostra até oito comandas em espera ou preparo, incluindo tempo de espera e andamento. Marcar prioridade coloca esse pedido à frente na próxima vaga de cozinha; não interrompe um prato já em preparo. Só uma comanda pode ter prioridade por vez.

Um mimo custa um tempero da horta. Pode ser enviado uma única vez por cliente em espera ou preparo e concede +25 segundos de paciência e +0,25 de satisfação. O benefício concorre com o uso de temperos em receitas autorais e festivais.

### Encomendas de bicicleta

Uma oferta aparece ao abrir cada serviço. A encomenda usa uma receita ativa e pede de três a seis pratos, conforme o nível da casa. O pagamento é 135% do valor total calculado pelos preços no momento da oferta. O prazo é 65 segundos mais 65% da soma dos tempos base de preparo. Novas encomendas só podem ser aceitas antes das 18h30.

Aceitar não reserva ingredientes gratuitamente: cada prato consome uma porção e o custo da receita quando seu preparo começa. Encomendas e clientes sentados compartilham o menor valor entre cozinheiros e vagas de fogão. O processo verifica as vagas ocupadas pelas duas filas; não existe um fogão extra invisível para delivery.

O pagamento só acontece quando todos os pratos estão prontos. Sucesso soma pratos servidos, impacto, receita e 0,035 de reputação. Atraso ou encerramento do serviço antes da conclusão cancela o pagamento, remove a encomenda e reduz a reputação em 0,08. Ingredientes já usados não são devolvidos. O jogador pode acompanhar a bike e o progresso no cenário e no painel. A receita autoral não pode ser substituída durante uma encomenda que a utiliza.

### Críticos

O Guia das Pequenas Casas pode ser convidado a partir do dia 3, com pelo menos três dias entre convites. É preciso ter portas abertas e uma cadeira disponível. O crítico é um cliente de verdade, sujeito à fila e ao preparo, com 95 segundos de paciência. Prioridade e mimo também funcionam para ele.

A nota corresponde à satisfação real arredondada entre uma e cinco estrelas. Quatro estrelas geram R$ 160; cinco geram R$ 320. Ambas aumentam a reputação em 0,12. Notas menores trazem recomendações e reduzem a reputação em 0,06. Se o crítico for embora sem comer, há perda de 0,05. As últimas oito avaliações são salvas; as duas mais recentes aparecem no painel.

### Desafio diário

Os serviços alternam três objetivos: servir 12 pratos; servir 10 e estar com higiene de pelo menos 85% na coleta; servir três receitas diferentes. A recompensa é R$ 160 mais R$ 50 por expansão. Deve ser coletada durante o serviço e só pode ser recebida uma vez por dia. Entregas concluídas também contam como pratos servidos.

### Remodelação

Com portas fechadas, clicar em um móvel abre sua inspeção e permite movê-lo gratuitamente. A origem fica preservada até o jogador escolher um destino válido. Pisos ocupados são rejeitados, e Esc cancela sem mudar o móvel. Abrir o serviço ou selecionar uma ferramenta também encerra a movimentação.

Três estilos de piso: Madeira & linho (inicial), Oliva & pedra (R$ 240) e Terracota & creme (R$ 360). Uma vez comprados, podem ser alternados gratuitamente entre os serviços. A Varanda da amizade custa R$ 750, adiciona guarda-sol e floreiras ao quintal e concede +0,1 de satisfação. É uma melhoria permanente, sem lugares adicionais no salão.

O avanço com tempo zero é bloqueado: a pausa não inicia pedidos, não consome ingredientes e não recebe novos clientes. Apenas decisões explícitas do jogador, como construção e compras, alteram o estado enquanto o relógio está parado.

## Experiência mobile

O celular usa um fluxo diferente do desktop, preservando a mesma simulação e o mesmo arquivo de progresso. A casa é a tela principal; o caixa e a reputação ficam no topo, e o cenário ocupa o espaço restante. O relógio continua visível. Indicadores secundários, diário e metas ficam no menu Mais.

A navegação inferior tem cinco destinos: Casa, Construir, Cardápio, Serviço e Mais. Painéis de gestão abrem acima dessa navegação e têm rolagem própria, botão de fechar e área externa para retornar à casa. As abas do painel continuam disponíveis para mudar diretamente de área. Enquanto o painel está aberto, a cena fica indisponível para interação e o tempo pausa. Ao fechar, é retomada exatamente a velocidade anterior, incluindo a pausa voluntária.

Construção no toque tem dois passos: selecionar um móvel no catálogo fecha o painel; tocar no piso mostra uma prévia e o custo. Confirmar na faixa inferior executa a compra. Vender também exige confirmação. A faixa inclui cancelamento e dá lugar ao botão normal de serviço quando a ferramenta é liberada. Arrastar ou pinçar suprime o clique subsequente, impedindo compras causadas pelo final de um gesto.

O cenário admite arraste com um dedo e zoom com dois. A geometria de interação é a mesma da renderização, inclusive após mudar a câmera. A altura interna do canvas acompanha sua proporção visual para manter pessoas e móveis sem distorção. Câmera centralizada pode ser restaurada a qualquer momento.

Os controles de gestão têm áreas de toque maiores e texto legível; comandas ocupam toda a largura. Menus, diálogos e confirmações rolam internamente. A página principal não exige rolagem vertical. Os controles inferiores respeitam a área segura do aparelho. O modo horizontal reduz o cabeçalho e reorganiza o HUD para preservar o cenário.

Os testes cobrem navegação, pausa e retomada, construção confirmada, cancelamento, pan e pinch com eventos reais do navegador, ausência de compras durante gestos, retorno da câmera, rotas secundárias, diálogos, largura mínima de 320 pixels e orientação horizontal.
