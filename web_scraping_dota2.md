# Análise Estatística da Dream League Season 26

Este projeto consiste em um web scraping da página Dota 2 ProTracker - Torneios, com o objetivo de coletar e analisar dados estatísticos dos heróis mais relevantes da última competição que ocorreu, a Dream League Season 26.

### Objetivo

- Extrair e organizar informações como:
  
  - Heróis mais escolhidos (picks)
    
  - Heróis mais banidos (bans)
    
  - Maiores e menores taxas de vitória (win rate) em picks significativos (≥10 partidas)

### Ferramentas Utilizadas
Python (Bibliotecas: Selenium, Pandas, Seaborn e Matplotlib)

### Código Web Scraping

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import pandas as pd
import time

service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)

try:
    driver.get("https://dota2protracker.com/tournaments")
    print("Carregando página...")

    # Espera pela tabela e seu container de scroll
    container = WebDriverWait(driver, 20).until(
        EC.presence_of_element_located((By.XPATH, '//svelte-virtual-list-viewport')))
    rows_selector = '//svelte-virtual-list-row[.//span[@class="text-white"]]'

    # Parâmetros de controle
    scroll_pause = 1.2
    max_attempts = 5
    unique_heroes = set()
    all_data = []
    last_window = []
    attempts = 0

    # Altura total estimada baseada no container
    total_height = driver.execute_script("return arguments[0].scrollHeight", container)
    scroll_step = int(total_height * 0.2)  # 20% da altura como passo

    print("Iniciando raspagem")
    
    for current_pos in range(0, total_height + scroll_step, scroll_step):
        # Scroll para posição calculada
        driver.execute_script(f"arguments[0].scrollTop = {current_pos}", container)
        time.sleep(scroll_pause)
        
        # Captura janela visível atual
        visible_rows = WebDriverWait(driver, 10).until(
            EC.presence_of_all_elements_located((By.XPATH, rows_selector)))
        
        # Filtra novas linhas
        new_rows = [row for row in visible_rows if row not in last_window]
        
        if not new_rows:
            attempts += 1
            if attempts >= max_attempts:
                print("Quebra por tentativas sem novos dados")
                break
            continue
        
        attempts = 0  # Resetar contador
        
        # Processa novas linhas
        for row in new_rows:
            try:
                hero = row.find_element(By.XPATH, './/span[@class="text-white"]').text
                if hero in unique_heroes:
                    continue
                    
                cells = row.find_elements(
                    By.XPATH,
                    './/div[contains(@class, "text-center") and contains(@class, "svelte-")]'
                )
                
                # Extração robusta com fallback
                record = {
                    'Hero': hero,
                    'Picks': cells[0].text if len(cells) > 0 else 'N/A',
                    'Win Rate': cells[1].find_element(By.XPATH, './/span').text if len(cells) > 1 else 'N/A',
                    'Bans': cells[2].text if len(cells) > 2 else 'N/A',
                    'Contest Rate': cells[3].find_element(By.XPATH, './/span').text if len(cells) > 3 else 'N/A'
                }
                
                all_data.append(record)
                unique_heroes.add(hero)
                print(f"{hero}")
                
            except Exception as e:
                print(f"Erro em linha: {str(e)}")
                continue
        
        last_window = visible_rows

    # Pós-processamento e exportação
    df = pd.DataFrame(all_data)
    print(f"\n Coleta finalizada! {len(df)} heróis únicos")
    
    # Verificação de dados ausentes
    if len(df) < 50:  # Alerta se menos que 50 heróis
        print("Possível perda de dados - verificar conexão/seletores")
    
    df.to_csv('dream_league_26.csv', index=False)
    print(df.head())

except Exception as e:
    print(f"Erro crítico: {str(e)}")

finally:
    driver.quit()
```

### Visualização dos Dados

<iframe src="https://gamma.app/embed/jma2mkyxstranyh" style="width: 700px; max-width: 100%; height: 450px" allow="fullscreen" title="Análise Dream League S26"></iframe>

[Home](./)
