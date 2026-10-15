# Pesquisa de mercado — Sistema para Restaurantes

> Levantamento feito em outubro/2026 como base para decidir **o que** construir e para guiar o
> protótipo em HTML. Números de mercado vêm, em sua maioria, da Abrasel e de imprensa
> especializada; preços de concorrentes vêm de sites oficiais ou blogs e **devem ser
> reconfirmados** antes de qualquer decisão comercial. Fontes no final.

---

## 1. Resumo executivo (leia só isto se tiver pouco tempo)

1. **O mercado é enorme e apertado.** Alimentação fora do lar faturou cerca de **R$ 495 bi em
   2025** (Abrasel). Mesmo assim, em vários meses de 2025–2026 entre **22% e 30% dos
   estabelecimentos operaram com prejuízo** e ~**40% tinham contas em atraso**. Só cerca de
   **42% tiveram lucro** em julho/2026.
2. **A dor nº 1 não é tecnologia, é margem.** O dono não sabe quanto custa cada prato (CMV),
   quanto o iFood realmente leva, nem quanto sobrou no fim do dia. Restaurantes fecham por falta
   de gestão e de capital de giro (Sebrae), não por falta de app.
3. **A dor nº 2 é a operação no horário de pico:** pedidos chegando por 4–5 canais ao mesmo tempo
   (salão, balcão, WhatsApp, iFood, telefone), comanda de papel ilegível, prato esquecido,
   cozinha sem saber a ordem de preparo, cliente reclamando de atraso.
4. **A dor nº 3 é gente:** rotatividade acima de **70% ao ano** e **90%** dos donos dizendo que é
   difícil contratar. Consequência prática: **o sistema precisa ser aprendido em minutos** por
   um garçom ou cozinheiro novo.
5. **O iFood virou o "dono" do software de restaurante.** Comprou Anota AI (2022) e, em 2025,
   **Saipos, Opdv e 3S Checkout**, com o objetivo declarado de ser o "all in one" do
   restaurante. Competir em "integração com iFood" é jogar no campo dele. Há espaço em
   **simplicidade, independência, canal próprio e clareza financeira**.
6. **Recomendação de foco:** um sistema **simples, para o restaurante pequeno/médio de 1 unidade**
   que una **(a) central de pedidos de todos os canais → (b) tela da cozinha (KDS) em tempo
   real → (c) caixa/fechamento → (d) "quanto eu ganhei hoje" (lucro real por canal e por
   prato)**. É o fluxo que acontece todo dia; o financeiro sai *de graça* dos pedidos, sem o dono
   precisar digitar nada.

---

## 2. Como um restaurante funciona na prática

### 2.1 Modelos de operação (cada um muda o sistema)

| Modelo | Como o pedido nasce | Como é pago | Particularidades |
|---|---|---|---|
| **À la carte (mesa)** | Garçom anota na mesa | Ao final, por mesa/pessoa | Comanda aberta por horas, divisão de conta, taxa de serviço 10% |
| **Self-service / por quilo** | Cliente se serve, balança | No caixa, na saída | Pouco pedido "de cozinha"; foco em caixa e reposição |
| **Balcão / fast-food / lanchonete** | Cliente pede no caixa ou totem | Antes de comer | Senha/chamada no painel, velocidade é tudo |
| **Bar** | Garçom ou balcão | Comanda individual (cartão/pulseira) | Comandas abertas muito tempo, consumo de bebidas, "pendura" |
| **Delivery / dark kitchen** | iFood, WhatsApp, site, telefone | Online ou na entrega | Tempo de preparo + despacho + motoboy, várias plataformas |
| **Pizzaria** | Mistura de tudo | Idem | Meio-a-meio, bordas, tamanhos — cardápio com muitas variações |

A maioria dos pequenos negócios é **híbrida**: salão no almoço + delivery à noite.

### 2.2 O dia de um restaurante

1. **Antes de abrir** — conferir estoque, receber fornecedores, conferir nota/peso, fazer
   *pré-preparo* (mise en place: cortar, porcionar, molhos), abrir o caixa com troco.
