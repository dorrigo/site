# Dashboard Meta Dota 2: Integração API + Python + Power BI #

### Objetivo
Como jogador de Dota 2 há mais de 10 anos, sempre quis entender melhor as mudanças no meta do jogo de forma visual e atualizada. Meu desafio foi criar um sistema automatizado que transformasse dados brutos da API em insights acionáveis sobre heróis, win rates e influência do mapa.

### Ferramentas Utilizadas
- **Fonte de Dados:** API OpenDota 
- **ETL:** Python (Requests para extração + Pandas para tratamento)
- **Visualização:** Power BI (dashboard interativo)

### Principais Etapas
1. **Integração com API:**
   - Extração dos dados de heróis (hero, pick rate, win rate, ban rate entre outros)
   - Tratamento de JSON para DataFrame estruturado

2. **Transformação dos Dados:**
   - Estruturação e tratamento dos dados recebidos pela API com Python utilizando Pandas
   - Criação dos Dataframes com os dados já tratados

3. **Dashboard no Power BI:**
   - Visão geral do meta atual (gráficos e tabelas)

### Resultados Obtidos
Dashboard atualizado automaticamente via Python
- Heróis mais pickados e banidos
- Heróis com  maior Win Rate
- Influência do lado do mapa na porcentagem de vitória (Radiant vs Dire)
  

### Aprendizados
- **API Design:** Documentação clara é crucial para eficiência e possibilidade de desenvolver o projeto
- **Automação:** Agendamento de scripts Python (+confiável que manual)  
- **Data Storytelling:** Visualizações precisam ser intuitivas para gamers

Para acessar o código utilizado no [Github](https://github.com/dorrigo/Projeto_API_OpenDota/blob/main/script_opendota2.py)

[Link Dashboard](https://app.powerbi.com/view?r=eyJrIjoiYjIwNDdhOWYtMWI5My00YjNjLWI3ZDUtYWEzOTcwNjFlNTU5IiwidCI6Ijc0NDY5NmNmLTYxMzYtNDYzOS04MTExLWY3NTUwN2I5ZmY2ZCJ9)
<iframe title="dota_meta" width="800" height="486" src="https://app.powerbi.com/view?r=eyJrIjoiYjIwNDdhOWYtMWI5My00YjNjLWI3ZDUtYWEzOTcwNjFlNTU5IiwidCI6Ijc0NDY5NmNmLTYxMzYtNDYzOS04MTExLWY3NTUwN2I5ZmY2ZCJ9" frameborder="0" allowFullScreen="true"></iframe>
