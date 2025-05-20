# Por que o BigQuery é mais completo para Análise de Dados do GA4 (Mesmo em Projetos de Exemplo) #

Utilizando o dataset público **ga4_obfuscated_sample_ecommerce**, explorei funcionalidades do BigQuery que superam as limitações da integração nativa do GA4 no Looker Studio. Veja os principais insights:

## 1. Dados Completos sem Amostragem (Até em Projetos de Demonstração) ##
Exemplo: Comparação de Contagens

```sql
SELECT 
  COUNT(DISTINCT user_pseudo_id) AS usuarios_unicos_total
FROM 
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`

-- Resultado: 270.154 usuários (dados brutos)
```
- Problema no GA4: Relatórios complexos sofrem amostragem de dados (especialmente em contas gratuitas)

## 2. Histórico de Dados Ilimitado ##

- Limitação GA4: 14 meses de retenção padrão

- Vantagem BigQuery: Armazene dados históricos indefinidamente com custo otimizado

## 3. Análise de Dados Aninhados com UNNEST ##

```sql
SELECT 
  item.item_name,
  ecommerce.total_item_quantity,
  item.price,
  ecommerce.total_item_quantity * item.price as receita_total
FROM 
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`,
  UNNEST(items) AS item
WHERE 
  item.item_name IS NOT NULL AND event_name = 'purchase'
ORDER BY receita_total desc
LIMIT 10;
```

Vantagem Big Query: Dados de produtos (armazenados como arrays como no caso dos itens) são acessados sem JOINs complexos.

## 4. Criação de Métricas Personalizadas ##
Exemplo: Produtos Frequentemente Comprados Juntos

```sql
WITH compras AS (
  SELECT 
  user_pseudo_id, 
  ARRAY_AGG(item.item_name ORDER BY item.item_name) AS produtos
  FROM `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`, 
  UNNEST(items) AS item
  WHERE 
  event_name = 'purchase'
  GROUP BY 
  user_pseudo_id
)

SELECT 
produtos[ORDINAL(1)] AS produto_1, 
produtos[ORDINAL(2)] AS produto_2, 
COUNT(*) AS vezes_comprados_juntos
FROM compras
WHERE ARRAY_LENGTH(produtos) > 1
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 10;
```

Vantagem Big Query: Mais liberdade para trabalhar os dados, com a integração direta com o GA4 as análises e possibilidades ficam limitadas como na integração nativa do GA4 no Looker Studio.

## 5. Processamento Antecipado para Carregamento mais Rápido ##

Pré-agrego dados no BigQuery, crio as querys e salvo como tabelas diretamente na ferramenta, depois é só criar a fonte de dados no Looker e conectar no dashboard:

```sql
-- Query Funil de Compra

SELECT
  COUNT(DISTINCT CASE WHEN event_name = 'view_item' THEN user_pseudo_id END) AS view_item,
  COUNT(DISTINCT CASE WHEN event_name = 'add_to_cart' THEN user_pseudo_id END) AS add_to_cart,
  COUNT(DISTINCT CASE WHEN event_name = 'begin_checkout' THEN user_pseudo_id END) AS begin_checkout,
  COUNT(DISTINCT CASE WHEN event_name = 'add_payment_info' THEN user_pseudo_id END) AS add_payment_info,
  COUNT(DISTINCT CASE WHEN event_name = 'purchase' THEN user_pseudo_id END) AS purchase
FROM 
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name IN ('view_item', 'add_to_cart', 'begin_checkout', 'add_payment_info', 'purchase')
```
```sql
-- Query Lucro Líquido vs Taxa

WITH net_revenue_data AS (
  SELECT
    item.item_name,
    item.price,
    ecommerce.tax_value,
    item.quantity,
    item.price - ecommerce.tax_value as net_revenue
  FROM 
    `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`,
    UNNEST(items) AS item
  WHERE 
    item.item_name IS NOT NULL 
    AND event_name = 'purchase'
)

SELECT 
  item_name,
  quantity,
  price,
  tax_value,
  net_revenue
FROM 
  net_revenue_data
ORDER BY 
  net_revenue DESC
LIMIT 50
```

Vantagem Big Query: Dashboards carregam mais rápido do que consultas diretas ao GA4, o dashboard fica mais leve!

## 6. Combinação com Dados Externos

- É possível adicionar outros bancos de dados no Big Query e relacionar com seus dados do GA4 através dos JOINs, então podemos relacionar tabelas do GA4 com CRM, Resultados de Campanhas, ERP entre outros bancos.

## 7. Uso de Machine Learning com SQL direto no Big Query ##

O BigQuery ML é uma funcionalidade incrível que permite criar e executar modelos de machine learning diretamente usando SQL. É possível utilizar modelos como Regressão Linear, Clustering, Random Forest, Deep Learning entre outros.

# Comparação Rápida: Integração Nativa GA4 vs. BigQuery

| **Recurso**               | **Integração Nativa GA4**       | **BigQuery**                     |
|---------------------------|--------------------------------|----------------------------------|
| **Amostragem de dados**    | Sim (em relatórios complexos)  | Não                              |
| **Personalização de métricas** | Limitada                     | Ilimitada                        |
| **Combinação com outras fontes** | Não                        | Sim                              |
| **Machine Learning**       | Não                           | Sim (BigQuery ML)                |
| **Custo**                 | Grátis (com limitações)       | Pago por consumo                    |


## Quando Usar a Integração Nativa? ##

A conexão direta GA4-Looker Studio ainda é útil para:

- Dashboards simples e rápidos
- Quando não se precisa de dados históricos profundos
- Para usuários sem conhecimentos de SQL


Ao final deste projeto realizei a integração com o Big Query no Looker Studio e criei a visualização dos dados atráves do Dashboard abaixo:

### Dashboard Looker Studio feito com a Integração Big Query ###

<iframe width="800" height="591" src="https://lookerstudio.google.com/embed/reporting/483c125f-1afd-48a4-8828-13bb487be03c/page/Hi3KF" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>




[Home](/.)