2. **Serviço (pico)** — receber pedidos de vários canais, mandar para a cozinha certa
   (chapa, fritadeira, bar, sobremesa), preparar na ordem certa, montar, conferir, entregar na
   mesa ou despachar para o motoboy.
3. **Durante** — fechar contas, dividir conta, aplicar taxa de serviço, pausar item que acabou
   ("acabou o feijão!"), responder WhatsApp, lidar com atraso/reclamação no iFood.
4. **Fechamento** — fechar caixa (dinheiro, Pix, cartões, vales), conferir sangrias, contar o que
   sobrou, anotar perdas, pagar motoboys, decidir compras do dia seguinte.
5. **Gestão (semana/mês)** — pagar fornecedores e boletos, folha, impostos, conciliar repasses do
   iFood e maquininha, reajustar preços do cardápio.

### 2.3 Quem usa o sistema (personas)

| Persona | O que precisa | Contexto de uso |
|---|---|---|
| **Dono / gerente** | Saber se está ganhando dinheiro, controlar o caixa, não ser roubado | Celular, fora do horário de pico, pouco tempo, pouca formação em gestão |
| **Atendente de caixa / balcão** | Lançar pedido rápido, receber, emitir nota | Computador ou tablet, fila na frente |
| **Garçom** | Lançar pedido na mesa sem voltar ao caixa | Celular na mão, em pé, andando |
| **Cozinheiro** | Saber *o que* fazer, *em que ordem* e *com quais observações* | Tela fixa na parede, mãos sujas/molhadas, barulho, calor — não vai digitar |
| **Entregador** | Saber qual pedido levar e para onde | Celular, rápido |
| **Cliente final** | Pedir fácil, saber quando chega | Cardápio digital / WhatsApp |

### 2.4 O fluxo de um pedido (o "coração" do sistema)

```
Canal (mesa | balcão | WhatsApp | iFood | site | telefone)
        │
        ▼
 [Novo] ──aceitar──► [Em preparo] ──pronto──► [Pronto] ──► [Entregue na mesa | Saiu p/ entrega | Retirado]
        │                 │ (dividido por praça: cozinha, bar, sobremesa)          │
        └─recusar/cancelar┘                                                       ▼
                                                                         [Pago / Fechado] → caixa → relatórios
```

Isso é praticamente o mesmo fluxo do Gestor de Pedidos do iFood (Pendente → Aceito/Em preparo →
Despachado → Concluído). Usar esse modelo mental reduz o treinamento.

---

## 3. Números do mercado

| Indicador | Valor | Fonte |
|---|---|---|
| Faturamento do setor (2025) | ~R$ 495 bi (vs R$ 455 bi em 2024) | Abrasel |
| Participação dos apps de entrega no faturamento | 29,9% | Abrasel |
| Delivery por canal | Marketplaces 54%, **WhatsApp 26%**, app/site próprio 12%, telefone 8% | Abrasel (2.176 donos, 2025) |
| Estabelecimentos que usam WhatsApp para vender | 63% | Abrasel |
| Operando com prejuízo | 22% a 30% conforme o mês (2025) | Abrasel |
| Com lucro (jul/2026) | 42% | Abrasel |
| Com pagamentos em atraso | 35% a 43% (bares pior) | Abrasel (jul/2025) |
| Conseguiram repassar inflação integralmente | só 38% | Abrasel |
| Rotatividade de funcionários | > 70% ao ano (73,5% dez/24–nov/25) | Abrasel / Gironews |
| Donos com dificuldade para contratar | 90% | Abrasel (mar/2025) |
| Mortalidade de restaurantes | ~35% fecham no 1º ano, ~50% em 2 anos (dado antigo, 2013) | Abrasel via estudo acadêmico |
| CMV saudável | 25%–40% do faturamento (30–35% o mais comum) | Sebrae / Abrasel |
| Comissão iFood | Plano Básico ~12% + mensalidade; Plano Entrega ~23%; +3,2% pagamento online | Fontes secundárias, conferir contrato |

