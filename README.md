# Projeto de Machine Learning — Dados Meteorológicos

## 1. Objetivo

O objetivo deste projeto é aplicar técnicas de Machine Learning sobre dados meteorológicos, realizando duas tarefas:

- **Classificação:** prever a categoria relacionada à fonte de energia.
- **Regressão:** prever o valor de **radiação solar (`radiacao_w_m2`)** a partir de variáveis meteorológicas.

Para cada tarefa foram utilizados três modelos, totalizando **seis modelos de Machine Learning**.

---

## 2. Dados

### 2.1 Tarefa de Classificação

Os dados foram utilizados para realizar a classificação entre as categorias:

- Eólica
- Hidráulica
- Solar

O conjunto de dados possui **3.876 instâncias**, conforme apresentado no Orange.

Os modelos utilizados foram:

1. Logistic Regression
2. k-Nearest Neighbors (kNN)
3. Random Forest

---

### 2.2 Tarefa de Regressão

A tarefa de regressão utiliza dados meteorológicos para prever a variável:

- `radiacao_w_m2`

As variáveis utilizadas como entrada foram:

- `temperatura_c`
- `umidade_pct`
- `nuvens_pct`
- `vento_kmh`
- `hora`

A coluna `data_hora` foi mantida como atributo do tipo meta.

O conjunto utilizado no Orange possui **1.001 instâncias**, **6 variáveis numéricas** e **1 atributo meta**.

---

## 3. Origem e período dos dados

Os dados utilizados neste projeto são provenientes do arquivo:

`meteo_regressao_orange.csv`

O arquivo utilizado no Orange possui **1.001 registros** para a tarefa de regressão.

> **Observação:** a origem da API e o período exato dos dados devem ser informados aqui conforme a documentação/API utilizada no projeto.

---

## 4. Ferramentas utilizadas

- Python
- Jupyter Notebook
- Orange Data Mining
- Pandas
- NumPy
- Matplotlib
- Scikit-learn

---

# 5. Tarefa 1 — Classificação

## 5.1 Modelos utilizados

Foram treinados e comparados três modelos:

- Logistic Regression
- kNN
- Random Forest

A avaliação foi realizada utilizando o componente **Test and Score** do Orange.

---

## 5.2 Métricas

Foram utilizadas as seguintes métricas:

- AUC — Area Under the ROC Curve
- CA — Classification Accuracy
- F1 — F1 Score
- Precision
- Recall
- MCC — Matthews Correlation Coefficient

---

## 5.3 Resultados

| Modelo | AUC | CA | F1 | Precision | Recall | MCC |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression | 0.886 | 0.807 | 0.805 | 0.815 | 0.807 | 0.713 |
| kNN | 0.954 | 0.870 | 0.871 | 0.872 | 0.870 | 0.805 |
| Random Forest | 0.994 | 0.970 | 0.970 | 0.971 | 0.970 | 0.955 |

---

## 5.4 Matriz de confusão

A matriz de confusão apresentada no Orange possui as seguintes classes:

- Eólica
- Hidráulica
- Solar

| Real \ Predito | Eólica | Hidráulica | Solar | Total |
|---|---:|---:|---:|---:|
| Eólica | 1092 | 78 | 30 | 1200 |
| Hidráulica | 98 | 1290 | 88 | 1476 |
| Solar | 313 | 111 | 776 | 1200 |
| **Total** | **1443** | **1509** | **919** | **3876** |

---

## 5.5 Interpretação da classificação

Os resultados mostram diferenças entre os três modelos avaliados.

A Logistic Regression apresentou AUC de 0.886 e acurácia de 0.807.

O kNN apresentou AUC de 0.954 e acurácia de 0.870.

O Random Forest apresentou AUC de 0.994 e acurácia de 0.970, além de F1 de 0.970 e MCC de 0.955.

A matriz de confusão permite observar a quantidade de classificações corretas e incorretas para cada uma das três classes.

---

# 6. Tarefa 2 — Regressão

## 6.1 Variável alvo

A variável utilizada como alvo da regressão foi:

`radiacao_w_m2`

As variáveis utilizadas para realizar a previsão foram:

- `temperatura_c`
- `umidade_pct`
- `nuvens_pct`
- `vento_kmh`
- `hora`

---

## 6.2 Modelos utilizados

Foram treinados e comparados três modelos:

1. Linear Regression
2. Tree
3. Random Forest

A avaliação foi realizada utilizando o componente **Test and Score** do Orange.

---

## 6.3 Métricas

Foram utilizadas as seguintes métricas:

- MSE — Mean Squared Error
- RMSE — Root Mean Squared Error
- MAE — Mean Absolute Error
- MAPE — Mean Absolute Percentage Error
- sMAPE — Symmetric Mean Absolute Percentage Error
- R² — Coeficiente de determinação

---

## 6.4 Resultados

| Modelo | MSE | RMSE | MAE | MAPE | sMAPE | R² |
|---|---:|---:|---:|---:|---:|---:|
| Linear Regression | 22846.675 | 151.151 | 118.830 | 48.397 | 35.088 | 0.652 |
| Tree | 7570.825 | 87.010 | 61.441 | 18.900 | 16.882 | 0.885 |
| Random Forest | 5072.670 | 71.223 | 50.677 | 15.639 | 14.040 | 0.923 |

---

## 6.5 Interpretação da regressão

A Linear Regression apresentou R² de 0.652.

O modelo Tree apresentou R² de 0.885, com redução dos valores de erro em comparação com a regressão linear.

O Random Forest apresentou R² de 0.923 e os menores valores de MSE, RMSE, MAE, MAPE e sMAPE entre os três modelos avaliados.

Esses resultados indicam que, neste conjunto de dados e na configuração utilizada no experimento, o Random Forest apresentou maior capacidade de explicar a variação da variável `radiacao_w_m2` e menores erros de previsão.

---

# 7. Estrutura dos experimentos no Orange

## 7.1 Classificação

O fluxo utilizado foi estruturado da seguinte maneira:

```text
Carga - Dados Classificação
            |
            v
      Select Columns
       /     |      \
      v      v       v
Logistic   Random    kNN
Regression Forest
      \      |       /
       \     |      /
        v    v     v
        Test and Score
              |
              v
       Confusion Matrix
