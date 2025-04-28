---
layout: default
---

# Análise de Determinantes de Saúde Mental  
**Base de Dados**: Anxiety and Depression - Mental Health Factors  

## Objetivo  
Identificar os fatores que mais impactam casos graves de depressão e ansiedade em uma amostra específica com 1.200 indivíduos.  

## Ferramentas Utilizadas  
- Power BI  
- Power Query  

## Principais Etapas  
Utilizei o método ETL para tratamento dos dados.  

### 1. Extração (Extract)  
**Fonte de dados**: Base obtida do Kaggle (em inglês).  

**Ações realizadas**:  
- Importação do dataset original  
- Verificação inicial da estrutura, qualidade e tipo dos dados  

### 2. Transformação (Transform)  
**Padronização de dados**:  
- Tradução de colunas (inglês → português) usando Replace Values  
- Ajuste de tipos de dados  

### 3. Carregamento (Load)  
**Modelagem no Power BI**:  

**Criação de novas colunas**:  
- Classificação de faixas (Ansiedade, Depressão, Estresse) e Faixa Etária com SWITCH  

**Criação de Medidas Calculadas**:  
- Utilizei bastante da função `CALCULATE` em conjunto com outras como `DIVIDE`, `COUNT`, `AVERAGE`, `FILTER` entre outras para as minhas medidas  

---

## Visualização e Insights  
**Dashboard**:  
- Gráficos de Pizza: Distribuição de faixas (Ansiedade/Depressão/Estresse)  
- Gráficos de Barras: Praticantes de Terapia  
- Cartões KPI: Taxas gerais e dos subgrupos  

## Resultados Obtidos  

### 1. Fatores Não Determinantes (Contra Intuitivos)  
**Privação de sono (<7h)**:  
- Depressão grave: 24% (vs. 24% da média geral)  
- Ansiedade grave: 27% (vs. 27% da média)  
- **Conclusão**: Não foi um agravante significativo nesta amostra  

**Sedentarismo (<2h/semana de exercício)**:  
- Taxas alinhadas com a média geral  
- **Destaque**: Diferente das recomendações médicas, o impacto foi mínimo no grupo estudado  

### 2. Fatores Críticos  

| Fator (Depressão Grave)       | Taxa de Depressão Grave | Diferença Relativa |
|-------------------------------|-------------------------|--------------------|
| Baixo suporte social (score ≤2)| 27% (+3 p.p.)           | +12,5% vs. média   |
| Histórico familiar             | 28% (+4 p.p.)           | +16,6% vs. média   |

| Fator (Ansiedade Grave)        | Taxa                   | Diferença Relativa |
|--------------------------------|------------------------|--------------------|
| Uso regular de medicamentos    | 30% (+3 p.p.)          | +11,1% vs. média   |

### 3. Terapia: O Fator Subutilizado  
- Em média 80% dos casos graves não faziam terapia  
- **Entre os diagnosticados**:  
  - Depressão grave: apenas 22% em terapia  
  - Ansiedade grave: 21%  
  - Estresse grave: 21%  

---

## Conclusões e Recomendações  
1. **Priorizar intervenções sociais**: Programas de apoio comunitário reduzem até 12,5% dos casos graves  
2. **Rastreamento familiar**: Indivíduos com histórico têm risco 16,6% maior – ideal para prevenção  
3. **Combater a resistência à terapia**: Aderência abaixo de 25% em casos graves indica necessidade de campanhas de conscientização  

## Observação Importante sobre os Resultados  
Este estudo analisou uma amostra específica de 1.200 indivíduos, e seus resultados diferem de pesquisas amplas sobre o impacto do sono e exercícios na saúde mental. Os dados mostram que, neste grupo em particular, fatores como suporte social e histórico familiar tiveram maior influência nos casos graves de depressão e ansiedade do que horas de sono ou atividade física.  

**Isso não invalida descobertas consolidadas pela medicina**, mas reforça que análises de dados devem considerar o contexto da amostra – políticas públicas e intervenções precisam ser baseadas em evidências locais, não apenas em generalizações.  

---

## Aprendizados  
Neste projeto, pude aplicar na prática o método ETL, desde a extração e transformação dos dados no Power Query até o carregamento eficiente no Power BI. Através da linguagem DAX, desenvolvi habilidades essenciais na criação de colunas calculadas e medidas personalizadas, com destaque para o domínio da função `CALCULATE` - compreendi sua versatilidade para análises contextuais avançadas e como ela amplia significativamente as possibilidades de investigação dos dados, permitindo comparações segmentadas e filtros dinâmicos que enriqueceram minha análise de indicadores de saúde mental.

[Link Power BI](https://app.powerbi.com/view?r=eyJrIjoiNzA3NWY1OTgtNDQ1MC00ZGNlLTlkM2QtNzgwMDllZGQwNGZmIiwidCI6Ijc0NDY5NmNmLTYxMzYtNDYzOS04MTExLWY3NTUwN2I5ZmY2ZCJ9)


<iframe title="mental_health_study" width="600" height="636" src="https://app.powerbi.com/view?r=eyJrIjoiNzA3NWY1OTgtNDQ1MC00ZGNlLTlkM2QtNzgwMDllZGQwNGZmIiwidCI6Ijc0NDY5NmNmLTYxMzYtNDYzOS04MTExLWY3NTUwN2I5ZmY2ZCJ9" frameborder="0" allowFullScreen="true"></iframe>


[Home](./)