**Leitura:** muito dinheiro circulando, pouca margem, alta dependência de marketplace e equipe
instável. Um sistema que **mostre lucro real** e **funcione com equipe que muda todo mês** tem
valor claro.

---

## 4. Principais dores (priorizadas)

Escala: **Impacto** no negócio × **Frequência** com que acontece.

| # | Dor | Como aparece no dia a dia | Impacto | Frequência |
|---|---|---|---|---|
| 1 | **Não saber se está tendo lucro** | Vende muito e o dinheiro "some"; não sabe CMV, nem margem por prato, nem por canal | Altíssimo | Contínuo |
| 2 | **Preço errado / não repassa custos** | Insumo sobe, cardápio fica igual; prato no iFood dá prejuízo depois da comissão | Altíssimo | Mensal |
| 3 | **Caos de pedidos em vários canais** | Tablet do iFood apitando, WhatsApp no celular do dono, comanda de papel, telefone — e cada um num lugar | Alto | Todo pico |
| 4 | **Erro e atraso na cozinha** | Letra ilegível, observação perdida ("sem cebola"), prato esquecido, ordem errada, mesa reclama | Alto | Diário |
| 5 | **Caixa que não fecha / furo** | Diferença no fechamento, sangria sem registro, desconto "por fora", pedido não cobrado | Alto | Diário |
| 6 | **Dependência e custo do iFood** | Comissão de 12–27% + taxas; cliente "é do iFood", não do restaurante | Alto | Contínuo |
| 7 | **Estoque e desperdício** | Acaba ingrediente no meio do serviço; compra no "olhômetro"; perda não registrada | Médio-alto | Semanal |
| 8 | **Rotatividade / treinamento** | Garçom novo a cada mês; sistema complicado = ninguém usa direito | Médio-alto | Mensal |
| 9 | **Fiscal** | NFC-e obrigatória, SAT/estado a estado, Reforma Tributária (IBS/CBS) mudando campos das notas | Médio | Contínuo |
| 10 | **Software ruim** | Sistema trava no pico, cai sem internet, suporte demora, cobra módulos que não usa | Médio | Pontual, mas crítico |

> Reclamações reais no Reclame Aqui sobre sistemas do setor citam justamente **lentidão e
> travamento em dias de pico, falha no envio de pedidos para o tablet da cozinha, suporte
> demorado e cobrança de módulos não usados**. Esses são critérios de qualidade, não features.

---

## 5. Concorrentes

### 5.1 Mapa do mercado brasileiro

| Sistema | Foco | Público | Preço de entrada (aprox.) | Observações |
|---|---|---|---|---|
| **iFood (Gestor de Pedidos + Portal do Parceiro)** | Pedidos do próprio iFood | Todos no iFood | Incluso na comissão | Só cobre o canal iFood; fiscal fraco |
| **Saipos** *(iFood, desde 2025)* | ERP completo: PDV, comanda, KDS, estoque, fiscal, CRM | Restaurante médio em crescimento | ~R$ 240/mês | Muito integrado ao iFood; Reclame Aqui nota 7,2 e queixas de instabilidade no pico e suporte |
| **Anota AI** *(iFood, desde 2022)* | Robô de WhatsApp + cardápio digital + gestor de pedidos | Delivery pequeno/médio | ~R$ 300/mês | 70 mil restaurantes; forte no WhatsApp |
| **Opdv / 3S Checkout** *(iFood, 2025)* | PDV / grandes redes (Burger King, Outback) | Redes | Sob consulta | Mostra que o iFood quer o salão também |
| **Goomer** | Cardápio digital, QR code, autoatendimento no salão, delivery | Pequeno a médio | Plano grátis limitado (30 pedidos/mês); pagos a partir de ~R$ 60–300/mês | Forte no salão; menos robusto em estoque |
| **Consumer** | PDV + delivery próprio (MenuDino) + fidelidade | Pequeno | Baixo / com plano gratuito | Historicamente popular por ser barato; instalado localmente |
| **Cardápio Web** | Cardápio digital + gestor de pedidos delivery | Pequeno | Baixo | Muito usado por pequenos deliveries |
| **Colibri (NCR)** | PDV/ERP tradicional | Médio e redes | Alto | Robusto, mas reclamações de lentidão e suporte |
| **TOTVS Chef / Linx Menew** | ERP corporativo | Redes, franquias | Alto | Complexo para o pequeno |
| **OlaClick, Simpliza, Neemo, Pede.ai etc.** | Cardápio digital / delivery próprio | Micro | Grátis a baixo | Muito focados em vitrine, pouco em operação/financeiro |

