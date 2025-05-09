# Análise de Comportamento do Consumidor: Insights Baseados em Dados com SQL

**Sobre o Dataset:**

Este conjunto de dados com 1000 registros, oferece um raio-x completo do comportamento do consumidor, capturando desde padrões de compra até preferências individuais. Com informações detalhadas sobre:

Dados demográficos (idade, localização, perfil socioeconômico, estado civil, gênero)

Padrões de compra (intenção, tempo de decisão, sensibilidade a desconto)

Satisfação e engajamento (avaliações, taxas de retorno, engajamento rede social, engajamento com anúncios, programa de fidelidade)

Interações com produtos (categorias e-commerce, ticket médio, receita, métodos de pagamento)

Por que ele é valioso?

✔️ Segmentação precisa de públicos-alvo

✔️ Entender como os clientes se comportam

✔️ Otimização de campanhas de marketing

Ideal para quem quer entender o consumidor na prática.

**Separei todas as querys no repositório, onde você pode visualizar separadamente cada uma. Além disso trouxe abaixo o que cada query retornou como output, de acordo com o questionamento realizado em cima do dataset e a análise dos dados retornados.**

**Para ver todo o repositório completo no Github, acesse [Análise de Comportamento do Consumidor: Insights Baseados em Dados com SQL](https://github.com/dorrigo/comportamento-consumidor-sql/blob/main/README.md)**


## Query_1

### Nossa campanha de anúncios está gerando resultados? Clientes que engajam com nossos anúncios compram mais do que os outros?

Output Query_1

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>engagement_with_ads</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>High</td>
<td class='normal' valign='top'>270</td>
<td class='normal' valign='top'>7.0074</td>
<td class='normal' valign='top'>277.6407</td>
<td class='normal' valign='top'>74963</td>
</tr>

<tr>
<td class='normal' valign='top'>Low</td>
<td class='normal' valign='top'>230</td>
<td class='normal' valign='top'>7.1565</td>
<td class='normal' valign='top'>268.2609</td>
<td class='normal' valign='top'>61700</td>
</tr>

<tr>
<td class='normal' valign='top'>Medium</td>
<td class='normal' valign='top'>244</td>
<td class='normal' valign='top'>7.0328</td>
<td class='normal' valign='top'>281.2131</td>
<td class='normal' valign='top'>68616</td>
</tr>

<tr>
<td class='normal' valign='top'>None</td>
<td class='normal' valign='top'>256</td>
<td class='normal' valign='top'>6.6055</td>
<td class='normal' valign='top'>272.6094</td>
<td class='normal' valign='top'>69788</td>
</tr>
</table>
</body></html>

**Principais Insights**

1. Clientes com alto engajamento em anúncios:
    - Representam a maior parcela de receita
    - Geram **7% a mais de receita** que clientes sem engajamento e **17.6% a mais** dos com baixo engajamento
    - Frequência de compra: **7/mês** (acima da média geral 6.95)

2. Oportunidades de melhoria:
    - Clientes com baixo engajamento trazem a menor participação de receita e ticket médio, menos do que os não engajam com anúncios
    - Clientes sem nenhum nível de engajamento com frequência de compra abaixo da média

**Estratégias Propostas**

**Campanha para Clientes com Baixo Engajamento**
- **Público-alvo:** Clientes que engajaram nos últimos 6 meses (excluindo clientes engajados nos últimos 30 dias)
- **Objetivo:** Aumentar conversão e nível de engajamento da base com baixo engajamento nos anúncios
- **Principais KPIs:** Ticket médio, receita e nível de engajamento

**Campanha para Não Engajados**
- **Público-alvo:** Clientes sem engajamento nos últimos 180 dias
- **Objetivo:** Aumentar o nível de engajamento e frequência de compra dos clientes não engajados
- **Principais KPIs:** Frequência de compra e nível de engajamento

## Query_2

### O nível de engajamento nas redes sociais gera mais receita?

Output Query_2

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>social_media_influence</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>None</td>
<td class='normal' valign='top'>247</td>
<td class='normal' valign='top'>6.8988</td>
<td class='normal' valign='top'>262.7935</td>
<td class='normal' valign='top'>64910</td>
</tr>

<tr>
<td class='normal' valign='top'>Low</td>
<td class='normal' valign='top'>249</td>
<td class='normal' valign='top'>7.1165</td>
<td class='normal' valign='top'>272.5181</td>
<td class='normal' valign='top'>67857</td>
</tr>

<tr>
<td class='normal' valign='top'>Medium</td>
<td class='normal' valign='top'>236</td>
<td class='normal' valign='top'>6.9788</td>
<td class='normal' valign='top'>280.1102</td>
<td class='normal' valign='top'>66106</td>
</tr>

<tr>
<td class='normal' valign='top'>High</td>
<td class='normal' valign='top'>268</td>
<td class='normal' valign='top'>6.7985</td>
<td class='normal' valign='top'>284.3060</td>
<td class='normal' valign='top'>76194</td>
</tr>
</table>
</body></html>

**Principais Insights**

1. **Receita por Nível de Engajamento**:
    - Clientes com **alto engajamento** geram a **maior receita total** (R$76,194)
    - A diferença entre alto e nenhum engajamento é de **+17.4%** em receita total

2. **Ticket Médio**:
    - Cresce progressivamente com o engajamento (de R$262.79 para R$284.31)
    - Clientes com alto engajamento gastam **8.2% mais** por compra

3. **Frequência de Compra**:
    - Relação inversa: engajamento mais alto tem uma frequência ligeiramente menor e abaixo da média geral (6.94)
    - Clientes com **baixo engajamento** compram com maior frequência (7.12/mês)

**Estratégias Propostas**

**Aumento do ticket médio**:
  - Oferecer para o cliente na hora da compra opções de *cross-selling* e *upselling* (**compre junto e oferecer produto mais completo**)
  - Ações de marketing para produtos de ticket alto

**Converter níveis mais baixos de engajamento**:
  - Utilizar postagens com promoções pontuais de curta duração
  - Ações semanais nas redes sociais para aumentar frequência de compra
  - Implementar estratégias de ativação via redes sociais


## Query_3

### O programa de fidelidade está aumentando o valor dos clientes? Membros compram com mais frequência e gastam mais?

Output Query_3

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>customer_loyalty_program_member</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>receita_total</td>
<td bgcolor=silver class='medium'>media_satisfacao_consumidor</td>
</tr>

<tr>
<td class='normal' valign='top'>0</td>
<td class='normal' valign='top'>509</td>
<td class='normal' valign='top'>6.9961</td>
<td class='normal' valign='top'>289.0393</td>
<td class='normal' valign='top'>147121</td>
<td class='normal' valign='top'>5.3163</td>
</tr>

<tr>
<td class='normal' valign='top'>1</td>
<td class='normal' valign='top'>491</td>
<td class='normal' valign='top'>6.8921</td>
<td class='normal' valign='top'>260.5825</td>
<td class='normal' valign='top'>127946</td>
<td class='normal' valign='top'>5.4847</td>
</tr>
</table>
</body></html>

**Principais Insights**

1. **Impacto na Receita**:
    - Membros do programa tem ticket médio **9.8% menor** (R$260.58 vs R$289.04)
    - Receita total **13% menor** entre membros do programa de fidelização

2. **Problemas Identificados**:
    - Programa pode estar atraindo clientes de menor valor
   - Benefícios não estão convertendo em maior gasto e frequência de compra

**Estratégias Propostas**

**Revisão de Benefícios**:
   - Criar incentivos no programa para aumento do ticket médio
   - Oferecer vantagens progressivas por gasto acumulado
   - Investimento na divulgação dos benefícios da fidelização para aumentar a aquisição de novos membros

**Segmentação**:
   - Avaliar criar níveis de fidelização, assim é possível dividir em subgrupos os perfis dos clientes (baixo, médio e alto ticket)
   - Desenvolver estratégias específicas para cada perfil

**Como bônus do projeto e pensando no programa de fidelidade, desenvolvi duas Procedures uma para cadastrar usuários no Programa de Fidelidade e outra para Descadastrar de forma otimizada! Vocês podem conferir no repositório em [procedure_programa_fidelidade.sql](./https://github.com/dorrigo/comportamento-consumidor-sql/blob/main/procedure_programa_fidelidade.sql)**

## Query_4

### Qual é o nosso perfil de cliente ideal?

Output Query_4.1

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>faixa_etaria</td>
<td bgcolor=silver class='medium'>total_customers</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>18-25</td>
<td class='normal' valign='top'>222</td>
<td class='normal' valign='top'>279.0360</td>
<td class='normal' valign='top'>7.2162</td>
<td class='normal' valign='top'>61946</td>
</tr>

<tr>
<td class='normal' valign='top'>26-35</td>
<td class='normal' valign='top'>308</td>
<td class='normal' valign='top'>278.0162</td>
<td class='normal' valign='top'>6.8442</td>
<td class='normal' valign='top'>85629</td>
</tr>

<tr>
<td class='normal' valign='top'>36-45</td>
<td class='normal' valign='top'>320</td>
<td class='normal' valign='top'>274.9094</td>
<td class='normal' valign='top'>6.9000</td>
<td class='normal' valign='top'>87971</td>
</tr>

<tr>
<td class='normal' valign='top'>46+</td>
<td class='normal' valign='top'>150</td>
<td class='normal' valign='top'>263.4733</td>
<td class='normal' valign='top'>6.8467</td>
<td class='normal' valign='top'>39521</td>
</tr>
</table>
</body></html>

Output Query_4.2

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>gender</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>Female</td>
<td class='normal' valign='top'>452</td>
<td class='normal' valign='top'>282.0863</td>
<td class='normal' valign='top'>6.8850</td>
<td class='normal' valign='top'>127503</td>
</tr>

<tr>
<td class='normal' valign='top'>Male</td>
<td class='normal' valign='top'>449</td>
<td class='normal' valign='top'>267.6392</td>
<td class='normal' valign='top'>6.9421</td>
<td class='normal' valign='top'>120170</td>
</tr>

<tr>
<td class='normal' valign='top'>Genderfluid</td>
<td class='normal' valign='top'>17</td>
<td class='normal' valign='top'>295.2353</td>
<td class='normal' valign='top'>7.2941</td>
<td class='normal' valign='top'>5019</td>
</tr>

<tr>
<td class='normal' valign='top'>Agender</td>
<td class='normal' valign='top'>19</td>
<td class='normal' valign='top'>243.7368</td>
<td class='normal' valign='top'>7.4737</td>
<td class='normal' valign='top'>4631</td>
</tr>

<tr>
<td class='normal' valign='top'>Polygender</td>
<td class='normal' valign='top'>15</td>
<td class='normal' valign='top'>308.0667</td>
<td class='normal' valign='top'>7.6000</td>
<td class='normal' valign='top'>4621</td>
</tr>

<tr>
<td class='normal' valign='top'>Bigender</td>
<td class='normal' valign='top'>20</td>
<td class='normal' valign='top'>258.4500</td>
<td class='normal' valign='top'>7.4000</td>
<td class='normal' valign='top'>5169</td>
</tr>

<tr>
<td class='normal' valign='top'>Genderqueer</td>
<td class='normal' valign='top'>12</td>
<td class='normal' valign='top'>279.4167</td>
<td class='normal' valign='top'>5.1667</td>
<td class='normal' valign='top'>3353</td>
</tr>

<tr>
<td class='normal' valign='top'>Non-binary</td>
<td class='normal' valign='top'>16</td>
<td class='normal' valign='top'>287.5625</td>
<td class='normal' valign='top'>7.8750</td>
<td class='normal' valign='top'>4601</td>
</tr>
</table>
</body></html>


Output Query_4.3

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>education_level</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>Master's</td>
<td class='normal' valign='top'>328</td>
<td class='normal' valign='top'>266.8049</td>
<td class='normal' valign='top'>6.9360</td>
<td class='normal' valign='top'>87512</td>
</tr>

<tr>
<td class='normal' valign='top'>High School</td>
<td class='normal' valign='top'>331</td>
<td class='normal' valign='top'>274.2145</td>
<td class='normal' valign='top'>7.0453</td>
<td class='normal' valign='top'>90765</td>
</tr>

<tr>
<td class='normal' valign='top'>Bachelor's</td>
<td class='normal' valign='top'>341</td>
<td class='normal' valign='top'>283.8416</td>
<td class='normal' valign='top'>6.8563</td>
<td class='normal' valign='top'>96790</td>
</tr>
</table>
</body></html>


Output Query_4.4

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>income_level</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>Middle</td>
<td class='normal' valign='top'>485</td>
<td class='normal' valign='top'>274.5856</td>
<td class='normal' valign='top'>6.8351</td>
<td class='normal' valign='top'>133174</td>
</tr>

<tr>
<td class='normal' valign='top'>High</td>
<td class='normal' valign='top'>515</td>
<td class='normal' valign='top'>275.5204</td>
<td class='normal' valign='top'>7.0485</td>
<td class='normal' valign='top'>141893</td>
</tr>
</table>
</body></html>


Output Query_4.5

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>marital_status</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>Single</td>
<td class='normal' valign='top'>242</td>
<td class='normal' valign='top'>276.5579</td>
<td class='normal' valign='top'>7.1364</td>
<td class='normal' valign='top'>66927</td>
</tr>

<tr>
<td class='normal' valign='top'>Divorced</td>
<td class='normal' valign='top'>245</td>
<td class='normal' valign='top'>274.5265</td>
<td class='normal' valign='top'>6.9551</td>
<td class='normal' valign='top'>67259</td>
</tr>

<tr>
<td class='normal' valign='top'>Married</td>
<td class='normal' valign='top'>253</td>
<td class='normal' valign='top'>280.5652</td>
<td class='normal' valign='top'>6.7628</td>
<td class='normal' valign='top'>70983</td>
</tr>

<tr>
<td class='normal' valign='top'>Widowed</td>
<td class='normal' valign='top'>260</td>
<td class='normal' valign='top'>268.8385</td>
<td class='normal' valign='top'>6.9346</td>
<td class='normal' valign='top'>69898</td>
</tr>
</table>
</body></html>

**A partir dos dados demográficos analisados podemos traçar os nossos perfis de cliente ideal, os critérios vão além do perfil que só trás a maior receita, vou trazer um perfil baseado nas consultas feitas anteriormente:**

- Faixa Etária: entre 26 - 45 anos
- Bacharel 
- Nível de renda: Classe média-alta
  
  - Não inclui Gênero e Estado Civil pela pouca diferença entre os dados de receita, frequência de compra e ticket médio

## Query_5

### Consulta para encontrar as categorias que levam mais tempo de decisão de compra, com o objetivo de identificar quais categorias de produtos podem ser alvos de ações de marketing com intuito de diminuir o tempo de decisão de compra.

Output Query_5

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>purchase_category</td>
<td bgcolor=silver class='medium'>tempo_medio_decisao</td>
<td bgcolor=silver class='medium'>tempo_media_geral</td>
</tr>

<tr>
<td class='normal' valign='top'>Gardening & Outdoors</td>
<td class='normal' valign='top'>8.9545</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Beauty & Personal Care</td>
<td class='normal' valign='top'>8.3824</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Toys & Games</td>
<td class='normal' valign='top'>8.2553</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Office Supplies</td>
<td class='normal' valign='top'>8.2368</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Books</td>
<td class='normal' valign='top'>8.1892</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Jewelry & Accessories</td>
<td class='normal' valign='top'>8.1000</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Travel & Leisure (Flights</td>
<td class='normal' valign='top'>8.0789</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Arts & Crafts</td>
<td class='normal' valign='top'>8.0588</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Animal Feed</td>
<td class='normal' valign='top'>7.8182</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Packages)</td>
<td class='normal' valign='top'>7.7674</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Mobile Accessories</td>
<td class='normal' valign='top'>7.7317</td>
<td class='normal' valign='top'>7.5470</td>
</tr>

<tr>
<td class='normal' valign='top'>Furniture</td>
<td class='normal' valign='top'>7.5854</td>
<td class='normal' valign='top'>7.5470</td>
</tr>
</table>
</body></html>

**Principais Insights**
- Temos pelos menos 8 categorias de produto com uma média de pelo menos 8 dias para tomar a decisão de compra, dentre elas o top 3:
  - Gardening & Outdoors (Jardinagem e Atividades ao Ar Livre)
  - Beauty & Personal Care (Beleza e Cuidado Pessoal)
  - Toys & Games (Brinquedos e Jogos)

**Estratégias Propostas**

**Campanhas de Remarketing**:
   - Campanhas para atingir o público que acessou a categoria e não finalizou compra nos últimos 7 dias
   - Oferecer cupom de desconto para as categorias com tempo de decisão alto a fim de incentivar a compra antecipada

## Query_6

### Clientes sensíveis a descontos tendem a ter maior taxa de retorno ou menor satisfação?

Output Query_6

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>discount_sensitivity</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>taxa_retorno</td>
<td bgcolor=silver class='medium'>satisfacao_cliente</td>
</tr>

<tr>
<td class='normal' valign='top'>Somewhat Sensitive</td>
<td class='normal' valign='top'>319</td>
<td class='normal' valign='top'>0.9624</td>
<td class='normal' valign='top'>5.5141</td>
</tr>

<tr>
<td class='normal' valign='top'>Very Sensitive</td>
<td class='normal' valign='top'>350</td>
<td class='normal' valign='top'>0.9171</td>
<td class='normal' valign='top'>5.4029</td>
</tr>

<tr>
<td class='normal' valign='top'>Not Sensitive</td>
<td class='normal' valign='top'>331</td>
<td class='normal' valign='top'>0.9849</td>
<td class='normal' valign='top'>5.2840</td>
</tr>
</table>
</body></html>

**Principais Insights**

1. **Taxa de Retorno**:
   - Clientes **não sensíveis** têm a **maior taxa de retorno**, são clientes mais fidelizados pois não precisam de desconto para comprar
   - Os clientes mais sensíveis a desconto tem a menor taxa de retorno, são clientes que só querem comprar com desconto

2. **Satisfação**:
   - Clientes **pouco sensíveis** são os mais satisfeitos (5.51)
   - Comportamento curioso: não sensíveis têm menor satisfação (5.28) mas maior retorno

**Estratégias Propostas**

**Para Muito Sensíveis**:
   - Programas de fidelidade (não apenas descontos)

**Para Pouco Sensíveis**:
   - Manter sobre ações de promoção e marketing 

**Para Não Sensíveis**:
   - Investir em experiência, serviço de qualidade e atendimento

## Query_7

### Qual a influência da intenção de compra na frequência de compra, ticket e receita?

Output Query_7

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>purchase_intent</td>
<td bgcolor=silver class='medium'>total_clientes</td>
<td bgcolor=silver class='medium'>frequencia_compra</td>
<td bgcolor=silver class='medium'>ticket_medio</td>
<td bgcolor=silver class='medium'>receita_total</td>
</tr>

<tr>
<td class='normal' valign='top'>Impulsive</td>
<td class='normal' valign='top'>248</td>
<td class='normal' valign='top'>6.9556</td>
<td class='normal' valign='top'>256.8347</td>
<td class='normal' valign='top'>63695</td>
</tr>

<tr>
<td class='normal' valign='top'>Need-based</td>
<td class='normal' valign='top'>256</td>
<td class='normal' valign='top'>6.8945</td>
<td class='normal' valign='top'>280.7773</td>
<td class='normal' valign='top'>71879</td>
</tr>

<tr>
<td class='normal' valign='top'>Wants-based</td>
<td class='normal' valign='top'>249</td>
<td class='normal' valign='top'>6.8715</td>
<td class='normal' valign='top'>292.0361</td>
<td class='normal' valign='top'>72717</td>
</tr>

<tr>
<td class='normal' valign='top'>Planned</td>
<td class='normal' valign='top'>247</td>
<td class='normal' valign='top'>7.0607</td>
<td class='normal' valign='top'>270.3482</td>
<td class='normal' valign='top'>66776</td>
</tr>
</table>
</body></html>

**Principais Insights**

1. **Ticket Médio**:
   - Compras **por desejo** têm maior valor (+13.7% vs impulsivas)
   - As compras impulsivas tem menor ocorrência e ticket médio

2. **Frequência**:
   - Compras **planejadas** são mais frequentes
   - Intenções emocionais (desejo/impulso) têm menor recorrência

3. **Receita Total**:
   - **Desejo** lidera em receita, seguido por **necessidade**
   - Compras impulsivas geram menor receita
  
**Estratégias Propostas**

**Anúncios com Comunicação Direcionada**:
   - Ajustar a comunicação das campanhas de mídia paga para incentivar o aumento as compras planejadas e por impulso
   - Campanhas que focam na dor do cliente para gerar mais intenção de necessidade de compra

## Query_8

### Clientes que pesquisam mais antes de comprar ficam mais satisfeitos?

Output Query_8

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<table border=1>
<tr>
<td bgcolor=silver class='medium'>tempo_gasto_em_pesquisa</td>
<td bgcolor=silver class='medium'>media_satisfacao_consumidor</td>
</tr>

<tr>
<td class='normal' valign='top'>0</td>
<td class='normal' valign='top'>5.5139</td>
</tr>

<tr>
<td class='normal' valign='top'>1</td>
<td class='normal' valign='top'>5.1690</td>
</tr>

<tr>
<td class='normal' valign='top'>2</td>
<td class='normal' valign='top'>5.5373</td>
</tr>
</table>
</body></html>

**Principais Insights**

1. **Compradores Rápidos (<1h)**:
   - Satisfação elevada (5.51)
   - Possivelmente compram produtos conhecidos/marcas de confiança

2. **Pesquisa Intermediária (1-2h)**:
   - **Menor satisfação** (5.17)
   - Produto pode não estar atendendo a expectativa do cliente

3. **Pesquisadores Dedicados (>2h)**:
   - **Máxima satisfação** (5.54)
   - Tomada de decisão mais assertiva

**Estratégias Propostas**

**Para Compradores de 1-2h**:
   - Adicionar seção de **Produtos Semelhantes**
   - Destacar as avaliações de quem já comprou o produto para ajudar na decisão de compra

[Home](./)






