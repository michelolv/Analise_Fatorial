# 📊 Unsupervised Latent Space Extraction via Exploratory Factor Analysis (EFA)
### High-Dimensional Consumer Preference Mining on `AnaFatBeer` Dataset

**Autor:** Michel Lima de Oliveira  
**Domínio:** Inteligência Artificial — Aprendizado de Máquina e Mineração de Dados  
**Área de Aplicação:** Estatística Multivariada, Redução de Dimensionalidade & Engenharia de Atributos Latentes  

---

## 📌 1. Visão Geral do Projeto (Executive Summary)

Este repositório contém uma pipeline estatístico-computacional focada na **descoberta de estruturas latentes não observáveis** e **redução de dimensionalidade multivariada** sobre o conjunto de dados *AnaFatBeer*. Em cenários de **Aprendizado de Máquina (ML)** e **Mineração de Dados (Data Mining)**, dados de alta dimensão frequentemente apresentam multicolinearidade e ruído, o que degrada o desempenho de modelos preditivos e descritivos.

Através da **Análise Fatorial Exploratória (AFE)** e da decomposição espectral, transformamos o espaço de atributos original (7 dimensões de valoração do consumidor) em um espaço de características latentes orthogonalizado e de menor dimensão, maximizando a **variância explicada (91,23%)** e garantindo interpretabilidade semântica para tarefas subsequentes (como clustering avançado ou modelagem preditiva downstream).

---

## 🎯 2. Objetivos Estratégicos & Alinhamento com Aprendizado de Máquina

* **Feature Extraction & Dimensionality Reduction:** Extrair representações latentes densas e não correlacionadas a partir de atributos observáveis de preferência de consumo.
* **Diagnóstico da Estrutura de Correlação:** Avaliar a suposição de esfericidade e adequação amostral (KMO e Teste de Esfericidade de Bartlett) para validar o uso de métodos baseados em vetores próprios (*eigenvalues*).
* **Comparação de Métodos de Estimação:** Implementar o método de **Componentes Principais (PC)** versus estresses de rotação **Varimax (Ortogonal)**.
* **Otimização de Pipeline & Remoção de Feature Redundante:** Avaliar o impacto da eliminação de variáveis com alta carga cruzada (*cross-loadings*) ou fraco suporte latente (`REPUTAT`) para refinar a estabilidade do espaço fatorial final.

---

## 🗃️ 3. Caracterização dos Dados (`AnaFatBeer`)

O dataset reúne escores de preferência ($0 \text{ a } 100$) atribuídos por $N = 200$ consumidores quanto a 7 atributos decisórios na compra de garrafas de cerveja:

| Atributo | Descrição Semântica | Categoria / Natureza |
| :--- | :--- | :--- |
| **`COST`** | Custo do pack | Quantitativa / Econômica |
| **`SIZE`** | Volume de cerveja por pack | Quantitativa / Volume |
| **`ALCOHOL`** | Teor alcoólico (%) | Quantitativa / Composição |
| **`REPUTAT`** | Reputação e valor percebido da marca | Qualitativa Latente / Branding |
| **`COLOR`** | Aspecto visual / Cor | Organoléptica / Sensorial |
| **`AROMA`** | Perfil aromático | Organoléptica / Sensorial |
| **`TASTE`** | Sabor e palatabilidade | Organoléptica / Sensorial |

---

## 🔬 4. Análise Exploratória & Teste de Hipóteses

1. **Normalidade Multivariada:** Avaliada pelos testes de **Shapiro-Wilk Multivariado** e **Royston**. A rejeição da hipótese nula de normalidade ($p < 0.05$) fundamentou a escolha da **Decomposição por Componentes Principais (PC)** como método de extração não paramétrico robusto.
2. **Adequação Amostral (KMO & Bartlett):**
   * **KMO Overall:** $0.67$ (confirmando a existência de variância compartilhada latente).
   * **Teste de Esfericidade de Bartlett:** Rejeição de $H_0: \mathbf{R} = \mathbf{I}$ ($p \approx 0$), garantindo a existência de correlações significativas inter-variáveis.
   * **Detecção de Anomalia:** A variável `REPUTAT` apresentou $MSA = 0.40$ (insuficiente), indicando isolamento estrutural.

