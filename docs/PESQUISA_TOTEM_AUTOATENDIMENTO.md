# Pesquisa — Totem de autoatendimento

> Levantamento feito em outubro/2026 para entender como funciona um sistema de totem de
> autoatendimento (o cliente escolhe, personaliza e paga sozinho) e preparar um protótipo em HTML.
> Preços e números de desempenho vêm em boa parte de fabricantes e blogs do setor; trate-os como
> ordem de grandeza. Fontes no final.

---

## 1. Resumo

1. **O que é:** uma tela touch (tablet, totem de bancada ou totem de chão) com um app em modo
   "quiosque". O cliente monta o pedido, paga ali mesmo (cartão, Pix) ou no caixa, recebe uma
   **senha** e o pedido cai direto na cozinha. Quando fica pronto, a senha é chamada num painel.
2. **Por que o dono compra:** menos fila no pico, menos erro de pedido (o cliente digita o próprio
   pedido), menos dependência de atendente (o setor tem rotatividade acima de 70% ao ano) e venda
   de adicionais sem constrangimento.
3. **Ticket médio — cuidado com a propaganda:** fabricantes falam em +10% a +30%. Não há estudo
   independente que confirme um ganho geral; o único estudo acadêmico de campo encontrado mostrou
   pedidos **mais rápidos (~17%)**, mas não maiores. O ganho real depende de **fotos boas,
   combos e sugestões bem configuradas**. É argumento de venda, não promessa.
4. **O mercado está esquentando no Brasil:** o **iFood comprou o software de totens da Videosoft**
   em junho/2025 (mais de 25 mil totens instalados) e testou em 500 restaurantes; a **Saipos**
   (também do iFood) tem totem próprio; a **Goomer** lançou totem vertical integrado; KFC já tem
   totem em 88% das lojas.
5. **Custos de referência:** hardware de **R$ 4 mil (bancada) a R$ 25 mil (premium)**; totem de
   chão 21" com impressora e pinpad em torno de **R$ 9–16 mil** no varejo; software de
   **R$ 100–500/mês**; locação completa de **R$ 480 a R$ 1.300/mês** por unidade.
6. **Oportunidade para nós:** a versão **tablet** (Android/iPad de 10–11" num suporte, com Pix na
   tela e maquininha ao lado) é a porta de entrada barata para sorveterias, açaiterias,
   cafeterias e lanchonetes pequenas — o público que o totem de R$ 15 mil não alcança.

---

## 2. Onde se usa

| Segmento | Para que serve | Particularidade |
|---|---|---|
| Fast food / hamburgueria | Pedido + pagamento + senha | Combos, "ponto da carne", retirar ingredientes |
| Praça de alimentação | Reduzir fila no balcão | Pico curto e intenso |
| **Sorveteria / açaiteria** | "Monte o seu" | Tamanho, sabores, complementos inclusos x pagos; às vezes vendido por peso |
| Cafeteria / padaria | Pedido rápido | Tamanho, tipo de leite, extras |
| Restaurante com salão | Pedido na mesa (tablet) ou no balcão | Comanda vinculada à mesa |
| Cinema, estacionamento, eventos | Venda de ingresso/ficha | Sem cozinha |
| Varejo / farmácia | Consulta de preço, retirada de pedido online | Leitor de código de barras |
| Clínicas, bancos, órgãos públicos | Emissão de senha e check-in | Sem pagamento |

---

## 3. Como funciona por dentro

```
                 ┌───────────────── Painel de gestão (web) ─────────────────┐
                 │ cardápio, fotos, preços, combos, horários, relatórios    │
                 └──────────────┬───────────────────────────────────────────┘
                                │ sincroniza cardápio
 Cliente ──► [ TOTEM / TABLET ] ┼──► Pagamento: pinpad/TEF · maquininha integrada · Pix QR
             app em modo        │
             quiosque           ├──► Nota fiscal (NFC-e) — via API fiscal
                                ├──► Impressora térmica: comprovante + senha
                                ├──► Cozinha: KDS (tela) ou impressora da cozinha
                                └──► Painel de senhas: "Pedido 042 pronto"
```

