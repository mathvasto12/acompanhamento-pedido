# Acompanhamento de Pedido

Painel diário de **atendimento vs planejado** do CD Outbound: lojas planejadas e expedidas, ondas, lanes, peças e SKUs.

- **Painel completo:** `index.html` (filtros, tabelas, evolução diária, lojas desconsideradas e exportação para PowerPoint, JPG e PDF)
- **Tela de TV:** `tv.html` (indicadores, ondas e grade de lanes em tela cheia)

## Como usar

1. Abra a página e clique em **Importar Excel**.
2. Escolha a base `.xlsx` com as abas **Ciclo do Pedido** e **Operação CD**.
3. O painel é calculado no próprio navegador. O arquivo não é enviado para nenhum servidor.
4. A base fica salva naquele navegador. Para atualizar, importe o Excel novo.

O repositório não guarda dados de expedição: só o cronograma de lojas, ondas e lanes, que está embutido nas páginas.

## Regras principais

- **Expedida no dia:** pedido com status `S` e `oh_ship_date` no dia, contado por loja.
- **Pedidos cancelados** (`oh_cancelled = Y`) são ignorados.
- **Não expedida:** loja do cronograma sem expedição no dia, com a situação (expedida depois, em processo com % coletado, pendente ou sem pedido).
- **Fora do plano:** loja expedida que não está no cronograma daquele dia.
- **Peças e SKUs:** `otd_qty` e SKUs distintos (`otd_part`) dos pedidos das lojas de cada onda, na aba Operação CD.

## Ondas

| Onda | Release (Control Desk) | Término da separação |
|---|---|---|
| 1 | 06:00 | 10:30 |
| 2 | 09:00 | 13:50 |
| 3 | 14:00 | 18:00 |
| 4 | 16:00 | 21:50 |

## Visões

- **Outbound Control Tower:** indicadores (Schedule, Adherence, On time, Pull forward, Pieces, Lines) com Wave Process Tracking, Dispatch Control, Production Curve e Exception Management.
- **Visão geral das ondas:** cartões das ondas (peças, SKUs, início e fim) e grade de lanes.
- **Processo das ondas:** Billing, Picking, Consolidação e Staging por onda (lojas concluídas / planejadas).
- **Controle de saída das rotas:** horário alvo e real de cada rota.
- **Timeline das ondas:** planejado vs realizado por etapa, com atraso em minutos.
- **Curva de produção:** peças separadas ao longo do dia vs meta (peças planejadas entre release e término).
- **Gestão de exceções:** lojas pendentes, separação atrasada, rotas atrasadas ou em risco.
- **Performance das rotas:** etapas por rota, com as lojas de cada rota.

A **Onda 5** (nova jornada sem sábado) aparece sem lojas até entrar no cronograma.

## Cronograma

Importe o arquivo do cronograma pelo mesmo botão **Importar Excel** (aba `CRONOGRAMA`). Colunas usadas:
`ROTA`, `LOJA`, `CÓDIGO LOJA`, `TRANSPORTADORA`, `WAVE`, `BILLING`, `ORDER RELEASE`, `DIA SEPARAÇÃO`, `TÉRMINO SEPARAÇÃO`, `ENTRADA EXPEDIÇÃO`, `ENTRADA DOCA`, `LANE`, `DOCA`.
Para o horário de saída da rota, inclua uma coluna **`SAÍDA ROTA`**. Sem ela, o alvo da rota usa a entrada na expedição (marcado com `*`).

## Consolidação (aba opcional na base)

Crie na base uma aba chamada **`Consolidação`** com, no mínimo:

| Coluna | Conteúdo |
|---|---|
| `pedido` | número do pedido (o mesmo de `oh_order`) |
| `fim` | data e hora do término da consolidação |

Sem essa aba, a etapa aparece como **WIP**. Carregamento também aparece como WIP (sem dados na base).

## Teclas (tela de TV)

A TV mostra um painel por vez e troca a cada **30 segundos**.

`Espaço` pausa/continua · `PageDown`/`PageUp` trocam o painel · `←` `→` trocam o dia · `F` tela cheia · `T` tema claro/escuro