Referências internacionais para inspiração de produto: **Toast** e **Square for Restaurants**
(EUA) — PDV + KDS + relatórios num só lugar, com hardware próprio, e **Lightspeed**.

### 5.2 Leitura competitiva

- **Ponta de cima (redes)**: dominada por TOTVS, Linx, Colibri e agora 3S/Opdv (iFood). Não é
  o nosso alvo.
- **Meio (restaurante que cresce)**: Saipos é a referência — e agora é do iFood.
- **Base (pequeno, 1 loja, 3–15 funcionários)**: fragmentada. Ou é cardápio digital barato sem
  gestão, ou é sistema completo caro e complicado. **Aqui está a lacuna.**
- **Tendência**: canal próprio (WhatsApp + cardápio digital) cresce porque dá controle e foge da
  comissão — mas **quase ninguém sai do iFood**, usa os dois. O sistema tem que conviver com o
  iFood, não brigar com ele.

### 5.3 Onde podemos nos diferenciar

1. **Simplicidade radical** — aprender em 5 minutos; telas com poucas opções; botões grandes.
2. **"Quanto eu ganhei hoje?"** — lucro estimado do dia já descontando CMV, comissão do iFood,
   taxa da maquininha. Ninguém entrega isso de forma clara para o pequeno.
3. **Lucro por canal e por prato** — "este X-burger dá R$ 9 de lucro no balcão e R$ 1,20 no
   iFood Entrega". Ajuda a precificar e a empurrar o cliente para o canal próprio.
4. **Funciona sem internet** no salão/cozinha (rede local), sincroniza depois — a queixa nº 1
   de software é travar no pico.
5. **Independência do iFood** — integra, mas o dado e o cliente são do restaurante.
6. **Preço justo e sem módulos escondidos.**

---

## 6. Funcionalidades × dores

| Funcionalidade | Resolve dores | Prioridade |
|---|---|---|
| **Central de pedidos unificada** (todos os canais numa tela, estilo quadro: Novo → Preparo → Pronto → Entregue) | 3, 4 | **MVP** |
| **Tela da cozinha (KDS)** com cronômetro por pedido, cores por atraso (verde/amarelo/vermelho), observações em destaque, separação por praça (cozinha/bar), som de novo pedido, toque único para "pronto" | 4, 8 | **MVP** |
| **Lançamento de pedido** rápido (balcão, mesa pelo celular do garçom) com adicionais/observações | 3, 4 | **MVP** |
| **Mapa de mesas** (livre/ocupada/conta pedida, tempo de ocupação, total parcial) | 3, 5 | **MVP** |
| **Cardápio** com categorias, adicionais, **pausar item que acabou** (reflete em todos os canais) | 3, 7 | **MVP** |
| **Caixa**: abertura, recebimento (dinheiro/Pix/cartão/vale), divisão de conta, taxa de serviço, sangria, **fechamento com diferença** | 5 | **MVP** |
| **Painel "Hoje"**: faturamento, nº pedidos, ticket médio, por canal, tempo médio de preparo, **lucro estimado** | 1, 6 | **MVP** |
| **Ficha técnica + CMV por prato** e simulador de preço por canal (balcão vs iFood) | 1, 2, 6 | **v1** |
| **Despesas e contas a pagar** simples → DRE mensal simplificado | 1 | v1 |
| **Estoque básico** (baixa automática pela ficha técnica, alerta de mínimo, lista de compras) | 7 | v1 |
| **Cardápio digital / pedido via link (WhatsApp)** sem comissão | 6 | v1 |
| **Entregas**: fila de despacho, motoboy, taxa por bairro, acerto do motoboy | 3 | v1 |
| **Cadastro de clientes + fidelidade simples** (cartão fidelidade digital, cupom) | 6 | v2 |
| **Integração iFood** (receber pedidos via API oficial — exige homologação) | 3, 6 | v2 |
| **Emissão de NFC-e** (via parceiro/API fiscal, não construir do zero) | 9 | v2 |
| **Usuários e permissões** (garçom não dá desconto; gerente sim) + log de cancelamentos | 5, 8 | v1 |
| **Robô de WhatsApp com IA** | 3, 6 | Futuro |