### 4.1. Critério de Retenção de Fatores (Kaiser-Guttman)
Aplicou-se o critério dos autovalores superiores à unidade ($\lambda_i \ge 1.0$), determinando a retenção de **2 Fatores Latentes Principais**, capazes de resumir a informação estrutural do sistema.

### 4.2. Rotação do Espaço Fatorial (Varimax)
A aplicação da rotação ortogonal **Varimax** redistribuiu a variância explicada, simplificando a estrutura de cargas fatoriais ($\mathbf{L}$) e eliminando ambiguidades de associação entre variáveis e fatores.

---

## 📈 5. Principais Resultados e Redução Dimensional

### Modelo 1 (7 Atributos Integrais)
* **Variância Total Explicada:** $84,70\%$
* **Problema Identificado:** Presença de cargas cruzadas (*cross-loadings*) elevadas e baixa comunalidade em `REPUTAT`.

### Modelo 2 Refinado (Feature Pruning - Remoção de `REPUTAT`)
* **Variância Total Explicada:** **$91,23\%$** (Ganho substancial de densidade informativa).
* **Estrutura Latente Resultante:**
  * **Fator 1 (Atributos Sensoriais Organolépticos):** Carregado fortemente por `COLOR`, `AROMA` e `TASTE`.
  * **Fator 2 (Atributos Físico-Econômicos):** Carregado por `COST`, `SIZE` e `ALCOHOL`.
* **Comunalidades ($h^2$):** Todas as variáveis mantidas obtiveram $h^2 > 0.88$, comprovando a eficácia da reconstrução dos atributos pelo espaço latente bidimensional.

---

## 🛠️ 6. Empacotamento Tecnológico & Requisitos de Execução

O script foi desenvolvido em **R (Markdown)** utilizando um conjunto robusto de bibliotecas para estatística multivariada e visualização de grafos:

```R
# Dependências Principais
pacman::p_load(
  "psych",       # Análise Fatorial e Testes de Diagnóstico
  "factoextra",   # Visualização Fatorial e Decomposição
  "GPArotation", # Rotações Avançadas do Espaço Fatorial
  "tidyverse",   # Manipulação e Tidy Data Pipelines
  "corrr",       # Processamento de Matrizes de Correlação
  "ggraph",      # Graph Theory & Network Visualizations
  "corrplot",    # Visualização de Matrizes de Adjacência
  "gt"           # Tabelas Formatadas de Alta Qualidade
)
```

---

## 🚀 7. Implicações para Aprendizado de Máquinas e Mineração de Dados

1. **Combate à Maldição da Dimensionalidade (*Curiosity of Dimensionality*):** A redução de 7 para 2 fatores preserva $91,23\%$ da variância total, mitigando o *overfitting* em classificadores ou regressores posteriores.
2. **Eliminação da Multicolinearidade:** Os escores fatoriais gerados via **Método de Bartlett** são ortogonais entre si, tornando-se *inputs* ideais para algoritmos sensíveis à multicolinearidade (ex.: Regressão Logística, SVM, Naive Bayes).
3. **Engenharia de Features Baseada em Teoria:** Transforma variáveis quantitativas brutas em conceitos de alto nível (*Sensoriality Index* vs *Economic-Volume Score*), aprimorando a **XAI (Explainable Artificial Intelligence)** do pipeline.

---

## 👤 Autor

* **Michel Lima de Oliveira**  
* Pesquisa voltada para Aprendizado de Máquina, Mineração de Dados e Estatística Multivariada Aplicada.
