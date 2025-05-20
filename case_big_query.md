#Por que o BigQuery é mais completo para Análise de Dados do GA4 (Mesmo em Projetos de Exemplo)#

Utilizando o dataset público ga4_obfuscated_sample_ecommerce, explorei funcionalidades do BigQuery que superam radicalmente as limitações da integração nativa do GA4. Veja os principais insights:

## 1. Dados Completos sem Amostragem (Até em Projetos de Demonstração) ##
Exemplo Prático: Comparação de Contagens

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
Vantagem: Dados de produtos (armazenados como arrays como no caso dos itens) são acessados sem JOINs complexos.

## 4. Criação de Métricas Personalizadas ##

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






