### Peças de hardware
| Peça | Função | Observação |
|---|---|---|
| **Tela touch** | Interface | Capacitiva; 10–11" (tablet), 15,6–21,5" (bancada/chão), 27–32" (chão premium). Formato vertical é o padrão |
| **Computador** | Roda o app | Android (mais comum no Brasil), Windows (totens antigos) ou iPad |
| **Impressora térmica 80 mm** | Comprovante e senha | Com corte automático; pode ser dispensada com senha na tela/SMS |
| **Pagamento** | Cartão e Pix | Pinpad via TEF (Sitef, PayGo), maquininha smart integrada ou Pix QR na tela |
| **Leitor QR/código de barras** | Cupom, cartão fidelidade, retirada | Opcional |
| **Gabinete** | Proteção | Metal, travado, cabos escondidos, ventilação |

### Peças de software
1. **App do totem** — roda travado em uma única tela (no Android, *Lock Task Mode* via
   gerenciador de dispositivos; no iPad, *Acesso Guiado*). O cliente não consegue sair do app, e
   ele reabre sozinho se travar.
2. **Painel de gestão** — o dono cadastra cardápio, fotos, adicionais, combos, preços e liga ou
   desliga itens ("acabou o açaí de cupuaçu").
3. **Integrações** — sistema de gestão/PDV, cozinha (KDS), painel de senhas, pagamentos e fiscal.
4. **Monitoramento remoto** — avisa se o totem caiu, ficou sem papel ou perdeu a internet.

### Pagamento no Brasil (as opções)
| Opção | Como funciona | Prós | Contras |
|---|---|---|---|
| **Pinpad + TEF** | Pinpad (Gertec etc.) ligado ao totem; software de TEF conversa com a adquirente | Padrão dos totens grandes; aceita tudo | Homologação, configuração e custo maiores |
| **Maquininha smart integrada** | Maquininha Android (Stone, PagBank, Mercado Pago…) recebe o valor via API/integração | Barato, já existe na loja | Depende da integração de cada adquirente |
| **Pix QR dinâmico na tela** | Totem gera QR com o valor exato; confirmação automática | **Não precisa de hardware**; taxa baixa | Só Pix |
| **Pix por aproximação** | Cliente encosta o celular | Rápido | Novo; nem todo terminal suporta |
| **Pagar no caixa** | Totem só envia o pedido; paga no balcão | Funciona sem integração | Ainda tem fila no caixa |

### Fiscal
- Venda ao consumidor exige **NFC-e** (São Paulo encerrou o SAT em 31/12/2025; desde 2026 é NFC-e).
- NFC-e precisa de certificado digital A1, CSC da Fazenda e **internet em tempo real**; se cair,
  entra em **contingência offline**, com prazo para regularizar. O totem precisa prever isso.
- Recomendação: usar uma **API fiscal de terceiros** (Focus NFe, PlugNotas, NFe.io), não
  construir emissor próprio.

---

## 4. Jornada do cliente (o fluxo de telas)

| # | Tela | O que acontece | Boas práticas |
|---|---|---|---|
| 1 | **Tela de descanso** | Vídeo/foto de destaque, "Toque para pedir" | Mostrar o produto mais desejado; promo do dia |
| 2 | **Comer aqui ou levar** | Define embalagem e, às vezes, preço | Dois botões enormes |
| 3 | **Cardápio** | Categorias à esquerda/topo, produtos em cards com foto e preço | Foto grande; destaques ("mais pedido") |
| 4 | **Produto** | Tamanho, sabores, adicionais, retirar ingredientes, observação | Mostrar preço atualizando; limites claros ("escolha até 3") |
| 5 | **Sugestão (upsell)** | "Que tal uma bebida?" / "Transforme em combo" | **Uma vez só**, fácil de recusar |
| 6 | **Carrinho** | Revisar, alterar quantidade, remover | Sempre visível em barra fixa |
| 7 | **Identificação** | Nome para chamar, CPF na nota (opcional), telefone para fidelidade | Tudo opcional; teclado grande |
| 8 | **Pagamento** | Escolher cartão, Pix ou pagar no caixa | Instruções visuais ("aproxime o cartão") |
| 9 | **Confirmação** | Senha grande, tempo estimado, comprovante | Volta sozinho à tela 1 em ~15 s |
| 10 | **Painel de senhas** (TV) | "Em preparo" e "Pronto" | Som e destaque ao chamar |

