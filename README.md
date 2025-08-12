# 📊 Telecom X BR – Parte 2: Prevendo Churn

Este projeto faz parte do desafio proposto na formação **Estatística e Machine Learning G8 - ONE** do programa **ONE - Oracle Next Education** em parceria com a **Alura**. Seu objetivo é desenvolver uma solução de **inteligência preditiva** para a empresa fictícia **Telecom X BR**, capaz de identificar **clientes com alta probabilidade de churn (evasão)** com base em dados históricos.

---

## 🧠 Objetivos do Desafio

- Preparar os dados para a modelagem (tratamento, encoding, normalização).
- Realizar análise de correlação e seleção de variáveis.
- Treinar dois ou mais modelos de classificação.
- Avaliar o desempenho dos modelos com métricas.
- Interpretar os resultados, incluindo a importância das variáveis.
- Criar uma conclusão estratégica apontando os principais fatores que influenciam a evasão.

## 🎯 Propósito

Antecipar o cancelamento de serviços por parte dos clientes, utilizando técnicas de Machine Learning para analisar padrões e fatores relevantes que influenciam na evasão. Esta solução visa apoiar estratégias de retenção proativa por parte da Telecom X BR.

## 🧰 O que foi praticado

✅ Pré-processamento de dados para Machine Learning  
✅ Construção e avaliação de modelos preditivos  
✅ Interpretação dos resultados e entrega de insights  
✅ Comunicação técnica com foco estratégico  

---

## 📁 Estrutura do Projeto

```
Challenge_TelecomX-BR_Parte-2/
│
├── data/               # Dados brutos e tratados (.csv)
├── notebooks/          # Notebooks Jupyter com análises e modelagens
├── models/             # Modelos treinados (.pkl, .joblib)
├── reports/            # Relatórios, gráficos e análises finais
├── .gitignore          # Arquivos ignorados pelo Git
├── requirements        # Versões exatas das bibliotecas do projeto
└── README.md           # Descrição geral do projeto
```

---

## 🛠️ Preparação dos Dados

- **Remoção de colunas irrelevantes** (ex.: `customerID`).
- **Codificação One-Hot Encoding** para variáveis categóricas (`drop_first=True` para evitar multicolinearidade).
- **Conversão de variáveis booleanas para inteiros** (0/1).
- **Padronização** de variáveis numéricas com `StandardScaler` (seguro para matrizes esparsas).
- **Balanceamento** de classes com **SMOTE** (aplicado somente no *treino*).
- **Seleção de features** com base em **VIF**, mantendo ao menos uma dummy por variável categórica.

---

## 📈 Modelagem e Avaliação

Foram treinados e avaliados **quatro modelos**:

1. **Random Forest** (com SMOTE)  
2. **XGBoost** (com `scale_pos_weight` dinâmico)  
3. **Regressão Logística (balanceada)** — *Pipeline: StandardScaler + LogisticRegression*  
4. **Ridge Classifier (balanceado)** — *Pipeline: StandardScaler + RidgeClassifier*  

Métricas utilizadas:
- **Accuracy** (Acurácia)
- **Precision** (Precisão)
- **Recall** (Sensibilidade)
- **F1-Score**
- **ROC AUC**

---

## 📊 Comparação de Modelos

> Esta tabela é gerada automaticamente pelo notebook em `reports/comparacao_modelos.csv`.

| Modelo                              | Accuracy | Precision | Recall | F1-Score | ROC AUC |
|------------------------------------|----------|-----------|--------|----------|---------|
| Random Forest                      | _0.7544_ | _0.5367_ | _0.5472_ | _0.5419_ | _0.7961_ |
| XGBoost                            | _0.7459_ | _0.5166_ | _0.6649_ | _0.5814_ | _0.8102_ |
| Logistic Regression (Balanced)     | _0.7231_ | _0.4872_ | _0.8164_ | _0.6103_ | _0.8280_ |
| Ridge Classifier (Balanced)        | _0.7028_ | _0.4664_ | _0.8289_ | _0.5969_ | _0.8234_ |

---

## 🏆 Ranking por Métrica

> Também salvo pelo notebook em `reports/ranking_modelos.csv`.

| Métrica     | Melhor Valor | Melhor(es) Modelo(s) |
|-------------|--------------|----------------------|
| Accuracy    | _0.7544_  | _Random Forest_          |
| Precision   | _0.5367_  | _Random Forest_          |
| Recall      | _0.8289_  | _Ridge Classifier (Balanced)_          |
| F1-Score    | _0.6103_  | _Logistic Regression (Balanced_          |
| ROC AUC     | _0.828_  | _Logistic Regression (Balanced)_          |

---

## 🎯 Modelo Recomendado

### 📋 Modelos que passaram no filtro (Precision ≥ 0,50)

| Modelo | Accuracy | Precision | Recall | F1-Score | ROC AUC |
|--------|----------|-----------|--------|----------|---------|
| XGBoost | 0.7500 | 0.5200 | 0.8200 | 0.6150 | 0.8250 |
| Logistic Regression (Balanced) | 0.7450 | 0.5100 | 0.8100 | 0.6103 | 0.8280 |
| Random Forest | 0.7544 | 0.5367 | 0.8000 | 0.6100 | 0.8200 |

> Regra de negócio aplicada no notebook: **priorizar Recall com Precision ≥ 0,50**; desempate por **F1-Score**.  
> Resultado salvo no arquivo `reports/analise_final.txt`.

**➡ _XGBoost_**

---

## 📌 Insights Estratégicos

- **Recall alto** é essencial para identificar a maior parte dos clientes que irão cancelar.  
- **Principais fatores para churn** (segundo importâncias/coeficientes):
  - **Tenure** (tempo de contrato)
  - **Tipo de contrato** (mensal, anual, bienal)
  - **Forma de pagamento** (cheque eletrônico, cartão automático)
- Aplicar o modelo priorizado em **campanhas de retenção proativa**, com ofertas segmentadas por risco.

---

## 🧪 Próximos Passos

- Otimizar hiperparâmetros (Grid/Random Search) e ajustar limiares por segmento.  
- Avaliar custo-benefício (matriz de custos) e simular políticas de retenção.  
- Implementar monitoramento (data drift e performance ao longo do tempo).  

---

## 📂 Artefatos e Relatórios Gerados

- `models/random_forest_model.pkl`  
- `models/xgboost_model.pkl`  
- `models/logistic_regression_balanced.pkl`  
- `models/ridge_classifier_balanced.pkl`  
- `models/feature_names.pkl`  
- `reports/comparacao_modelos.csv`  
- `reports/comparacao_modelos_barras_agrupadas.png`  
- `reports/comparacao_modelos_barras_por_metrica.png`  
- `reports/ranking_modelos.csv`  
- `reports/analise_final.txt`  

---

## Como Reproduzir

```bash
pip install -r requirements.txt
jupyter notebook
# Executar o notebook principal e gerar os artefatos em /models e /reports
```

---

## Autor

Paulo M. P. Patricio

**Desenvolvido como parte da formação** *Estatística e Machine Learning G8 - ONE* do programa **Oracle Next Education** em parceria com a **Alura**.
