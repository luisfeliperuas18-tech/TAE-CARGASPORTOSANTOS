# # Consolidado Entrega 8 - Reta, Knn, Kernel e Cv5

## Projeto

**T.A.E. — Porto da Baixada**

## Integrantes

- Arthur Davino
- Lorenzo Ribeiro Louzada 
- Luis Felipe Ruas

## Notebook

`9-reta-knn-kernel-cv5.ipynb`

## Descrição

Este documento apresenta o resumo da análise e modelagem estatística realizada sobre o banco de dados de cargas conteinerizadas no Porto de Santos[cite: 229].

## 1. Visão Geral e Preparação dos Dados
* O banco de dados original continha **1.097.014 observações** e **16 variáveis**[cite: 229].
* Foram filtrados apenas os registros com a natureza de carga **"CARGA CONTEINERIZADA"**, resultando em **978.320 observações** válidas[cite: 229].
* As variáveis numéricas (`TOTAL_TONELADAS`, `TOTAL_TEU`, `TOTAL_UNID`, `ANO`, `MES`) foram tratadas, convertidas e limpas para remover inconsistências ou valores ausentes[cite: 229].

## 2. Divisão do Conjunto de Dados
Para avaliar o desempenho preditivo dos modelos, os dados foram divididos em duas partes utilizando uma proporção de 70/30:
* **Conjunto de Treino:** 684.824 observações[cite: 229].
* **Conjunto de Teste:** 293.496 observações[cite: 229].

## 3. Modelagem Preditiva com Regressão Linear
Foram testados três modelos com complexidade crescente utilizando a transformação logarítmica (`log1p`) na variável resposta (`TOTAL_TONELADAS`) e em algumas preditoras[cite: 229]:
* **Modelo 1:** Apenas `TOTAL_TEU` ($R^2$ ajustado = $0,8335$)[cite: 229].
* **Modelo 2:** `TOTAL_TEU` + `TOTAL_UNID` ($R^2$ ajustado = $0,8462$)[cite: 229].
* **Modelo 3:** `TOTAL_TEU` + `TOTAL_UNID` + `ANO` + `MES` ($R^2$ ajustado = $0,8475$)[cite: 229].

## 4. Comparação de Erros (RMSE) no Conjunto de Teste
O erro de previsão foi medido pelo Erro Quadrático Médio da Raiz (**RMSE**) na escala original de toneladas[cite: 229]:
* **TEU:** 1.201,643 toneladas[cite: 229].
* **TEU + Unidades:** 1.183,662 toneladas[cite: 229].
* **TEU + Unidades + Tempo (Ano e Mês):** 1.188,740 toneladas[cite: 229].

## 5. Conclusão
* O **Modelo 2** (incluindo `TOTAL_TEU` e `TOTAL_UNID`) apresentou o melhor desempenho geral, obtendo o menor **RMSE (1.183,66 toneladas)** no conjunto de teste e um excelente equilíbrio entre precisão e simplicidade[cite: 229].
* A inclusão de variáveis temporais (`ANO` e `MES`) não melhorou significativamente a capacidade preditiva em dados de teste, indicando que o volume físico (`TEU` e unidades movimentadas) detém o principal poder explicativo para o peso da carga conteinerizada analisada[cite: 229].
