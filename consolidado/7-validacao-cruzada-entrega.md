# Consolidado Entrega 7 — Validação Cruzada e Bootstrap

## Projeto

**T.A.E. — Porto da Baixada**

## Integrantes

- Arthur Davino
- Lorenzo Ribeiro Louzada 
- Luis Felipe Ruas

## Notebook

`7_validacao_cruzada.ipynb`

## Descrição

Notebook dedicado a comparar dois modelos de regressão sobre o volume de carga conteinerizada usando validação cruzada de 5 partes, e a estimar a incerteza do coeficiente do modelo escolhido por meio de bootstrap.

## Atividades realizadas

- carregamento e conferência do banco de dados;
- seleção apenas da carga conteinerizada;
- seleção das três variáveis necessárias (TOTAL_TONELADAS, TOTAL_TEU, TOTAL_UNID);
- conversão das variáveis para numérico e remoção de valores inválidos;
- amostragem de 50.000 registros;
- ajuste de um modelo de regressão simples e de um modelo de regressão múltipla;
- implementação de uma função de validação cruzada em 5 partes (k-fold);
- cálculo do erro de validação cruzada dos dois modelos e comparação entre eles;
- escolha do modelo com menor erro de validação cruzada;
- bootstrap com 2.000 réplicas do coeficiente de TOTAL_TEU no modelo escolhido;
- cálculo do erro padrão e do intervalo de confiança de 95% via bootstrap;
- interpretação do intervalo de confiança;
- gráfico do histograma do bootstrap.
