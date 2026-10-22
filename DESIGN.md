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
