# Projeto: People Analytics no Databricks

---

## Problema/Objetivo

A empresa enfrenta desafios relacionados à rotatividade de funcionários e necessita compreender os principais fatores que influenciam a retenção de talentos. Este projeto tem como objetivos:

- **Identificar a taxa de turnover** geral e por departamento
- **Analisar o clima organizacional** através de métricas de satisfação
- **Avaliar a equidade salarial** entre diferentes grupos demográficos
- **Investigar oportunidades de desenvolvimento** e progressão de carreira
- **Detectar funcionários em risco de saída** para ações preventivas
- **Fornecer insights acionáveis** para reduzir turnover e melhorar retenção

---

## Ferramentas Utilizadas

- **Databricks SQL**: Plataforma de análise de dados
- **SQL**: Linguagem para consultas e transformações
- **Dataset**: people_analytics.employee e people_analytics.performance
- **Técnicas aplicadas**:
  - Views para reutilização de código
  - CTEs (Common Table Expressions) para queries complexas
  - Window Functions (DENSE_RANK, AVG OVER)
  - Agregações e GROUP BY
  - JOINs entre tabelas relacionadas
  - Análises de correlação e segmentação

---

## Resultados Obtidos

### 1. Panorama de Turnover

#### 1.1 Taxa de Turnover Geral

```sql
CREATE VIEW funcionarios AS (
  SELECT
    Department,
    COUNT(CASE WHEN Attrition = 'Yes' THEN 1 ELSE NULL END) as funcionario_inativo,
    COUNT(CASE WHEN Attrition = 'No' THEN 1 ELSE NULL END) as funcionario_ativo,
    COUNT(DISTINCT EmployeeID) as total_funcionarios,
    CONCAT(ROUND((funcionario_ativo/total_funcionarios) * 100, 2), "%") as pct_funcionario_ativo,
    CONCAT(ROUND((funcionario_inativo/total_funcionarios) *100, 2), "%") as pct_funcionario_inativo
  FROM people_analytics.employee
  GROUP BY Department
);

SELECT
  total_funcionarios,
  funcionario_ativo,
  funcionario_inativo,
  pct_funcionario_ativo,
  pct_funcionario_inativo
FROM funcionarios
```

**Resultados:**

| Total Funcionários | Funcionários Ativos | Funcionários Inativos | % Ativos | % Inativos |
|-------------------|--------------------|-----------------------|----------|------------|
| 446 | 354 | 92 | 79.37% | 20.63% |
| 63 | 51 | 12 | 80.95% | 19.05% |
| 961 | 828 | 133 | 86.16% | 13.84% |

**Insights:**
- Taxa média de turnover entre 13-21% dependendo do departamento
- Aproximadamente 1 em cada 5-7 funcionários deixou a empresa

#### 1.2 Turnover por Departamento

```sql
SELECT
  Department,
  funcionario_ativo,
  funcionario_inativo,
  pct_funcionario_ativo,
  pct_funcionario_inativo
FROM funcionarios
ORDER BY pct_funcionario_inativo DESC;
```

**Resultados:**

| Departamento | Funcionários Ativos | Funcionários Inativos | % Ativos | % Inativos |
|--------------|--------------------|-----------------------|----------|------------|
| Sales | 354 | 92 | 79.37% | 20.63% |
| Human Resources | 51 | 12 | 80.95% | 19.05% |
| Technology | 828 | 133 | 86.16% | 13.84% |

**Insights:**
- **Sales** tem a maior taxa de turnover (20.63%)
- **Technology** apresenta a melhor retenção (86.16%)
- Sales é o departamento prioritário para ações de retenção

---

### 2. Clima Organizacional

#### 2.1 Índice de Satisfação Geral

