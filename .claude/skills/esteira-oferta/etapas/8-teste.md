# Etapa 8 — Plano de teste de tráfego

Objetivo: descobrir com pouco dinheiro se a oferta vende, e saber **quando cortar e quando
escalar**. Os números abaixo são pontos de partida comuns em low ticket, não leis; ajuste com os
dados reais.

## Conta básica (sempre calcule e mostre)
- Ticket médio esperado = preço principal + (preço do bump × 30%) + (preço do upsell × 10%).
- Receita líquida por venda = ticket médio × (1 − taxa da plataforma, ~10%).
- **CPA máximo (empate)** = receita líquida por venda. Acima disso, perde dinheiro.
- CPA alvo para escalar = 60–70% do CPA máximo.

## Estrutura inicial
- 1 campanha de **Vendas** otimizando para **Compra**.
- 1 conjunto com público aberto (Brasil, idade e gênero do `4-publico.md`) ou com os interesses
  principais; posicionamentos automáticos.
- 5 criativos (os da "ordem de teste" da etapa 7).
- Orçamento: R$ 50 a R$ 100 por dia, durante 3 a 4 dias antes de julgar.

## Leitura das métricas
| Métrica | Referência | Se estiver ruim, o problema é… |
|---|---|---|
| CTR no link | ≥ 1% | Criativo/gancho |
| CPC no link | Abaixo de ~R$ 1,50 | Criativo ou público |
| Página → início de checkout | ≥ 8–10% | Página (promessa, preço, clareza) |
| Checkout → compra | ≥ 30–40% | Checkout (preço, confiança, meios de pagamento) |
| Taxa de bump | ≥ 20–30% | Oferta do bump ou texto dele |

## Regras de decisão
- Criativo gastou **1 CPA máximo sem nenhuma venda** → pausar.
- Criativo com CPA **abaixo do alvo** por 2 dias → duplicar e aumentar orçamento 20–30% por dia.
- CTR bom e nenhuma venda → mexer na página, não no criativo.
- Nenhum criativo com CTR ≥ 1% → voltar à etapa 7 com novos ângulos (não novos tons de cor).
- Depois de ~R$ 500 investidos sem venda lucrativa → rever a oferta (etapa 3), não só anúncios.

## Formato de saída (`8-teste.md`)
```
# Plano de teste — <nome>

## Conta
| Item | Valor |
|---|---|
| Ticket médio esperado | |
| Receita líquida por venda | |
| CPA máximo | |
| CPA alvo | |

## Campanha
<estrutura, público, orçamento, criativos que sobem>

## Rotina diária (5 minutos)
<o que olhar, em que ordem, e as regras de decisão aplicadas a esta oferta>

## Próximos passos depois da primeira venda
```

Ao final, atualize `ficha.md` com o status "Pronta para rodar" e a lista do que o usuário ainda
precisa fazer fora do Claude (produzir arte, subir página, configurar pixel).
