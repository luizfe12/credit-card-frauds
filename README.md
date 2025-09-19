# Detecção de Fraudes em Cartões de Crédito

![Status](https://img.shields.io/badge/status-conclu%C3%ADdo-brightgreen)

## 📖 Visão Geral do Projeto

Este projeto tem como objetivo desenvolver um modelo de Machine Learning capaz de identificar transações fraudulentas em cartões de crédito. Devido à natureza do problema, lidamos com um dataset altamente desbalanceado, onde o número de fraudes representa uma porcentagem mínima do total de transações (~0.17%).

O desafio principal é construir um classificador que maximize a detecção de fraudes reais (alto *recall*) e, ao mesmo tempo, minimize o número de alarmes falsos, evitando o bloqueio de transações legítimas (alta *precisão*).

## 📊 Dataset

O conjunto de dados utilizado foi o ["Credit Card Fraud Detection"](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud), disponível no Kaggle. Ele contém transações feitas por cartões de crédito europeus em setembro de 2013.

**Características do Dataset:**
- **Número de Transações:** 284,807
- **Features:** 31 colunas no total.
  - `Time` e `Amount`: As únicas features não anonimizadas.
  - `V1` a `V28`: Features anonimizadas, resultantes de uma transformação de Análise de Componentes Principais (PCA).
  - `Class`: A variável alvo, onde `1` representa uma fraude e `0` uma transação normal.

## 🛠️ Tecnologias Utilizadas

- **Linguagem:** Python 3
- **Bibliotecas Principais:**
  - `Pandas` para manipulação e análise de dados.
  - `Matplotlib` e `Seaborn` para visualização de dados.
  - `Scikit-learn` para pré-processamento, modelagem e avaliação.
  - `Imbalanced-learn` para técnicas de reamostragem (SMOTE).
  - `XGBoost` para modelagem com Gradient Boosting.

## 🚀 Metodologia

O projeto foi estruturado seguindo as principais etapas de um fluxo de trabalho de Machine Learning:

1.  **Análise Exploratória (EDA):** Verificação da proporção de classes, análise de valores ausentes e estudo da distribuição das features `Time` e `Amount`.
2.  **Pré-processamento:**
    - Padronização (`StandardScaler`) das colunas `Time` e `Amount` para que tivessem a mesma escala das features `V1-V28`.
3.  **Balanceamento de Dados:**
    - Aplicação da técnica **SMOTE (Synthetic Minority Over-sampling Technique)** *apenas no conjunto de treino* para criar exemplos sintéticos da classe minoritária (fraude), evitando que o modelo ficasse enviesado para a classe majoritária.
4.  **Modelagem e Treinamento:**
    - Divisão dos dados em conjuntos de treino e teste (80/20), utilizando estratificação para manter a proporção de classes.
    - Treinamento e comparação de três algoritmos de classificação:
      1.  Regressão Logística (como baseline)
      2.  Random Forest
      3.  XGBoost
5.  **Avaliação:**
    - Análise da Matriz de Confusão.
    - Foco nas métricas de **Precisão (Precision)**, **Revocação (Recall)** e **F1-Score**, que são mais adequadas para datasets desbalanceados do que a Acurácia.

## 📈 Análise dos Resultados

### Distribuição dos Valores de Transação

O boxplot abaixo mostra que, em geral, as transações fraudulentas (Classe 1) tendem a envolver valores monetários menores em comparação com as transações normais (Classe 0). No entanto, ambas as classes possuem uma grande quantidade de outliers.

![Distribuição dos Valores de Transação por Classe](./images/image_4b38cd.png)

### Comparativo de Performance dos Modelos

A tabela abaixo resume o desempenho dos modelos na tarefa de classificar a **Classe 1 (Fraude)** no conjunto de teste:

| Modelo | Precisão (Fraude) | Recall (Fraude) | F1-Score (Fraude) | Conclusão Prática |
| :--- | :---: | :---: | :---: | :--- |
| Regressão Logística | 5% | **95%** | 10% | Pega quase todas as fraudes, mas gera alarmes falsos demais. Inviável. |
| **Random Forest** | **85%** | 87% | **86%** | **O melhor equilíbrio.** Pega a maioria das fraudes com poucos erros. |
| XGBoost | 77% | 88% | 82% | Ótimo em pegar fraudes, mas com mais alarmes falsos que o Random Forest. |

O modelo **Random Forest** se destacou como o grande vencedor, apresentando o melhor equilíbrio entre Precisão e Recall, refletido no maior F1-Score. Ele foi capaz de identificar **87% das fraudes reais**, com uma taxa de acerto de **85%** em suas previsões positivas.

## 🏁 Conclusão

O projeto demonstrou com sucesso a capacidade de construir um modelo eficaz para a detecção de fraudes. O uso da técnica SMOTE foi crucial para lidar com o desbalanceamento dos dados, permitindo que modelos como o Random Forest aprendessem os padrões das transações fraudulentas de forma robusta.

O modelo final (Random Forest) representa uma ferramenta valiosa, capaz de economizar recursos financeiros ao mesmo tempo que minimiza o impacto negativo sobre a experiência de clientes legítimos.

## 🚀 Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
    cd seu-repositorio
    ```
2.  **Crie um ambiente virtual (recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```
3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Execute o notebook ou script principal:**
    Abra o arquivo `.ipynb` no Jupyter Notebook/Lab ou execute o script `.py`.

## ✍️ Autor

- **Luiz Felipe da Silva**
- **LinkedIn:** [https://www.linkedin.com/in/luiz-felipe-da-silva12](https://www.linkedin.com/in/luiz-felipe-da-silva12)
- **GitHub:** [https://github.com/luizfe12](https://github.com/luizfe12)# credit-card-frauds