```sql
SELECT
  employee.Department as Departamento,
  ROUND(AVG(performance.EnvironmentSatisfaction), 2) as satisfacao_ambiente,
  ROUND(AVG(performance.JobSatisfaction), 2) as satisfacao_trabalho,
  ROUND(AVG(performance.RelationshipSatisfaction), 2) as satisfacao_relacionamento,
  ROUND((AVG(performance.EnvironmentSatisfaction) + 
         AVG(performance.JobSatisfaction) + 
         AVG(performance.RelationshipSatisfaction)) / 3, 2) as indice_satisfacao_geral
FROM people_analytics.employee employee
JOIN people_analytics.performance performance
  USING (EmployeeID)
WHERE employee.Attrition = 'No'
GROUP BY employee.Department
ORDER BY indice_satisfacao_geral DESC
```

**Resultados:**

| Departamento | Satisfação Ambiente | Satisfação Trabalho | Satisfação Relacionamento | Índice Geral |
|--------------|---------------------|---------------------|---------------------------|--------------|
| Sales | 3.90 | 3.40 | 3.41 | 3.57 |
| Technology | 3.86 | 3.42 | 3.43 | 3.57 |
| Human Resources | 3.87 | 3.45 | 3.30 | 3.54 |

**Insights:**
- Satisfação moderada em todos os departamentos (3.54-3.57 em escala de 5)
- HR tem menor satisfação com relacionamentos (3.30)
- Sales tem melhor satisfação com ambiente, mas não se traduz em menor turnover

#### 2.2 Funcionários em Alto Risco de Saída

```sql
SELECT
  Department as Departamento,
  COUNT(*) AS funcionario_risco_de_saida,
  DENSE_RANK() OVER (ORDER BY COUNT(*) DESC) AS rank_departamento
FROM people_analytics.employee e
JOIN people_analytics.performance p
  USING (EmployeeID)
WHERE e.Attrition = 'No'
  AND (
    p.JobSatisfaction <= 2
    AND p.ManagerRating <= 2
    AND p.WorkLifeBalance <= 2
  )
GROUP BY Department
ORDER BY funcionario_risco_de_saida DESC
```

**Resultados:**

| Departamento | Funcionários em Risco | Ranking |
|--------------|----------------------|---------|
| Technology | 32 | 1 |
| Sales | 18 | 2 |
| Human Resources | 1 | 3 |

**📌 Insights:**
- **51 funcionários ativos** em risco crítico de saída
- Technology tem 32 funcionários nesta situação (ação urgente necessária)
- Critério: baixa satisfação + baixa performance + desequilíbrio de vida

#### 2.3 Work-Life Balance por Overtime

```sql
SELECT 
    employee.OverTime,
    employee.Department,
    ROUND(AVG(performance.WorkLifeBalance),2) AS AvgWorkLifeBalance,
    COUNT(*) AS EmployeeCount
FROM people_analytics.employee employee
JOIN people_analytics.performance performance USING (EmployeeID)
GROUP BY 1,2
ORDER BY 1,2
```

**Resultados:**

| Overtime | Departamento | Work-Life Balance Médio | Total Funcionários |
|----------|--------------|------------------------|-------------------|
| No | Human Resources | 3.41 | 211 |
| No | Sales | 3.42 | 1,407 |
| No | Technology | 3.42 | 2,854 |
| Yes | Human Resources | 3.32 | 92 |
| Yes | Sales | 3.40 | 742 |
| Yes | Technology | 3.41 | 1,403 |

**Insights:**
- 2,237 funcionários (43%) fazem horas extras regularmente
- Work-life balance é consistentemente menor para quem faz overtime
- HR com overtime tem o menor índice (3.32)

---

### 3. Análise de Compensação

#### 3.1 Equidade Salarial por Gênero

```sql
WITH salarios_por_genero AS (
    SELECT 
        Gender,
        COUNT(*) as total_funcionarios,
        ROUND(AVG(Salary), 2) as salario_medio_anual,
        ROUND(MIN(Salary), 2) as salario_minimo_anual,
        ROUND(MAX(Salary), 2) as salario_maximo_anual
    FROM people_analytics.employee
    WHERE Attrition = 'No'
    GROUP BY Gender
)

SELECT 
    Gender as Genero,
    total_funcionarios,
    salario_medio_anual,
    salario_minimo_anual,
    salario_maximo_anual,
    ROUND((salario_medio_anual - MAX(salario_medio_anual) OVER()) / MAX(salario_medio_anual) OVER() * 100, 2) as gap_percentual
FROM salarios_por_genero
ORDER BY gap_percentual;
```

