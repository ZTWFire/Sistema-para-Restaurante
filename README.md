# Sistema para Restaurante

Projeto de um sistema simples para restaurantes pequenos e médios: central de pedidos de todos os
canais, tela da cozinha (KDS) em tempo real, caixa e visão clara do lucro.

- `docs/PESQUISA_DE_MERCADO.md` — como um restaurante funciona, principais dores, concorrentes,
  funcionalidades recomendadas e diretrizes para o protótipo em HTML.

Próximo passo: protótipo navegável em HTML (visual inspirado no iFood) com as telas da seção 9 da
pesquisa.

## Esteira de ofertas (skill do Claude)

`.claude/skills/esteira-oferta/` + `.claude/agents/` — esteira para analisar uma oferta que está
escalando e criar uma oferta adjacente (raio-x, público, produto, página, criativos e teste).
Em qualquer sessão do Claude Code com este repositório: `/esteira-oferta <link da oferta>`.
Os resultados ficam em `ofertas/<apelido>/`.
