📊 Análise Fatorial Exploratória (AFE) Aplicada à Preferência de Consumo
📌 Visão Geral do Projeto
Este repositório/documento apresenta um pipeline analítico em R voltado para a Redução de Dimensionalidade e Engenharia de Atributos (Feature Engineering). O estudo utiliza a técnica de Análise Fatorial Exploratória (AFE) sobre o dataset AnaFatBeer.txt (disponível em github.com/fabiorocha/DataSets), que mapeia a percepção de 200 consumidores em relação a sete atributos de um pack de cerveja.

No contexto de Machine Learning e Data Mining, este projeto demonstra como extrair variáveis latentes (fatores) a partir de variáveis observáveis altamente correlacionadas, mitigando o problema da maldição da dimensionalidade e otimizando a performance de futuros modelos preditivos.

🎯 Objetivos e Metodologia
O objetivo central é explorar a estrutura de covariância da base de dados para identificar os fatores subjacentes que regem a decisão de compra dos consumidores (variáveis originais: COST, SIZE, ALCOHOL, REPUTATION, COLOR, AROMA, TASTE).

O Pipeline Analítico contempla:
Análise Descritiva e Visualização de Dados: Avaliação da distribuição e dispersão dos escores (0 a 100).

Verificação de Premissas Estatísticas: Testes de Normalidade Multivariada (Shapiro-Wilk e Royston) para definição do método de extração mais robusto.

Análise de Estrutura de Correlação: Uso da matriz de Pearson, gráficos de correlação e redes (network graphs) para mapear as interdependências entre as variáveis.

Validação da Aplicabilidade: Teste de Esfericidade de Bartlett e Critério de Kaiser-Meyer-Olkin (KMO) para atestar a adequação da amostra.

Extração e Rotação: Comparação de métodos de extração (Componentes Principais e Fatores Principais) e aplicação de rotação ortogonal (Varimax) para maximizar a interpretabilidade das cargas fatoriais.

Validação do Modelo: Análise de comunalidades, variâncias específicas, resíduos e soma de quadrados dos resíduos.

🛠️ Tecnologias e Bibliotecas Utilizadas
O ecossistema foi construído inteiramente em R, com foco em reprodutibilidade e visualizações de alto padrão:

Manipulação e Estruturação: tidyverse, dplyr, tidyr, tibble

Análise Fatorial e Estatística: psych, GPArotation, MVar.pt, rela, Hmisc

Testes Multivariados: MVN, mclust, goft

Visualização de Dados: corrplot, corrr, igraph, ggraph, ggplot2, factoextra

Relatórios e Tabelas: gt

🧠 Resultados e Aplicabilidade em IA (Insights)
1. Redução de Dimensionalidade e Extração de Features
O Critério de Kaiser-Guttman indicou a retenção de 2 fatores, que juntos explicam 84,70% da variância total do sistema. Isso significa que conseguimos comprimir quase 85% da informação original de 7 variáveis em apenas 2 dimensões latentes, um passo crucial para algoritmos de clusterização ou classificação.

2. Interpretação de Fatores (Feature Importance)
A aplicação da rotação Varimax permitiu separar os atributos em duas grandes frentes:

Fator 1 (Atributos Sensoriais): Fortemente associado a COLOR, AROMA e TASTE.

Fator 2 (Atributos Quantitativos/Custo): Fortemente associado a COST, SIZE e ALCOHOL.

A variável REPUTATION apresentou cargas cruzadas, indicando multicolinearidade complexa com ambos os fatores, o que justificou sua exclusão em um modelo secundário para maximizar a pureza dos dados.

3. Refinamento do Modelo (Feature Selection)
Após a exclusão da variável REPUTATION, o modelo otimizado apresentou um salto na variância explicada conjunta, atingindo 91,23%. Esse processo simula o que fazemos em algoritmos de Feature Selection no Aprendizado de Máquina: remover ruídos ou variáveis complexas para aumentar a acurácia e a estabilidade do modelo.

📁 Estrutura do Repositório
Analise_Fatorial.Rmd: Script documentado em R Markdown contendo todo o pipeline de análise, geração de tabelas (gt) e gráficos.

AnaFatBeer.txt: Base de dados original (200 observações x 7 variáveis).

README.md: Documentação e contextualização do projeto.

🚀 Conclusão para a Banca
Este estudo transcende a estatística descritiva tradicional ao aplicar um rigoroso processo de redução de dimensionalidade. A metodologia adotada (limpeza, testes de premissas, extração de fatores latentes e refinamento iterativo) espelha o fluxo de trabalho essencial de um Cientista de Dados ou Engenheiro de Machine Learning ao preparar dados não estruturados ou altamente correlacionados para a ingestão em modelos de Inteligência Artificial. A extração de escores fatoriais (via método de Bartlett) demonstra a capacidade de transformar dados brutos em features otimizadas para futuras tomadas de decisão baseadas em dados (Data-Driven Decisions).