**Resultados:**

| Gênero | Total Funcionários | Salário Médio Anual | Salário Mínimo | Salário Máximo | Gap Percentual |
|--------|-------------------|---------------------|----------------|----------------|----------------|
| Non-Binary | 105 | $114,827.08 | $21,649 | $542,695 | -10.35% |
| Male | 537 | $116,770.36 | $20,418 | $547,204 | -8.83% |
| Female | 571 | $121,236.06 | $20,802 | $546,549 | -5.35% |
| Prefer Not To Say | 20 | $128,083.35 | $21,202 | $365,504 | 0% |

**Insights:**
- **Equidade positiva**: mulheres ganham 3.8% a mais que homens
- Funcionários Non-Binary têm gap de -10.35% (requer investigação)
- Ampla faixa salarial ($20k-$547k) indica diversos níveis hierárquicos

#### 3.2 Impacto Salarial do Overtime

```sql
SELECT
  Department AS Departamento,
  COUNT(*) AS funcionario_hora_extra,
  ROUND(AVG(CASE WHEN OverTime = 'Yes' THEN Salary END), 2) AS media_salarial_funcionario_horas_ex,
  ROUND(AVG(CASE WHEN OverTime = 'No' THEN Salary END), 2) AS media_salarial_sem_extra,
  ROUND(AVG(CASE WHEN OverTime = 'Yes' THEN Salary END) - AVG(CASE WHEN OverTime = 'No' THEN Salary END), 2) AS diferenca_media
FROM people_analytics.employee
GROUP BY Department
ORDER BY diferenca_media DESC
```

**Resultados:**

| Departamento | Func. com Overtime | Salário Médio c/ Overtime | Salário Médio s/ Overtime | Diferença |
|--------------|-------------------|---------------------------|---------------------------|-----------|
| Human Resources | 63 | $129,414.71 | $116,108.15 | $13,306.55 |
| Sales | 446 | $122,709.54 | $117,671.80 | $5,037.74 |
| Technology | 961 | $110,382.39 | $109,369.49 | $1,012.91 |

**Insights:**
- HR: +$13k para quem faz overtime (+11.5%)
- Sales: +$5k para quem faz overtime (+4.3%)
- **Technology: apenas +$1k (+0.9%)** - compensação inadequada
- Isso pode explicar o alto número de funcionários em risco em TI

---

### 4. Desenvolvimento e Carreira

#### 4.1 Taxa de Utilização de Treinamentos

```sql
SELECT
  employee.Department,
  ROUND(AVG(performance.TrainingOpportunitiesTaken / performance.TrainingOpportunitiesWithinYear * 100), 2) AS taxa_media_uso_treino
FROM people_analytics.employee employee
JOIN people_analytics.performance performance
  USING (EmployeeID)
GROUP BY employee.Department
ORDER BY taxa_media_uso_treino DESC
```

**Resultados:**

| Departamento | Taxa Média de Utilização (%) |
|--------------|------------------------------|
| Technology | 61.69% |
| Sales | 61.66% |
| Human Resources | 60.89% |

**Insights:**
- Aproximadamente 60% das oportunidades de treinamento são aproveitadas
- **40% das oportunidades não são utilizadas** (investigar barreiras)
- Taxas similares entre departamentos

#### 4.2 Análise de Estagnação Profissional

```sql
SELECT 
    Department as Departamento,
    COUNT(CASE WHEN YearsSinceLastPromotion >= 5 THEN 1 END) AS Alta_estagnacao,
    COUNT(CASE WHEN YearsSinceLastPromotion BETWEEN 3 AND 4 THEN 1 END) AS Media_estagnacao,
    COUNT(CASE WHEN YearsSinceLastPromotion < 3 THEN 1 END) AS Baixa_estagncacao,
    ROUND(AVG(YearsSinceLastPromotion),2) AS Media_anual_ultima_promocao
FROM people_analytics.employee
WHERE Attrition = 'No'
GROUP BY Department
```

