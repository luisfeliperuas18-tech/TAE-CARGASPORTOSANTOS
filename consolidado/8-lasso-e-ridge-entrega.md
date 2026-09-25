# Entrega 8 — Regressão Linear, Transformação Log, Breusch-Pagan e Regularização (Lasso/Ridge)

## Projeto

**T.A.E. — Porto da Baixada**

## Integrantes

- Arthur Davino
- Lorenzo Ribeiro Louzada 
- Luis Felipe Ruas

## Notebook

`8_lasso_e_ridge.ipynb`

## Descrição

Notebook dedicado a modelar a relação entre o volume de carga conteinerizada e o peso total transportado, evoluindo de uma regressão linear simples até a regularização com Lasso e Ridge, passando por diagnóstico de resíduos, transformação logarítmica e teste formal de heterocedasticidade.

## Atividades realizadas

- verificação e importação do banco de dados;
- conferência das linhas e colunas;
- correção do tipo de TOTAL_TONELADAS, removendo a vírgula decimal;
- correção de TOTAL_TEU e TOTAL_UNID como variáveis inteiras;
- criação de subconjunto com apenas carga conteinerizada;
- regressão linear simples entre TOTAL_TONELADAS e TOTAL_TEU;
- gráfico de dispersão com a reta ajustada;
- regressão linear múltipla incluindo TOTAL_UNID;
- diagnóstico visual dos resíduos do modelo múltiplo;
- transformação logarítmica de TEU e toneladas;
- regressão com as variáveis em log;
- novo diagnóstico de resíduos e comparação do R² entre o modelo original e o modelo em log;
- teste de Breusch-Pagan no modelo original e no modelo em log;
- seleção das variáveis e amostragem para o modelo de regularização;
- ajuste de Lasso e Ridge com validação cruzada;
- análise da curva de erro (curva em U) e dos preditores que sobreviveram no Lasso;
- comparação do erro de validação cruzada entre Lasso e Ridge.
