# Análise e Previsão de Churn - Desafio Telecom X

Este repositório contém a solução completa para o desafio de Data Science da Telecom X, focado em entender e prever a evasão de clientes (churn). O projeto está dividido em duas partes principais:

1.  **Análise Exploratória de Dados (EDA):** Investigação dos dados para identificar os principais fatores e perfis de clientes associados ao churn.
2.  **Modelagem Preditiva:** Construção, treinamento e avaliação de modelos de Machine Learning para prever quais clientes têm maior probabilidade de cancelar o serviço.

## 📂 Estrutura do Repositório
├── challenge_telecomx_parte1.ipynb # Notebook com a Análise Exploratória de Dados (EDA)

├── challenge_telecomx_parte2.ipynb # Notebook com a Modelagem Preditiva (Machine Learning)

├── dados_tratados.csv # Arquivo CSV gerado na Parte 1 e utilizado na Parte 2

└── README.md # Este arquivo

## 🎯 Objetivo do Projeto

O objetivo central deste desafio é utilizar dados de clientes da Telecom X para construir um pipeline de Data Science ponta a ponta, desde a coleta e limpeza de dados até a criação de um modelo preditivo acionável. O resultado final visa fornecer insights e uma ferramenta para a empresa desenvolver estratégias de retenção mais eficazes, reduzindo a perda de receita associada ao churn.

---

## 📈 Parte 1: Análise Exploratória de Dados (EDA)

O notebook `challenge_telecomx_parte1.ipynb` cobre todo o processo de ETL (Extração, Transformação e Carga) e análise inicial.

### Principais Etapas:

1.  **Extração de Dados:** Os dados foram coletados diretamente de uma API em formato JSON e carregados em um DataFrame do Pandas.
2.  **Limpeza e Tratamento:**
    *   Correção de tipos de dados (ex: `TotalGasto` de texto para numérico).
    *   Tratamento de valores ausentes e inconsistentes, utilizando a mediana para imputação.
    *   Remoção de registros que não agregavam valor à análise de churn.
3.  **Engenharia de Features:**
    *   Criação de novas colunas como `Faturamento_Diario` e `Quantidade_Servicos` para aprofundar a análise.
4.  **Padronização:**
    *   Conversão de colunas binárias (Sim/Não) para formato numérico (1/0).
    *   Renomeação das colunas para facilitar a interpretação.

### Principais Descobertas da EDA:

A análise revelou uma taxa de churn de **26,5%** e identificou um perfil claro de cliente com alta propensão a cancelar:

-   **Tipo de Contrato:** Clientes com contrato **Mês a Mês** são os que mais cancelam.
-   **Tempo de Contrato (Tenure):** A maioria dos cancelamentos ocorre nos **primeiros meses**.
-   **Faturamento Mensal:** Faturas **mais altas** estão correlacionadas com maior churn.
-   **Serviços Adicionais:** A ausência de serviços de valor agregado, como **Suporte Técnico** e **Segurança Online**, é um forte indicador de risco.

O DataFrame tratado e limpo foi salvo como `dados_tratados.csv` para ser utilizado na próxima fase.

---

## 🤖 Parte 2: Modelagem Preditiva de Machine Learning

O notebook `challenge_telecomx_parte2.ipynb` foca na construção de modelos preditivos para identificar clientes com risco de churn.

### Principais Etapas:

1.  **Preparação para Modelagem:**
    *   Carregamento do arquivo `dados_tratados.csv`.
    *   Separação dos dados em variáveis preditoras (X) e variável alvo (y).
    *   Divisão em conjuntos de **treino (70%)** e **teste (30%)** de forma estratificada.
2.  **Pré-processamento com Pipeline:**
    *   Criação de um `ColumnTransformer` para aplicar `StandardScaler` em variáveis numéricas e `OneHotEncoder` em variáveis categóricas.
3.  **Construção e Treinamento dos Modelos:**
    *   **Modelo 1: Regressão Logística** - Um modelo linear robusto e interpretável.
    *   **Modelo 2: Random Forest** - Um modelo de conjunto poderoso, com balanceamento de classes.
4.  **Avaliação e Comparação:**
    *   Os modelos foram avaliados usando **Acurácia**, **Relatório de Classificação** (Precisão, Recall, F1-Score) e a **Curva ROC/AUC**.

### Resultados Finais:

O modelo de **Regressão Logística foi o escolhido** por apresentar um desempenho superior e mais equilibrado, com um **AUC de 0.835** e um **Recall de 55%** para a classe "Churn", indicando uma excelente capacidade de identificar corretamente os clientes que irão cancelar.

### Importância das Variáveis (Feature Importance):

Os fatores que mais influenciam a previsão do modelo são, em ordem de importância:
1.  `Meses_de_Contrato`
2.  `Total_Gasto`
3.  `Faturamento_Mensal`
4.  `Tipo_Contrato_Month-to-month`
5.  `Forma_de_Pagamento_Electronic check`

---

## 🚀 Como Executar o Projeto no Google Colab

Para executar este projeto no Google Colab, não é necessário instalar nenhuma dependência. Siga os passos abaixo:

1.  **Acesse o Google Colab:**
    *   Vá para [colab.research.google.com](https://colab.research.google.com).

2.  **Abra os notebooks a partir do GitHub:**
    *   No Colab, vá em `Arquivo > Abrir notebook`.
    *   Selecione a aba **GitHub**.
    *   Cole a URL deste repositório e pressione Enter.
    *   Abra o notebook `challenge_telecomx_parte1.ipynb`.

3.  **Execute a Parte 1:**
    *   No notebook `challenge_telecomx_parte1.ipynb`, vá em `Ambiente de execução > Executar tudo`.
    *   Ao final da execução, o arquivo `dados_tratados.csv` será gerado e salvo no ambiente temporário do Colab. Você poderá vê-lo no painel de arquivos à esquerda.

4.  **Execute a Parte 2:**
    *   Repita o passo 2 para abrir o notebook `challenge_telecomx_parte2.ipynb`.
    *   Como o arquivo `dados_tratados.csv` já está no ambiente do Colab (gerado pela Parte 1), você pode simplesmente ir em `Ambiente de execução > Executar tudo` para treinar e avaliar os modelos.

> **Importante:** O ambiente do Google Colab é temporário. Se sua sessão for desconectada, os arquivos gerados (como `dados_tratados.csv`) serão perdidos. Por isso, é essencial executar a Parte 1 antes da Parte 2 na mesma sessão.

## 🛠️ Ferramentas Utilizadas

*   **Linguagem:** Python 3
*   **Bibliotecas Principais:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Requests
*   **Ambiente:** Jupyter Notebook / Google Colab
