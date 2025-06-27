# Projeto de Pipeline de Dados: Da Ingestão à Análise de Vendas

## 1. Introdução
### Problema
Dados de vendas desorganizados em múltiplas fontes, sem padronização ou qualidade garantida, dificultando a análise estratégica.

### Objetivo
Construir um pipeline completo que transforme dados brutos em insights acionáveis, seguindo as melhores práticas de engenharia de dados.

## 2. Ferramentas Utilizadas

| Camada       | Ferramentas               | Função Principal                     |
|--------------|---------------------------|---------------------------------------|
| Ingestão     | Python (Faker, Psycopg2)  | Gerar e carregar dados sintéticos     |
| Armazenamento| PostgreSQL                | Banco de dados relacional             |
| Transformação| dbt (Data Build Tool)     | Modelagem e transformação de dados    |

## 3. Arquitetura do Projeto

```sql
pipeline_vendas/
├── ingestao/ # Scripts Python
├── models/
│ ├── bronze/ # Dados brutos
│ ├── silver/ # Dados limpos
│ └── gold/ # Análises prontas
└── documentation/ # Esquemas e metadados
```
## 4. Principais Etapas

### Etapa 1: Ingestão dos dados (Python)

Geração de dados sintéticos com Faker:
Dados gerados: 100 clientes, 50 produtos, 20 lojas, 1.000 vendas.

- Exemplo com um dos códigos de ingestão dos dados:
```python
# --- Ingestão de CLIENTES ---
for i in range(1, 101):  # 100 clientes
    cursor.execute(
        """
        INSERT INTO clientes_bronze (cliente_id, nome, cidade, segmento)
        VALUES (%s, %s, %s, %s)
        """,
        (i,  # ID sequencial para evitar duplicatas
         fake.name(),
         fake.city(),
         random.choice(["Varejo", "Atacado", "Online"]))
    )
```