---

## 7. Recomendação de produto

**Público-alvo:** restaurante, lanchonete, hamburgueria ou pizzaria **com 1 unidade**, que
mistura **salão/balcão + delivery**, de 3 a 20 funcionários, dono que faz de tudo.

**Proposta de valor (uma frase):** *"Todos os seus pedidos numa tela, a cozinha sem papel e,
no fim do dia, você sabe quanto realmente ganhou."*

**Por que começar pelo fluxo de pedidos (e não pelo financeiro):**
- É usado **todo dia, o dia todo, por todos** — cria hábito e dificulta a troca de sistema.
- Gera os dados que alimentam o financeiro automaticamente (o dono odeia digitar; planilha
  financeira manual é abandonada).
- KDS é a feature mais "visível" e fácil de vender numa demonstração.
- O financeiro (lucro do dia, CMV, lucro por canal) vira o **diferencial** em cima disso.

---

## 8. Diretrizes de UX e visual (referência: iFood)

O visual do iFood para parceiros funciona porque é **limpo, com muito branco, um vermelho forte
só para o que importa, cards arredondados e status com cor**. Vamos nos *inspirar*, sem copiar
marca/logo (usar identidade própria).

- **Cores**: primária vermelha quente (na linha do iFood, ex. `#EA1D2C`) só em ações principais
  e alertas; fundo branco/cinza bem claro; texto cinza-escuro. Status: **azul** = novo,
  **amarelo/laranja** = em preparo, **verde** = pronto, **cinza** = finalizado, **vermelho** =
  atrasado.
- **Tipografia**: sem serifa, números grandes e legíveis (valores, cronômetros, nº do pedido).
- **Cards** com cantos arredondados (12–16px), sombra leve, informações mais importantes no topo
  (nº do pedido, canal, tempo).
- **Navegação lateral** simples no desktop (Pedidos, Cozinha, Mesas, Caixa, Cardápio,
  Relatórios, Configurações) e barra inferior no celular.
- **Cozinha (KDS)**: tema escuro opcional, fonte enorme, **um toque** para avançar status, sem
  menus, cronômetro sempre visível, som e piscar em pedido novo.
- **Garçom**: mobile-first, alvo de toque ≥ 44px, busca rápida de item, adicionais em "chips".
- **Regra geral**: no máximo **uma ação principal por tela**; tudo a no máximo 2 toques;
  linguagem do restaurante ("comanda", "mesa", "saiu pra entrega"), nada de jargão de software.

---

## 9. Telas sugeridas para o protótipo HTML

1. **Login / escolha de perfil** (Dono, Caixa, Garçom, Cozinha).
2. **Pedidos (central)** — quadro em colunas Novo / Em preparo / Pronto / Saiu-Entregue, filtro
   por canal (Salão, Balcão, WhatsApp, iFood), card com itens, observações e cronômetro.
3. **Cozinha (KDS)** — grade de tickets grandes, cores por tempo, separação por praça, botão
   "Pronto".
4. **Novo pedido / PDV** — cardápio por categoria, carrinho, adicionais, tipo (mesa/balcão/
   entrega), forma de pagamento.