Proteções em todas as telas: botão **Recomeçar**, botão **Voltar**, aviso **"Ainda está aí?"**
após ~60 s parado (com contagem e opção de continuar), e limpeza total do pedido ao voltar à
tela inicial.

---

## 5. Formatos de equipamento

| Formato | Tela | Custo aproximado | Para quem | Prós | Contras |
|---|---|---|---|---|---|
| **Tablet em suporte** (bancada) | 10–11" | R$ 1,5–4 mil (tablet + suporte antifurto) | Sorveteria, café, lanchonete pequena | Barato, rápido de instalar | Tela pequena; pagamento separado |
| **Totem de bancada** | 15,6–21,5" | R$ 4–7 mil | Lanchonetes, quiosques | Compacto, com impressora | Ocupa balcão |
| **Totem de chão** | 21,5–27" | R$ 8–16 mil | Fast food, praça de alimentação | Visível, completo (impressora + pinpad) | Caro; precisa de espaço |
| **Totem premium / 32"** | 27–32" | R$ 18–25 mil | Redes | Impacto visual | Caro |
| **Locação completa** | — | R$ 480–1.300/mês + setup | Quem não quer comprar | Suporte e troca incluídos | Custo mensal alto |

**iPad x Android:** no Brasil, Android domina porque as maquininhas smart e os pinpads integram
melhor com ele, e o hardware é mais barato. iPad funciona bem em **Acesso Guiado** com pagamento
por **Pix QR na tela** ou maquininha separada. Para o nosso produto, o ideal é um **app web/PWA**
que roda em qualquer um dos dois.

---

## 6. Concorrentes

