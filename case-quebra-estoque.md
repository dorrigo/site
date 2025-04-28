# Case: Solução Baseada em Dados para Quebra de Estoque em E-commerce

## Desafio
O cliente enfrentava quedas inesperadas de receita em semanas específicas, sem padrão aparente, impactando negativamente a lucratividade mensal e o desempenho das campanhas de produtos estratégicos. Era crítico identificar a raiz do problema para corrigi-lo rapidamente. Era crítico identificar a raiz do problema para corrigi-lo rapidamente.

## Análise de Dados
Utilizando o Google Analytics 4 (GA4), analisei:

1. **Métricas do funil de compra**:
   - Visualizações de Produto
   - Adições ao Carrinho
   - Conversões

2. **Receita por produto** e desempenho por canal:
   - Google Ads
   - Meta Ads

## Descoberta
- Alguns produtos mantinham alta visualização, mas a taxa de adição ao carrinho caía abruptamente
- Ao inspecionar as páginas, identifiquei que os produtos estavam com estoque esgotado - e a reposição levava dias, ssa falha não era comunicada prontamente, gerando perda de receita.

## Solução (Baseada em Dados)
Para criar um sistema de alerta rápido, implementei:

### 1. Rastreamento de Quebra de Estoque via Google Tag Manager
- **Tag de evento** acionada pelo elemento CSS "Avise-me quando disponível"
- **Trigger**: "Visibilidade do Elemento"
- **Dados registrados no GA4**:
  - Nome do produto
  - Valor do item
  - Número de ocorrências

### 2. Relatório Automatizado no Looker Studio

Dashboard com:
- Produtos sem estoque
- Volume de alertas
- Impacto estimado na receita (baseado no preço e demanda)

Automação: Relatório enviado toda segunda-feira para a equipe de logística

## Resultados
- **Redução de 60%** nas ocorrências de quebra de estoque em 3 meses
- **Minimização de perdas**: Campanhas de mídia paga com anúncios de catálogo não sofriam mais com pausas de veiculação
- **Processo proativo**: A equipe passou a priorizar reposições com base em dados, não apenas em alertas de vendas

## Aprendizados
1. Saber identificar, rastrear, utilizar e mensurar **dados comportamentais do usuário** são tão importantes quanto métricas de vendas
2. Construir **dashboards acessíveis** para dar suporte eficaz às equipes responsáveis
