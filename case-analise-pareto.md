# Análise de Pareto Aplicada a Dados de E-commerce

## Desafio
A empresa modificou nomes e URLs dos produtos de uma categoria inteira do e-commerce para melhorar o posicionamento orgânico no Google. Porém, a equipe não previu o impacto nos canais de aquisição:

- **Risco para canais**:  
  - Mídia paga  
  - Tráfego orgânico  
- **Perda de receita direta**: Usuários digitando URLs antigas  

## Análise de Dados
**Período comparativo**: 30 dias antes vs. após a mudança  

1. **Extração e tratamento**:  
   - Dados dos canais de aquisição via Google Analytics 4 (GA4)  
   - Tratamento e Visualização dos dados no Power BI  

**Resultados da análise**:  
- Queda geral de **24% na receita**  
- **Canais mais afetados**:  

| Canal       | Queda de Receita | Causa Principal                                                                 |
|-------------|------------------|---------------------------------------------------------------------------------|
| **Direct**  | 50%              | URLs antigas retornando erro 404                                                |
| **Orgânico**| 33%              | Novas URLs sem posição competitiva após re-indexação                            |
| **Pago**    | 22%              | Links quebrados e campanhas em fase de aprendizado novamente                    |

## Solução (Baseada em Dados)  

### Passo 1: Priorização com Princípio de Pareto  
- Foco nos **20% dos produtos que geravam 80% da receita**  
- Análise do impacto específico das modificações nesses produtos  

### Passo 2: Ações Direcionadas  
- **Mídia Paga**:  
  - Redirecionamento imediato de campanhas  
  - Catálogo personalizado com produtos prioritários  
- **Direct**:  
  - E-mail marketing com novos links para base de clientes  

## Resultados  
| Canal       | Situação Inicial | Após 60 Dias | Crescimento |  
|-------------|------------------|--------------|-------------|  
| **Direct**  | -50%             | +8%          | **+58%**    |  
| **Orgânico**| -33%             | +15%         | **+48%**    |  
| **Mídia Paga**| -22%           | +20%         | **+42%**    |  

## Aprendizados  
1. **Definição prévia de KPIs** é essencial para decisões ágeis baseadas em dados  
2. **Priorização da Curva A** (20% dos produtos) otimizou a estratégia  
3. **Segmentação de problemas complexos** acelera a solução e aumenta eficácia  

