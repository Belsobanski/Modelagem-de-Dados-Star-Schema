# 🌟 Projeto de Modelagem de Dados - YouTube 2025 Dataset

## 🧠 Visão Geral

Este projeto aplica a modelagem de dados no formato Star Schema utilizando o dataset futurista do YouTube 2025, disponível no [Kaggle](https://www.kaggle.com/datasets/amansingh0000000/youtube-2025-dataset).  
O objetivo é estruturar os dados para análises, construção de dashboards e aplicação em pipelines ETL.

## 🛠️ Tecnologias Utilizadas

- Python
- Pandas
- Power BI

## 💄 Modelagem Star Schema

- **Tabela Fato: `fato_canal_youtube`**
  - Total Videos
  - Total Subscribers
  - Members Count
  - AI Generated Content (%)
  - Engagement Score
  - Content Value Index

- **Tabelas Dimensão**
  - `dim_youtuber`
    - Youtuber Name
  - `dim_canal`
    - Channel Name
    - Youtuber Name
    - Best Video
    - Avg Video Length (min)
  - `dim_tecnologia`
    - Neural Interface Compatible
    - Metaverse Integration Level
    - Quantum Computing Topics
    - Holographic Content Rating

## 🔥 Como foi feito

```python
import pandas as pd
from graphviz import Digraph
from IPython.display import display

# Carregar o dataset original
file_path = 'youtube_2025_dataset_202504061614.csv'
df = pd.read_csv(file_path)
display(df)

# Tabela Dimensão: Youtuber
# =========================
dim_youtuber = df[['Youtuber Name']].drop_duplicates().reset_index(drop=True)
dim_youtuber['Youtuber ID'] = dim_youtuber.index + 1
display(dim_youtuber)

# =========================
# Tabela Dimensão: Canal
# =========================
dim_canal = df[['Channel Name', 'Youtuber Name', 'Best Video', 'Avg Video Length (min)']].drop_duplicates().reset_index(drop=True)
dim_canal = dim_canal.merge(dim_youtuber, on='Youtuber Name', how='left')
dim_canal['Channel ID'] = dim_canal.index + 1
display(dim_canal)

# =========================
# Tabela Dimensão: Tecnologia
# =========================
dim_tecnologia = df[['Channel Name', 'Neural Interface Compatible', 'Metaverse Integration Level', 'Quantum Computing Topics', 'Holographic Content Rating']].drop_duplicates().reset_index(drop=True)
dim_tecnologia = dim_tecnologia.merge(dim_canal[['Channel Name', 'Channel ID']], on='Channel Name', how='left')
dim_tecnologia['Tecnologia ID'] = dim_tecnologia.index + 1
display(dim_tecnologia)

# =========================
# Tabela Fato: Canal YouTube
# =========================
fato_canal_youtube = df[['Channel Name', 'Total Videos', 'Total Subscribers', 'Members Count', 'AI Generated Content (%)', 'Engagement Score', 'Content Value Index']]
fato_canal_youtube = fato_canal_youtube.merge(dim_canal[['Channel Name', 'Channel ID']], on='Channel Name', how='left')
display(fato_canal_youtube)

# =========================
# Salvar em arquivos CSV para uso posterior
# =========================
dim_youtuber.to_csv('dim_youtuber.csv', index=False)
dim_canal.to_csv('dim_canal.csv', index=False)
dim_tecnologia.to_csv('dim_tecnologia.csv', index=False)
fato_canal_youtube.to_csv('fato_canal_youtube.csv', index=False)
```

## 📊 Dashboard Gerado

- Top 10 Canais por Engajamento
- Top Youtubers por Total de Inscritos
- Distribuição do Conteúdo Gerado por IA (%)

## ✨ Conclusão

Esse projeto mostra como estruturar dados brutos em um formato analítico ideal, preparando-os para visualizações, relatórios e aplicações em Machine Learning.
