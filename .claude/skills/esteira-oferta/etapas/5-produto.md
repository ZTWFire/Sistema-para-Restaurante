# Etapa 5 — Produto

Leia `etapas/regras.md` antes de começar.

Objetivo: definir um produto que **entrega de verdade** o que promete, com escada de valor
simples: produto principal + bônus + order bump + upsell.

## Decisões
- **Promessa principal:** resultado específico + prazo ou esforço ("…em 15 minutos por dia",
  "…sem gastar mais de R$ 150 por semana"). Precisa ser algo que o cliente consegue verificar.
- **Mecanismo:** o nome do jeito de fazer (ex.: "Método Marmita 3x3"). Explica por que dessa vez
  funciona. Nome curto, fácil de lembrar, sem prometer milagre.
- **Nome do produto:** até 5 palavras, diz o que é.
- **Formato:** escolha o que o público usa mais fácil (PDF para ler no celular, planilha para
  quem gosta de controle, checklist imprimível, pack de modelos).
- **Preço:** principal entre R$ 19,90 e R$ 37 (low ticket), ancorado num valor maior real
  (soma dos bônus ou preço de alternativa). Order bump entre R$ 9,90 e R$ 19,90. Upsell entre
  R$ 37 e R$ 97.
- **Garantia:** 7 dias (é o direito de arrependimento do CDC em compras online; diga isso como
  segurança, não como favor).

## Formato de saída (`5-produto.md`)
```
# Produto — <nome>

| Item | Definição |
|---|---|
| Promessa principal | |
| Mecanismo | |
| Nome | |
| Formato | |
| Preço / ancoragem | |
| Garantia | 7 dias |

## Sumário do produto principal
<capítulos ou seções com 1 linha cada sobre o que o cliente consegue fazer depois de ler>

## Bônus (2 ou 3, baratos de produzir e ligados a uma objeção)
| Bônus | Que objeção resolve | Formato | Valor percebido |
|---|---|---|---|

## Order bump
Nome, preço, o que é e por que combina com a compra principal (1 frase).

## Upsell
Nome, preço, o que é, e downsell se o upsell for recusado.

## Plano de produção com IA
| Peça | Como produzir | Tempo estimado |
|---|---|---|
(ex.: texto com Claude por capítulo → revisão humana → diagramação no Canva → exportar PDF;
planilha no Google Sheets com fórmulas; capa e mockup 3D)

## Checklist de qualidade antes de vender
- [ ] Cada promessa da página está entregue em algum capítulo
- [ ] Nada genérico que a pessoa acharia de graça no primeiro resultado do Google
- [ ] Exemplos práticos, listas, modelos prontos para copiar
- [ ] Leitura confortável no celular
- [ ] Revisado por um humano (português e fatos)
```

## Produção do material (só se o usuário pedir)
Se o usuário pedir "produz o material", escreva o conteúdo completo capítulo por capítulo em
`ofertas/<apelido>/produto/` (um arquivo por capítulo + bônus), seguindo o sumário. Entregue um
capítulo de cada vez se o conteúdo for longo e pergunte se segue. Para gerar PDF, use a skill de
PDF se disponível.
