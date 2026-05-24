# ✈️ Tech Challenge 3 — Predição de Atraso de Voos

Projeto de Machine Learning para prever se um voo chegará atrasado (**≥ 15 minutos**, critério da FAA) usando apenas informações disponíveis **antes da decolagem**. O pipeline inclui EDA, feature engineering, modelos supervisionados (Regressão Logística e Random Forest) e não supervisionados (K-Means e DBSCAN).

---

## Estrutura do projeto

```
tech_challenge_3/
├── data/
│   ├── raw/                  # Dados brutos (não versionados no git)
│   │   ├── flights.csv       # Dataset principal (~565 MB, ~5.8M voos)
│   │   ├── airlines.csv      # Códigos IATA → nome da companhia
│   │   └── airports.csv      # Informações dos aeroportos
│   └── refined/              # Dados processados (gerados pelo notebook 02)
│       └── flights_features.csv
├── notebooks/
│   ├── 01_eda.ipynb                  # Análise exploratória
│   ├── 02_feature_engineering.ipynb  # Engenharia de features
│   ├── 03_supervised_model.ipynb     # Regressão Logística + Random Forest
│   └── 04_unsupervised_model.ipynb   # K-Means + DBSCAN
├── pyproject.toml
└── uv.lock
```

---

## Instalação

### Pré-requisitos

- [uv](https://docs.astral.sh/uv/getting-started/installation/) instalado
- Python ≥ 3.14

### Passos

```bash
# Clone o repositório
git clone <url-do-repositorio>
cd tech_challenge_3

# Crie o ambiente virtual e instale as dependências
uv sync

# Ative o ambiente virtual
source .venv/bin/activate   # Linux/macOS
# ou
.venv\Scripts\activate      # Windows
```

---

## Obtendo os dados

Os arquivos de dados **não estão versionados** no repositório (o `flights.csv` tem ~565 MB). O dataset é o [2015 Flight Delays and Cancellations](https://www.kaggle.com/datasets/usdot/flight-delays) disponível publicamente no Kaggle.

### Opção recomendada — Download manual

1. Acesse: [kaggle.com/datasets/usdot/flight-delays](https://www.kaggle.com/datasets/usdot/flight-delays)
2. Clique em **Download** (requer conta gratuita no Kaggle)
3. Crie as pastas manualmente:

   ```bash
   mkdir -p data/raw data/refined
   ```

4. Extraia os arquivos `flights.csv`, `airlines.csv` e `airports.csv` para `data/raw/`

---

## Executando os notebooks

Com o ambiente ativado, inicie o Jupyter:

```bash
jupyter notebook
# ou
jupyter lab
```

Execute os notebooks **na ordem numérica**:

| # | Notebook | Descrição |
|---|----------|-----------|
| 01 | `01_eda.ipynb` | Análise exploratória dos dados brutos |
| 02 | `02_feature_engineering.ipynb` | Gera `data/refined/flights_features.csv` |
| 03 | `03_supervised_model.ipynb` | Classificação: Regressão Logística e Random Forest |
| 04 | `04_unsupervised_model.ipynb` | Clustering: K-Means e DBSCAN |

> **O notebook `02` deve ser executado antes dos notebooks `03` e `04`**, pois ele gera o arquivo `data/refined/flights_features.csv` consumido pelos modelos.

---

## Sobre o projeto

### Variável alvo

`IS_DELAYED = 1` se `ARRIVAL_DELAY ≥ 15 minutos` (critério da FAA), caso contrário `IS_DELAYED = 0`.

### Premissa fundamental

Utilizamos apenas **features pré-voo** — informações disponíveis antes da decolagem — para evitar *data leakage*. Colunas como `DEPARTURE_DELAY`, `TAXI_OUT` e outras capturadas em tempo de execução são excluídas.

### Modelos

- **Supervisionados:** Regressão Logística (baseline interpretável) e Random Forest (captura relações não-lineares)
- **Não supervisionados:** K-Means e DBSCAN para descoberta de padrões latentes nos voos

---

## Dependências principais

| Biblioteca | Uso |
|------------|-----|
| `pandas` | Manipulação de dados |
| `numpy` | Operações numéricas |
| `scikit-learn` | Modelos de ML |
| `matplotlib` / `seaborn` | Visualizações |
| `jupyter` / `ipykernel` | Ambiente de notebooks |

Gerenciadas via `uv` — veja o `pyproject.toml` para versões exatas.
