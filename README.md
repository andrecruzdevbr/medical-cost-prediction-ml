# Predição de Custos Médicos com Machine Learning

Projeto de Aprendizado Supervisionado voltado à previsão de custos médicos individuais a partir de características demográficas, comportamentais e geográficas.

**Autor:** André Douglas da Silva Cruz

---

## Objetivo

Desenvolver e comparar modelos de regressão capazes de estimar a variável `charges`, que representa os custos médicos individuais.

O projeto percorre um pipeline completo de Machine Learning, incluindo análise exploratória dos dados, pré-processamento, treinamento de modelos, avaliação de métricas e interpretação dos resultados.

---

## Base de Dados

A base possui **1.338 registros** e **7 variáveis**.

| Variável   | Descrição                                  |
| ---------- | ------------------------------------------ |
| `age`      | Idade do indivíduo                         |
| `sex`      | Sexo                                       |
| `bmi`      | Índice de Massa Corporal                   |
| `children` | Número de filhos/dependentes               |
| `smoker`   | Indica se o indivíduo é fumante            |
| `region`   | Região de residência                       |
| `charges`  | Custos médicos individuais — variável alvo |

As variáveis `age`, `bmi`, `children` e `charges` são numéricas. As variáveis `sex`, `smoker` e `region` são categóricas.

---

## Etapas do Projeto

### 1. Exploração Inicial

Foram analisados:

* estrutura e dimensões da base;
* tipos de dados;
* estatísticas descritivas;
* valores ausentes.

A base não apresentou valores nulos, permitindo avançar diretamente para as etapas de análise e modelagem.

### 2. Análise Exploratória dos Dados

Foram construídos gráficos para investigar a relação entre os atributos e os custos médicos:

* idade × custos médicos;
* IMC × custos médicos;
* comparação de custos entre fumantes e não fumantes.

A análise indicou que idade, IMC e principalmente o tabagismo apresentam associação relevante com os custos médicos.

### 3. Pré-processamento

As variáveis categóricas foram convertidas em variáveis numéricas por meio de One-Hot Encoding com `pd.get_dummies()`.

Foi utilizado `drop_first=True` para reduzir redundância entre as categorias criadas.

Em seguida, os dados foram divididos em:

* **80% para treinamento** — 1.070 registros;
* **20% para teste** — 268 registros.

### 4. Modelos Avaliados

Foram treinados quatro modelos de regressão:

1. Regressão Linear Simples, utilizando apenas a variável `age`;
2. Regressão Linear Múltipla, utilizando todas as variáveis disponíveis;
3. Ridge Regression, com padronização das variáveis;
4. Random Forest Regressor.

---

## Resultados

Os modelos foram avaliados utilizando as métricas MAE, RMSE e R².

| Modelo                    |     MAE |     RMSE |   R² |
| ------------------------- | ------: | -------: | ---: |
| Random Forest Regressor   | 2559.94 |  4597.05 | 0.86 |
| Regressão Linear Múltipla | 4181.19 |  5796.28 | 0.78 |
| Ridge Regression          | 4182.80 |  5796.98 | 0.78 |
| Regressão Linear Simples  | 9173.26 | 11661.22 | 0.12 |

O Random Forest Regressor apresentou o melhor desempenho, explicando aproximadamente **86% da variação dos custos médicos** no conjunto de teste.

A comparação entre os modelos lineares mostrou que utilizar múltiplas variáveis elevou o R² de **0.12 para 0.78**, demonstrando que idade isoladamente não é suficiente para prever os custos médicos com boa precisão.

---

## Importância das Variáveis

A importância das variáveis foi analisada a partir do modelo Random Forest.

| Variável           | Importância |
| ------------------ | ----------: |
| `smoker_yes`       |      0.6100 |
| `bmi`              |      0.2149 |
| `age`              |      0.1342 |
| `children`         |      0.0194 |
| `sex_male`         |      0.0063 |
| `region_northwest` |      0.0057 |
| `region_southeast` |      0.0053 |
| `region_southwest` |      0.0042 |

O tabagismo foi a variável mais relevante para as previsões realizadas pelo modelo, seguido por IMC e idade. Essa importância representa contribuição para a predição do modelo e não uma relação causal.

---

## Principais Insights

* Fumantes apresentam custos médicos consideravelmente mais elevados do que não fumantes;
* Custos médicos tendem a aumentar conforme a idade avança;
* IMC mais elevado está associado a maior dispersão e a custos potencialmente maiores;
* Modelos multivariados apresentam desempenho muito superior ao modelo baseado apenas em idade;
* O Random Forest capturou melhor relações não lineares e interações entre as variáveis.

---

## Tecnologias Utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn

---

## Estrutura do Repositório

```text
medical-cost-prediction-ml/
│
├── medical_cost_prediction_ml.ipynb
├── custo_medico.csv
└── README.md
```

---

## Como Executar

1. Clone este repositório:

```bash
git clone https://github.com/andrecruzdevbr/medical-cost-prediction-ml.git
```

2. Entre na pasta do projeto:

```bash
cd medical-cost-prediction-ml
```

3. Instale as dependências:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

4. Execute o notebook:

```bash
jupyter notebook
```

Abra o arquivo `medical_cost_prediction_ml.ipynb`.

---

## Conclusão

Os resultados demonstraram que tabagismo, IMC e idade são fatores relevantes para a previsão dos custos médicos. O Random Forest Regressor apresentou o melhor desempenho, com R² de 0.86. A inclusão de múltiplas variáveis melhorou significativamente as previsões quando comparada ao uso da idade isoladamente. Apesar do bom desempenho, a ausência de informações clínicas limita a capacidade de explicar completamente os custos médicos.
