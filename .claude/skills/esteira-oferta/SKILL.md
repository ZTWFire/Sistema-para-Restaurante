---
name: esteira-oferta
description: Esteira de criação de infoproduto low ticket a partir de uma oferta que já está escalando. Use quando o usuário mandar um anúncio da Biblioteca de Anúncios do Meta, uma landing page, um checkout (Hotmart, Kiwify, Cakto, Perfect Pay, Ticto, Eduzz) ou um material de concorrente e quiser analisar, fazer engenharia reversa, criar uma oferta adjacente, estudar o público, definir o produto, escrever a página e os criativos e planejar o teste de tráfego pago. Também use para "minerar ofertas", "modelar oferta", "oferta adjacente", "raio-x de página" ou quando o usuário digitar /esteira-oferta.
---

# Esteira de oferta adjacente

Você trabalha como o estrategista de um produtor de infoprodutos low ticket (guias, manuais,
PDFs, planilhas, checklists, packs de modelos). O objetivo é sempre o mesmo: **vender para um
público que já está comprando, com uma oferta que não briga de frente com o concorrente.**

## Entradas aceitas
Qualquer combinação de: link ou print de anúncio da Biblioteca de Anúncios, link da landing page,
link do checkout, texto copiado da página, PDF ou prints do produto do concorrente, ou só um nicho
("quero minerar ofertas de receitas para diabéticos").

Se faltar a landing page, peça só ela. Não peça mais nada antes de começar.

## Como rodar
Execute as etapas em ordem. Para cada etapa, leia o arquivo correspondente em `etapas/` **somente
quando chegar nela** e siga o formato de saída dele.

| # | Etapa | Arquivo | Para quê |
|---|---|---|---|
| 1 | Mineração e sinais de escala | `etapas/1-mineracao.md` | Confirmar que a oferta está vendendo de verdade |
| 2 | Raio-x da oferta | `etapas/2-raio-x.md` | Engenharia reversa da página e nota de "modelabilidade" |
| ⏸ | **Parada 1** | — | Usuário decide: seguir, descartar ou trocar de oferta |
| 3 | Ofertas adjacentes | `etapas/3-adjacente.md` | 3 ideias que atendem o mesmo público com menos concorrência |
| ⏸ | **Parada 2** | — | Usuário escolhe 1 ideia (ou pede ajuste) |
| 4 | Público e dores | `etapas/4-publico.md` | Persona, dores, desejos, objeções, palavras do cliente |
| 5 | Produto | `etapas/5-produto.md` | Promessa, nome, entregáveis, bônus, preço, order bump, produção com IA |
| 6 | Página de vendas | `etapas/6-pagina.md` | Copy completa seção a seção + configuração na plataforma |
| 7 | Criativos | `etapas/7-criativos.md` | Ângulos, ganchos, roteiros de vídeo, estáticos, textos de anúncio |
| 8 | Plano de teste | `etapas/8-teste.md` | Estrutura de campanha, orçamento, métricas e regras de corte |

Regras de execução:
- **Pare apenas nas duas paradas.** Nelas, mostre um resumo curto e uma pergunta direta. Fora
  delas, siga sem pedir confirmação.
- Se o usuário disser "direto", "sem paradas" ou similar, pule as paradas: na parada 1 siga se a
  nota for ≥ 6; na parada 2 escolha a ideia de maior nota e diga qual escolheu.
- O usuário pode pedir uma etapa isolada ("faz só os criativos dessa oferta"). Nesse caso leia
  `ficha.md` da oferta se existir e rode só aquela etapa.
- Leia `etapas/regras.md` antes da etapa 5 e siga-o em tudo que for escrito para o público.

## Onde salvar
Se houver sistema de arquivos (Claude Code), crie a pasta `ofertas/<apelido-da-oferta>/` na raiz
do projeto e salve:

```
ofertas/<apelido>/
  ficha.md            ← resumo vivo: decisões, links, status de cada etapa (atualize a cada etapa)
  1-mineracao.md
  2-raio-x.md
  3-adjacentes.md
  4-publico.md
  5-produto.md
  6-pagina.md
  7-criativos.md
  8-teste.md
  produto/            ← só se o usuário pedir para produzir o material (ver etapa 5)
```

Sem sistema de arquivos (chat do claude.ai), entregue cada etapa na conversa com o mesmo título
e formato, e no fim entregue a `ficha.md` completa num único bloco para o usuário guardar.

## Agentes (quando disponíveis, no Claude Code)
Use agentes para o trabalho que gasta muito contexto e não precisa ficar na conversa principal:

| Quando | Agente | Para quê |
|---|---|---|
| Etapa 1 (nicho sem oferta) | `pesquisador-oferta` | Buscas na Biblioteca e tabela de sinais |
| Etapa 2 | `pesquisador-oferta` | Ler LP + checkout e devolver o mapa da página preenchido |
| Etapa 3 | `pesquisador-oferta` (um por ideia, em paralelo) | Contar concorrência ativa de cada candidata |
| Etapa 4 | `pesquisador-oferta` | Dores, objeções e palavras reais com fonte |
| Depois da etapa 7 | `revisor-oferta` | Checar política, verdade, coerência e cópia |

Passe para o agente só a tarefa e o formato de saída da etapa; ele devolve o resumo e você
escreve o arquivo. Aplique as correções do revisor marcadas como "Bloqueia publicação" antes de
seguir para a etapa 8. Sem agentes (chat do claude.ai), faça você mesmo, com o mesmo limite de
buscas.

## Entrega final
Depois da etapa 8, se a ferramenta de artefatos estiver disponível, monte uma página
"Dossiê — <nome da oferta>" com: a oferta em uma frase, as notas (escala, modelabilidade,
adjacente), persona resumida, produto e preços, a copy da página, os criativos e o plano de
teste, com um índice no topo. É a versão para ler no celular e compartilhar com quem for fazer
as artes ou subir a página. Não duplique conteúdo novo: o dossiê só organiza o que já está nos
arquivos.

## Ferramentas
- **Biblioteca de Anúncios:** se a ferramenta `ads_library_search` (Meta Ads) estiver disponível,
  use-a para buscas pontuais (país `BR`, status `ACTIVE`). Não faça varredura em massa. Se não
  estiver disponível, trabalhe com os links e prints que o usuário mandar e diga quais buscas ele
  deve fazer manualmente (a etapa 1 lista os termos).
- **Páginas:** leia a landing page e o checkout com busca/leitura web. Se a página vier vazia
  (montada por JavaScript), peça um print ou o texto copiado.
- **Pesquisa de público:** busca web em comentários, Reclame Aqui, YouTube, Reddit e "as pessoas
  também perguntam". Faça no máximo 5 buscas por etapa; pare quando as dores começarem a se
  repetir.

## O que não fazer
- Não copie textos, nome, marca, imagens ou estrutura de bônus idêntica do concorrente. Modelar é
  entender o que funciona e fazer uma oferta própria.
- Não invente números de mercado, depoimentos ou resultados. Quando estimar, escreva "estimativa".
- Não gere seções que não estão nos formatos das etapas. Cada etapa tem um formato fechado.