### Brasil
| Empresa | O que oferece | Destaque | Preço (aprox.) |
|---|---|---|---|
| **iFood / Videosoft** | Software de totem (iFood) + hardware (Videosoft) | 25 mil+ totens instalados; iFood comprou o software em jun/2025 e testou em 500 restaurantes | Locação a partir de ~R$ 979/mês (fonte não oficial) |
| **Saipos** *(iFood)* | Totem PDV 15,6" com impressora e Tablet PDV 11" | Integra direto à cozinha e ao sistema de gestão; diz "até +20% de ticket" | Sob demonstração |
| **Goomer** | Totem vertical com pedido, pagamento e impressão integrados; configuração remota | Integra com TOTVS Chef, NCR Colibri, Aloha, Teknisa | Sob consulta |
| **Consumer** | Módulo de autoatendimento no sistema | Público pequeno/médio | Sob consulta |
| **SisFood, CPlug, TabletCloud, Gototem** | Sistemas com módulo de totem | Totem como módulo adicional | Sistema a partir de ~R$ 150/mês + módulo |
| **Datacake** | Locação de totem | Pacote com hardware | A partir de ~R$ 484/mês + setup de R$ 5 mil |
| **PagBank (PagTotem), Mercado Pago** | Totem com maquininha integrada / Pix por aproximação | Pagamento nativo | Atrelado às taxas |
| **Gertec, TAS, Simpress** | Hardware (totens, pinpads) | Fabricantes | R$ 8–16 mil (21–32") |

### Fora do Brasil (referência de produto)
**McDonald's/Acrelec** (o padrão de UX do setor), **GRUBBRR**, **Square Kiosk** (roda em iPad),
**Toast Kiosk**. A lição deles: o totem que funciona é o que **parece o app de delivery que o
cliente já usa** — fotos, cards, carrinho fixo, poucos passos.

### Leitura competitiva
- Os grandes vendem **hardware caro + contrato longo**. O pequeno comércio (sorveteria, açaí,
  café) fica de fora.
- O iFood está fechando o ecossistema (Saipos + Videosoft + Anota AI). Um concorrente
  independente precisa ser **barato, rodar em tablet comum e se integrar com qualquer
  maquininha ou Pix**.

---

## 7. Dores

### Do dono
| Dor | Como o totem ajuda |
|---|---|
| Fila no horário de pico, cliente desiste | Vários pedidos simultâneos; caixa só entrega |
| Erro de pedido (atendente entendeu errado) | O próprio cliente escolhe; vai direto para a cozinha |
| Falta de atendente e rotatividade alta | Um totem cobre parte do caixa |
| Atendente esquece de oferecer adicional | Sugestão automática, toda vez |
| Cardápio com muitas variações (açaí, pizza, burger) | Montagem guiada com limites e preço calculado |
| Preço desatualizado em cardápio impresso | Muda no painel e vale na hora |

### Do cliente (o que o totem precisa evitar)
| Dor | Solução de UX |
|---|---|
| Totem lento ou travado | App leve, sem carregamento entre telas; monitoramento |
| Pagamento que falha | Mensagem clara, tentar de novo ou "pagar no caixa" |
| Pessoas idosas ou com pouca familiaridade | Letras grandes, poucos passos, botão "chamar atendente" |
| Cadeirantes e pessoas baixas não alcançam o topo da tela | **Modo acessível**: traz o conteúdo para a metade de baixo |
| Ter que digitar muito | Nome, CPF e telefone opcionais |
| Não saber quando o pedido fica pronto | Senha grande + painel + tempo estimado |

---

## 8. Funcionalidades

### Lado do cliente (o totem)
| Funcionalidade | MVP? | Como funciona |
|---|---|---|
| Tela de descanso com destaque/promoção | ✅ | Carrossel de fotos; qualquer toque inicia |
| Comer aqui / Para levar | ✅ | Define embalagem e aparece no ticket da cozinha |
| Cardápio por categorias com fotos | ✅ | Barra de categorias + grade de cards |
| Montagem do produto (tamanho, sabores, complementos) | ✅ | Etapas com limite ("até 3 grátis, depois R$ 2 cada"), preço ao vivo |
| Retirar ingrediente / observação | ✅ | Chips "sem cebola"; observação curta |
| Sugestão inteligente (upsell) | ✅ | Uma vez, antes do carrinho, baseada no que foi escolhido |
| Carrinho fixo com total | ✅ | Barra inferior; editar quantidade |
| Nome para chamar, CPF na nota | ✅ | Opcionais |
| Pagamento: cartão (pinpad/maquininha), Pix QR, pagar no caixa | ✅ | Pix com QR dinâmico e confirmação automática |
| Senha e tempo estimado | ✅ | Tela final + impressão opcional |
| Inatividade e reinício | ✅ | Aviso após 60 s; limpa tudo |
| Modo acessível e idioma (PT/EN/ES) | v1 | Botões fixos no rodapé |
| Cupom e fidelidade (telefone ou QR) | v1 | "Você tem 1 açaí grátis" |
| Chamar atendente | v1 | Aciona aviso no balcão |

### Lado da loja (painel)
| Funcionalidade | MVP? |
|---|---|
| Cadastro de cardápio com fotos, grupos de complementos e regras (mín/máx, grátis/pagos) | ✅ |
| Ligar/desligar item ("acabou") em tempo real | ✅ |
| Combos e sugestões configuráveis | ✅ |
| Tela da cozinha (KDS) ou impressão na cozinha | ✅ |
| Painel de senhas para TV | ✅ |
| Relatórios: vendas por hora, itens mais vendidos, taxa de aceite das sugestões, pedidos abandonados | v1 |
| Vários totens e lojas, monitoramento (online, papel, erro) | v1 |
| Horários e cardápio por período (café da manhã x almoço) | v1 |
| Integração iFood/PDV, NFC-e via API fiscal | v2 |

---

## 9. Diretrizes de interface para totem

- **Alvos de toque grandes:** mínimo 44×44 px pela regra geral; em totem, usar **≥ 64 px** e
  espaçamento generoso — as pessoas tocam em pé, com pressa, às vezes com a mão suja.
- **Fotos grandes e apetitosas** em todo item. Sem foto, o totem vira só um caixa sem atendente.
- **Contraste** mínimo 4,5:1 para texto; fonte de corpo ≥ 18 px em totem grande.
- **Fluxo linear** com indicador de etapa na montagem do produto.
- **Preço sempre visível** e atualizado a cada escolha; nada de surpresas no final.
- **Upsell uma vez só**, com "Não, obrigado" do mesmo tamanho que "Adicionar".
- **Ações principais embaixo** (a mão alcança melhor); em totem de chão, nada importante acima de
  ~1,20 m do chão; oferecer modo acessível.
- **Feedback imediato:** animação ao adicionar ao carrinho, som discreto, vibração no tablet.
- **Sem teclado sempre que possível.** Se precisar, teclado grande na tela.
- **Inatividade:** aviso com contagem regressiva; o padrão de acessibilidade pede que o usuário
  possa estender o tempo.
- **Cores da marca do cliente** (o totem é personalizável por loja) — o sistema é a "moldura".

---

## 10. Particularidades de sorveteria / açaiteria (o caso citado)

- Vendido de três jeitos: **por tamanho** (300 ml, 500 ml, 700 ml), **por peso** (self-service com
  balança) ou **copo pronto** (receitas da casa).
- "**Monte o seu**": etapas típicas — tamanho → base (açaí tradicional, zero, cupuaçu, sorvete) →
  **complementos inclusos** (ex.: até 3 grátis) → **complementos pagos** (Nutella, morango,
  leite Ninho) → coberturas/caldas → finalização.
- O totem **não pesa** sozinho. Para venda por peso: cliente escolhe extras no totem, a balança
  do caixa registra o peso e o pagamento é feito no caixa, **ou** o totem vende só por tamanho.
  No protótipo, usar **venda por tamanho**.
- Upsell natural: "dobro de Nutella por + R$ 4", "leve uma água", "+100 ml por + R$ 3".

---

## 11. Proposta para o protótipo em HTML

**Cenário:** uma açaiteria/sorveteria fictícia (com marca própria, fotos ilustradas), porque o
"monte o seu" é o fluxo mais rico e mostra bem o valor do totem. Alternativa: hamburgueria.

**Telas:**
1. Descanso com destaque e "Toque para começar".
2. Comer aqui / Para levar.
3. Cardápio: categorias (Monte seu açaí, Copos da casa, Sorvetes, Milk-shakes, Bebidas), cards com
   foto, selo "mais pedido".
4. Montagem em etapas com preço ao vivo e limite de complementos grátis.
5. Sugestão (upsell) antes do carrinho.
6. Carrinho com edição.
7. Nome para chamar + CPF opcional.
8. Pagamento simulado: **Pix com QR e confirmação automática**, **cartão ("aproxime ou insira")**
   e **pagar no caixa**.
9. Senha grande, tempo estimado e volta automática ao início.
10. Extras para demonstração: alternância **tablet (horizontal) x totem (vertical)**, painel de
    senhas e aviso de inatividade.

---

## 12. Decisões em aberto

1. Nicho do protótipo: **açaí/sorveteria** (recomendado) ou hamburgueria/lanchonete?
2. Nome e cores da marca fictícia (ou uso uma sugestão minha)?
3. Incluir o painel da loja (cadastro de cardápio, cozinha) no protótipo, ou só a experiência do
   cliente no totem?

---

## Fontes

- Goomer — melhores totens para restaurantes 2026: <https://goomer.com.br/blog/totens-autoatendimento-restaurantes>
- Goomer lança totem vertical: <https://gironews.com/food-service/goomer-lanca-totem-vertical-para-reduzir-filas-e-erros-no-foodservice/> · <https://centraldovarejo.com.br/?p=35593> · <https://www.baguete.com.br/noticias/goomer-recebe-aporte-da-domo-invest>
- SisFood — autoatendimento e preço/ROI: <https://www.sisfood.com.br/saiba-mais/autoatendimento> · <https://sisfood.com.br/saiba-mais/autoatendimento/quanto-custa-totem-autoatendimento>
- Datacake — quanto custa totem: <https://www.datacake.com.br/blog/quanto-custa-totem-de-autoatendimento/>
- Totemdeautoatendimento.com.br — compra e locação: <https://totemdeautoatendimento.com.br/quanto-custa/>
- Food Connection — totem no food service: <https://www.foodconnection.com.br/tecnologia/totem-de-autoatendimento-como-tecnologia-impacta-o-food-service/>
- Zip Automação — vale a pena?: <https://blog.zipautomacao.com.br/totem-de-autoatendimento-em-restaurantes/>
- Tendências food service 2026: <https://sistemacatedral.com.br/blog/tendencias-tecnologia-food-service-2026/>
- iFood — o que é totem: <https://blog-parceiros.ifood.com.br/o-que-e-totem-de-autoatendimento/>
- iFood compra software da Videosoft: <https://www.baguete.com.br/noticias/ifood-compra-divisao-da-videosoft> · <https://gironews.com/food-service/ifood-adquire-software-de-autoatendimento-da-videosoft/> · <https://timesbrasil.com.br/empresas-e-negocios/tecnologia-e-inovacao/ifood-adquire-software-para-totens-de-autoatendimento-da-videosoft/> · <https://www.bloomberglinea.com.br/negocios/ifood-faz-nova-aquisicao-e-reforca-plano-para-crescer-no-salao-dos-restaurantes/>
- Saipos — totem de autoatendimento: <https://saipos.com/sistema/totem-de-autoatendimento> · <https://gironews.com/food-service/saipos-lanca-totem-para-ampliar-eficiencia-no-food-service/>
- KFC com totens em 88% das lojas: <https://mercadoeconsumo.com.br/tag/frango-frio/>
- Hardware e preços de varejo: <https://m.magazineluiza.com.br/busca/totem+21+polegadas+vertical/> · <https://simpress.com.br/wp-content/uploads/2025/08/Catalogo-PTB200-Totem-de-21-e-27-Polegadas.pdf> · <https://www.mercadolivre.com.br/loja/gertec>
- Pagamentos e Pix em totens: <https://www.mercadopago.com.br/blog/pix-por-aproximacao-totem-autoatendimento-lanchonetes-cafes> · <https://blog.pagbank.com.br/conheca-o-pagtotem> · <https://tecnoblog.net/391576/mcdonalds-testa-pix-para-pagar-via-autoatendimento-no-brasil/> · <https://manual.cplug.com.br/books/tef/chapter/instala%C3%A7%C3%A3o-pix/export/pdf>
- Instalação de totem, KDS e pinpad: <https://ajuda.tabletcloud.com.br/integracoes/o-que-e-o-autoatendimento-food/como-realizar-a-instalacao-totem-kds-e-pinpad>
- Fiscal (fim do SAT em SP, NFC-e): <https://online.crcsp.org.br/portal/noticias/noticia.asp?c=10087> · <https://nfe.io/blog/?p=13580>
- Modo quiosque Android: <https://developer.android.com/work/dpc/dedicated-devices/lock-task-mode> · <https://blog.scalefusion.com/turning-android-devices-single-app-kiosk-mode>
- Ticket médio (visão crítica e de fornecedores): <https://www.duck-hub.com/blog/self-service-kiosk-statistics> · <https://blog.epson.com/self-order-kiosks-in-the-fast-food-space> · <https://www.restroworks.com/blog/self-ordering-kiosk-restaurant-statistics-2025/>
- UX e acessibilidade de totens: <https://acrelec.com/wp-content/uploads/2024/03/10-Guiding-Principles-for-Kiosk-UX_2024.pdf> · <https://xchange.avixa.org/posts/kiosk-ux-ui-design-checklist> · <https://seenlabs.com/blog/ada-compliance-for-self-order-kiosks-what-restaurant-operators-must-know> · <https://vispero.com/4-tips-to-make-food-and-hospitality-kiosks-accessible-for-everyone/> · <https://collections.ncrvoyix.com/resource/how-to-offer-more-self-service-kiosk-accessibility-and-better-experiences-for-customers-with-disabilities>
- Plataformas internacionais: <https://oliverpos.com/en-ca/best-kiosk-software-restaurants/>
- Dores do autoatendimento: <https://consumidormoderno.com.br/dores-autoatendimento-consumidores/>
- Como açaiterias vendem "monte o seu" (cardápios): <https://99app.com/99food/rio-de-janeiro/pegue-e-monte-aaiteria-e-sorveteria/5764609655708585498/> · <https://99app.com/99food/curitiba/bahiana-aai-e-sorvetes-gourmet-sao-jose-dos-pinhais/5764611628637882136/>