**Resultados:**

| Departamento | Alta Estagnação (≥5 anos) | Média Estagnação (3-4 anos) | Baixa Estagnação (<3 anos) | Média Anos s/ Promoção |
|--------------|---------------------------|----------------------------|---------------------------|------------------------|
| Sales | 125 | 86 | 143 | 3.71 |
| Human Resources | 20 | 10 | 21 | 3.75 |
| Technology | 325 | 186 | 317 | 3.88 |

**Insights:**
- **470 funcionários** (38%) estão há 5+ anos sem promoção
- Technology tem 325 pessoas em alta estagnação
- Média de 3.7-3.9 anos sem promoção é elevada
- Alto risco de perda de talentos experientes

---

### 5. Gestão de Performance

#### 5.1 Performance Gap (Alinhamento Autoavaliação vs Gestor)

```sql
SELECT
employee.EmployeeID as id_funcionario,
employee.Department as departamento,
performance.SelfRating as auto_avaliacao,
performance.ManagerRating as avaliacao_gerente,
(performance.ManagerRating - performance.SelfRating) as diferenca_avaliacao
FROM people_analytics.employee employee
JOIN people_analytics.performance performance
USING (EmployeeID)
ORDER BY  diferenca_avaliacao DESC
LIMIT 10;
```

**Resultados (Top 10):**

| ID Funcionário | Departamento | Autoavaliação | Avaliação Gestor | Diferença |
|---------------|--------------|---------------|------------------|-----------|
| 5634-9D10 | Technology | 3 | 4 | +1 |
| DA8E-9496 | Technology | 5 | 5 | 0 |
| 528C-3E0D | Technology | 5 | 5 | 0 |
| B013-7D0C | Technology | 3 | 3 | 0 |
| D077-169C | Sales | 5 | 5 | 0 |
| F93E-BDEF | Technology | 4 | 4 | 0 |
| DEC5-9319 | Technology | 4 | 4 | 0 |
| 9C57-828C | Technology | 3 | 3 | 0 |
| 79F7-78EC | Sales | 4 | 4 | 0 |
| 88B8-EB84 | Technology | 5 | 5 | 0 |

**Insights:**
- Maioria dos funcionários tem boa calibração (diferença = 0)
- Quando há gap, geralmente o gestor avalia melhor (+1)
- Bom alinhamento entre expectativas de gestores e funcionários

---

## Aprendizados

### Insights Principais

**1. Sales é o departamento crítico**
- Maior taxa de turnover (20.63%)
- 18 funcionários em alto risco de saída
- Satisfação moderada não está impedindo a saída
- **Ação necessária**: Programa de retenção focado e urgente

**2. Estagnação é um problema generalizado**
- 470 funcionários (38%) sem promoção há 5+ anos
- Technology concentra 325 desses casos
- Tempo médio sem promoção é alto (3.7-3.9 anos)
- **Aprendizado**: Estrutura de carreira precisa ser revista

**3. Overtime em Technology não é valorizado**
- Diferença salarial de apenas $1k entre quem faz e não faz overtime
- 43% da empresa faz horas extras regularmente
- Isso contribui para os 32 funcionários em risco em TI
- **Aprendizado**: Compensação inadequada gera insatisfação

**4. Equidade de gênero está bem implementada**
- Mulheres ganham 3.8% a mais que homens
- Porém, funcionários Non-Binary têm gap de -10.35%
- **Aprendizado**: Boas práticas existem, mas precisam ser expandidas

**5. Oportunidades de desenvolvimento são subutilizadas**
- 40% dos treinamentos disponíveis não são aproveitados
- Taxa similar em todos os departamentos (~60% de uso)
- **Aprendizado**: Investigar barreiras (tempo, relevância, comunicação)

**6. Performance está alinhada**
- Gestores e funcionários têm expectativas calibradas
- Poucas discrepâncias nas avaliações
- **Aprendizado**: Processo de avaliação está funcionando bem

---

[Home](./)

