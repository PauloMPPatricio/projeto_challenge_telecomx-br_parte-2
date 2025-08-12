## 📌 Critério de Escolha do Modelo Recomendado

O modelo recomendado **não necessariamente** é o que aparece no topo do ranking de cada métrica isolada.  
Ele é definido com base em uma **regra de negócio**:

1. Filtrar modelos com **Precision ≥ 0,50**  
2. Entre eles, escolher o que tiver **maior Recall**  
3. Em caso de empate no Recall, usar o **F1-Score** como desempate  
4. Se nenhum modelo atingir a Precision mínima, escolher o de maior F1-Score

### 📋 Modelos que passaram no filtro (Precision ≥ 0,50)

| Modelo | Accuracy | Precision | Recall | F1-Score | ROC AUC |
|--------|----------|-----------|--------|----------|---------|
| XGBoost | 0.7500 | 0.5200 | 0.8200 | 0.6150 | 0.8250 |
| Logistic Regression (Balanced) | 0.7450 | 0.5100 | 0.8100 | 0.6103 | 0.8280 |
| Random Forest | 0.7544 | 0.5367 | 0.8000 | 0.6100 | 0.8200 |

### 🏆 Modelo Recomendado pelo Critério

➡ **XGBoost** — Maior Recall entre os modelos com Precision mínima exigida.