5. **Mesas** — mapa com status e tempo, abrir/fechar conta, dividir conta.
6. **Caixa** — abertura, movimentos, sangria, fechamento com conferência.
7. **Cardápio** — itens, preços, foto, ativar/pausar ("acabou"), preço por canal.
8. **Painel "Hoje" / Relatórios** — faturamento, lucro estimado, por canal, mais vendidos,
   tempo médio de preparo, gráfico por hora.
9. **Ficha técnica / CMV** (v1) — ingredientes, custo do prato, margem por canal, preço
   sugerido.

O protótipo pode ser **um único HTML com dados fictícios**, navegação entre telas e simulação
de pedidos chegando em tempo real (para "sentir" o KDS funcionando).

---

## 10. Riscos e pontos de atenção

- **Fiscal**: NFC-e é obrigatória para venda ao consumidor; regras variam por estado. A Reforma
  Tributária exige campos de IBS/CBS nas notas desde 2026 (fase de teste; Simples/MEI em 2027).
  **Não construir emissor próprio** — usar API fiscal de terceiros (ex.: Focus NFe, PlugNotas,
  eNotas) quando chegar a hora.
- **Integração iFood**: existe API oficial para parceiros de software, mas exige cadastro e
  homologação; e o iFood hoje é dono de concorrentes diretos. Tratar como v2 e não depender dela.
- **Offline**: cozinha e salão não podem parar se a internet cair. Impacta a arquitetura desde o
  início (PWA com armazenamento local + sincronização).
- **Hardware**: muitos restaurantes ainda querem **impressora térmica** na cozinha/balcão;
  suportar impressão é quase obrigatório, mesmo com KDS.
- **LGPD**: dados de clientes (telefone, endereço) exigem cuidado.
- **Suporte**: é o que mais gera reclamação no setor; precisa estar no plano de negócio.

---

## 11. Decisões em aberto (para conversarmos antes do protótipo)

1. Qual **tipo de restaurante** queremos atender primeiro? (lanchonete/hamburgueria com
   delivery é o mais comum e o que mais se beneficia de KDS + central de pedidos)
2. O protótipo deve cobrir **todas as telas da seção 9** ou começamos por Pedidos + Cozinha +
   Painel "Hoje"?
3. Nome e identidade visual próprios (para não confundir com a marca iFood).
4. Pensamos em vender como SaaS (mensalidade) ou é um projeto para um restaurante específico?

---

## Fontes

