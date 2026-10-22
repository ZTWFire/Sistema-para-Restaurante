# Etapa 1 — Mineração e sinais de escala

Objetivo: responder **"essa oferta está vendendo agora?"** com evidência, não com impressão.

## Se o usuário mandou um nicho (sem oferta)
Sugira de 6 a 10 buscas para a Biblioteca de Anúncios (país Brasil, status ativo) combinando o
tema com termos de entregável e de preço:

- Entregável: `guia`, `manual`, `pdf`, `e-book`, `passo a passo`, `checklist`, `planilha`,
  `kit`, `pack`, `modelos prontos`, `apostila`, `cardápio`, `receitas`, `método`
- Oferta: `acesso imediato`, `pagamento único`, `baixe agora`, `R$ 19,90`, `R$ 27`, `R$ 37`,
  `por apenas`, `garantia de 7 dias`
- Plataformas no texto ou no link: `hotmart`, `kiwify`, `cakto`, `pay.`, `go.`

Se a ferramenta da Biblioteca estiver disponível, rode as 3 buscas mais promissoras e traga as
ofertas encontradas para a tabela abaixo.

## Sinais de escala (pontue cada oferta)
| Sinal | Como ver | Pontos |
|---|---|---|
| Anúncio ativo há 7–29 dias | Data de início | 1 |
| Ativo há 30 dias ou mais | Data de início | 2 |
| 5 a 19 anúncios ativos da mesma oferta | Contagem na página do anunciante ou "X anúncios usam esse criativo" | 1 |
| 20 ou mais anúncios ativos | Idem | 2 |
| Mesma landing page anunciada por 2+ páginas diferentes | Busca pelo domínio da LP | 2 |
| Criativos novos nos últimos 7 dias | Datas recentes | 1 |
| Vários formatos (vídeo, imagem, carrossel) | Biblioteca | 1 |
| Rodando em vários posicionamentos | Detalhes do anúncio | 1 |

Leitura: **0–3 = fraco**, **4–6 = validado**, **7+ = escalando**. Só siga com 4 ou mais.

Atenção: um único anúncio antigo pode ser só esquecido. O que pesa é volume + criativos novos.

## Formato de saída (`1-mineracao.md`)
```
# Mineração — <apelido>
Data da análise: <data>

| Oferta | Página/anunciante | Link da LP | Ativo desde | Nº anúncios | Sinais | Nota | Status |
|---|---|---|---|---|---|---|---|

Oferta escolhida para o raio-x: <nome> — motivo em 1 frase.
Buscas que o usuário deve repetir manualmente (se a ferramenta não estava disponível): <lista>
```
