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

## Teclas (tela de TV)

`←` `→` trocam o dia · `F` tela cheia · `T` tema claro/escuro