- Abrasel via Monitor Mercantil — prejuízo no setor: <https://monitormercantil.com.br/cresce-numero-de-bares-e-restaurantes-operando-em-prejuizo/>
- Abrasel via Jornal Contábil — dificuldades das MPEs de alimentação: <https://jornalcontabil.com.br/noticia/micro-e-pequenas-empresas-enfrentam-maiores-dificuldades-no-setor-de-alimentacao-fora-do-lar/amp/>
- Faturamento 2025 e participação dos apps: <https://monitormercantil.com.br/bares-e-restaurantes-faturaram-mais-em-2025/> · <https://www.meioemensagem.com.br/marketing/alimentacao-fora-do-lar-projeta-alta-com-concorrencia-de-apps> · <https://gironews.com/food-service/alimentacao-fora-do-lar-cresce-em-2025-mas-setor-inicia-2026-com-cautela/> · <https://ohoje.com/2026/09/09/alimentacao-fora-do-lar-fatura-mais-mas-custos-apertam-lucro/>
- WhatsApp = 26% do faturamento de delivery (Abrasel): <https://mercadoeconsumo.com.br/16/03/2025/foodservice/whatsapp-representa-26-do-faturamento-com-delivery-em-bares-e-restaurantes/> · <https://gironews.com/food-service/whatsapp-representa-26-do-faturamento-do-food-service-com-delivery/>
- Delivery próprio e dependência do iFood: <https://www.correiobraziliense.com.br/economia/2022/02/amp/4982972-restaurantes-criam-delivery-proprio-para-fugir-da-dependencia-do-ifood.html> · <https://startups.com.br/negocios/estrategia/quem-define-o-ifood-como-um-aplicativo-esta-errado-diz-ceo/> · <https://saipos.com/noticia/restaurantes-investem-em-seus-proprios-deliveries>
- Rotatividade e mão de obra: <https://gironews.com/food-service/turnover-nos-bares-e-restaurantes-registra-alta-e-chega-a-73/> · <https://monitormercantil.com.br/bares-e-restaurantes-enfrentam-crise-de-mao-de-obra/> · <https://www.em.com.br/degusta/2026/01/amp/7330486-como-donos-de-bares-e-restaurantes-lidam-com-os-desafios-para-comecar-2026.html>
- Mortalidade e causas (Sebrae/Abrasel, estudos acadêmicos): <https://repositorio.ufpb.br/jspui/bitstream/123456789/15708/1/LLS13092019.pdf> · <https://www.aedb.br/seget/arquivos/artigos09/195_Mortalidade_nas_MPEs.pdf>
- CMV e ficha técnica: <https://sebraepr.com.br/comunidade/artigo/entendendo-o-cmv-de-restaurante-como-fazer-o-calculo-e-sua-importancia> · <https://blog.cielo.com.br/financas/cmv-o-que-e-como-calcular/?amp=1> · <https://saipos.com/gestao-financeira/planilha-de-precificacao-para-restaurante>
- Comissões iFood: <https://www.serasa.com.br/blog/abrir-loja-no-ifood/> · <https://www.cora.com.br/blog/como-vender-no-ifood/> · <https://www.idinheiro.com.br/negocios/como-vender-no-ifood/>
- Gestor de Pedidos / Portal do Parceiro iFood: <https://saipos.com/integracoes/ifood/ifood-portal> · <https://ajuda.tabletcloud.com.br/integracoes/integracao-com-ifood-o-que-preciso-saber>
- Aquisições do iFood: <https://www.bloomberglinea.com.br/negocios/ifood-adquire-tres-empresas-de-gestao-e-avanca-pelo-salao-dos-restaurantes/> · <https://startups.com.br/negocios/ifood-compra-tres-startups-para-ser-o-all-in-one-dos-restaurantes/> · <https://startups.com.br/negocios/exclusivo-ifood-compra-a-anota-ai-para-oferecer-atendimento-pelo-whatsapp/>
- Concorrentes e preços: <https://saipos.com/planos-e-precos> · <https://reidodelivery.com.br/blog/saipos-ou-anota-ai> · <https://www.abrahao.com.br/blog/tecnologia-e-tendencias/goomer-sistema-para-restaurantes> · <https://goomer.com.br/sobre-nos> · <https://www.sisfood.com.br/saiba-mais/sistema-pdv/melhor-sistema-restaurante-otimizado> · <https://olaclick.com/ranking-melhores-sistemas-para-restaurantes/> · <https://conteudo.stone.com.br/restaurantes-6-softwares-para-te-ajudar-na-gestao> · <https://gironews.com/food-service/site-e-app-para-restaurantes-53537/>
- Reclamações de usuários de sistemas: <https://www.reclameaqui.com.br/empresa/saipos/> · <https://www.reclameaqui.com.br/colibri-sistemas-de-informatica/sistema-de-gestao-para-pasteleiros-lentidao-travamentos-e-suporte-ineficiente_pQodjZ6u5i6pBYC9/>
- KDS e comanda digital: <https://www.omie.com.br/blog/kds-kitchen-display-system/> · <https://www.ledware.com.br/2026/05/06/comandas-digitais-em-restaurantes-5-erros-que-custam-caro/> · <https://saipos.com/sistema/restaurante/monitor-kds-para-restaurante>
- Reforma Tributária (IBS/CBS) para restaurantes: <https://blog.econeteditora.com.br/?p=26865> · <https://gironews.com/food-service/nova-regra-evita-rejeicao-de-notas-fiscais-por-erros-em-ibs-e-cbs/> · <https://sefaz.es.gov.br/Media/Sefaz/Links/Nota%20IBS%20CBS%20Sefaz.pdf>
