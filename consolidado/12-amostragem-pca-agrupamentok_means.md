# Entrega TAE, Aula 12: Amostragem, PCA e Agrupamento (K means)

## Descrição

Aula 12 de Teoria do Aprendizado Estatístico, sobre aprendizado sem supervisão aplicado ao banco do projeto Porto da Baixada. Ela junta três ideias: trabalhar com uma amostra aleatória quando a base inteira é grande demais para o método (amostragem), resumir variáveis correlacionadas em poucos eixos (PCA, análise de componentes principais) e separar as observações em grupos parecidos entre si (agrupamento por K means, com o número de grupos K escolhido pela silhueta).

O laboratório foi feito no banco de movimentação de cargas, só com carga conteinerizada, e ligado à pergunta do projeto: "Quais variáveis da movimentação de cargas conteinerizadas contribuem para a previsão da quantidade de toneladas movimentadas no Porto de Santos?". A pergunta específica do notebook é se um agrupamento feito sem olhar para as toneladas descobre algo sobre as toneladas, e se o grupo encontrado serve de preditor.

## Principais etapas

1. Base e filtro. A base tem 1.097.014 linhas e 16 colunas. Ficando só com `NATUREZA_CARGA == "CARGA CONTEINERIZADA"`, restam 978.320 registros.

2. Preparação das variáveis. As colunas `TOTAL_TONELADAS`, `TOTAL_TEU`, `TOTAL_UNID`, `ANO` e `MES` foram convertidas para número (trocando a vírgula decimal por ponto), e só ficaram registros completos e sem valor negativo. Nenhum registro saiu nesse passo (978.320 antes e depois). A resposta Y é `TOTAL_TONELADAS`; os preditores X são `TOTAL_TEU`, `TOTAL_UNID`, `ANO` e `MES`.

3. Amostra de 2.000 registros. O K means e a silhueta precisam da matriz de distâncias entre todos os pares de observações. Com 978.320 registros seriam quase 480 bilhões de pares, o que não cabe na memória; com 2.000 são cerca de 2 milhões. A amostra é aleatória simples, feita com `sample()` e `set.seed(1)` para o resultado se reproduzir. Pelo que se viu na aula de distribuições amostrais, uma amostra aleatória grande reproduz a base com um erro que cai com a raiz de n, então o que se conclui na amostra vale, com incerteza, para a base inteira.

4. Transformação e padronização. `TOTAL_TEU` e `TOTAL_UNID` têm dispersão enorme (o TEU vai de 1 a 5.445, com mediana 11), então entram em `log1p`. Depois as quatro variáveis são padronizadas com `scale()` (média 0 e desvio padrão 1). Sem isso, a variável de maior escala mandaria sozinha nas distâncias e no PCA. A matriz de distâncias D é calculada sobre as variáveis padronizadas.

5. PCA. Feito com `prcomp(X, scale. = TRUE)`.

| Componente | Desvio padrão | Variância explicada | Acumulada |
|---|---|---|---|
| PC1 | 1,416 | 50,1% | 50,1% |
| PC2 | 1,000 | 25,0% | 75,1% |
| PC3 | 0,992 | 24,6% | 99,7% |
| PC4 | 0,104 | 0,3% | 100% |

Pesos das variáveis nos dois primeiros componentes:

| Variável | PC1 | PC2 |
|---|---|---|
| TOTAL_TEU | 0,702 | 0,013 |
| TOTAL_UNID | 0,702 | 0,016 |
| ANO | 0,120 | −0,220 |
| MES | −0,007 | −0,975 |

6. Escolha de K pela silhueta. Para K de 2 a 8, rodamos o K means (`nstart = 25`) e calculamos a silhueta média. A silhueta de cada ponto mede o quanto ele está mais perto do próprio grupo do que do grupo vizinho; quanto mais perto de 1, melhor.

| K | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|
| Silhueta | 0,331 | 0,268 | 0,271 | 0,269 | 0,272 | 0,268 | 0,273 |

O maior valor é o de K = 2, escolhido pelo código com `which.max`.

7. Agrupamento final. K means com K = 2, `nstart = 25` e semente 1. O grupo 1 ficou com 715 registros e o grupo 2 com 1.285.

8. Centros dos grupos nas unidades originais (média de cada variável por grupo).

| Grupo | TOTAL_TEU | TOTAL_UNID | ANO | MES |
|---|---|---|---|---|
| 1 | 207,81 | 126,90 | 2016,31 | 6,42 |
| 2 | 6,80 | 4,76 | 2015,16 | 6,55 |

9. Gráficos. O plano PC1 por PC2 com os pontos coloridos pelo grupo, e dois gráficos de toneladas por grupo (boxplot e barras da mediana).

10. Toneladas por grupo. As toneladas não entraram no agrupamento.

| Grupo | Média de toneladas | Mediana de toneladas |
|---|---|---|
| 1 | 2.179,4 | 951,7 |
| 2 | 100,2 | 58,2 |

11. O grupo vira preditor? Dois modelos lineares para `log1p(TOTAL_TONELADAS)`, um com `log1p(TOTAL_TEU) + log1p(TOTAL_UNID) + ANO + MES` e outro com o grupo a mais.

| Modelo | R² |
|---|---|
| Sem grupo | 0,8467 |
| Com grupo | 0,8469 |

Código central do laboratório:

```r
# amostra de 2.000 registros
set.seed(1)
d <- dados_reg[sample(seq_len(nrow(dados_reg)), 2000), ]

# log nas variáveis muito dispersas, padronização e distâncias
X <- data.frame(TOTAL_TEU = log1p(d$TOTAL_TEU), TOTAL_UNID = log1p(d$TOTAL_UNID),
                ANO = d$ANO, MES = d$MES)
Z <- scale(X)
D <- dist(Z)

# PCA
pca <- prcomp(X, scale. = TRUE)
summary(pca)
round(pca$rotation[, 1:2], 3)

# silhueta para K de 2 a 8
ks <- 2:8
set.seed(1)
S <- sapply(ks, function(k) {
  modelo <- kmeans(Z, centers = k, nstart = 25)
  mean(silhouette(modelo$cluster, D)[, 3])
})
K <- ks[which.max(S)]

# agrupamento final e toneladas por grupo
set.seed(1)
km <- kmeans(Z, centers = K, nstart = 25)
d$grupo <- factor(km$cluster)
aggregate(TOTAL_TONELADAS ~ grupo, data = d, FUN = mean)
aggregate(TOTAL_TONELADAS ~ grupo, data = d, FUN = median)

# o grupo ajuda a prever?
m0 <- lm(log1p(TOTAL_TONELADAS) ~ log1p(TOTAL_TEU) + log1p(TOTAL_UNID) + ANO + MES, data = d)
m1 <- update(m0, . ~ . + grupo)
c(sem = summary(m0)$r.squared, com = summary(m1)$r.squared)
```

## Leitura dos resultados

O PCA mostra três eixos quase independentes. O PC1 (50,1%) é o tamanho da operação: TEU e UNID entram com o mesmo peso e andam juntas. O PC2 (25,0%) é praticamente só o mês, e o PC3 (24,6%) fica com o que sobra, em especial o ano. O PC4 tem só 0,3% da variância, o que confirma que TEU e UNID carregam quase a mesma informação, como já se tinha visto na Aula 10, em que as duas eram redundantes no GAM.

A silhueta escolheu K = 2 com 0,331, contra valores em torno de 0,27 para K de 3 a 8. Pela regra prática usual (Kaufman e Rousseeuw), valores entre 0,26 e 0,50 indicam estrutura fraca, que pode ser artificial. Ou seja, o agrupamento corta um contínuo em dois pedaços, e não revela blocos bem separados. A curva quase plana de K = 3 em diante também diz que não existe um número natural de grupos além de dois.

Os dois grupos separam só por tamanho: o grupo 1 reúne as operações grandes (cerca de 208 TEU e 127 unidades em média) e o grupo 2 as pequenas (cerca de 7 TEU e 5 unidades). Ano e mês são praticamente iguais nos dois (2016,3 contra 2015,2 no ano, 6,4 contra 6,6 no mês), então o calendário não ajudou a formar os grupos.

Mesmo sem ter visto as toneladas, os grupos diferem muito nelas: a média do grupo grande é cerca de 22 vezes a do pequeno (2.179,4 contra 100,2) e a mediana cerca de 16 vezes (951,7 contra 58,2). Nos dois grupos a média fica acima da mediana, o que indica assimetria à direita. Os dois grupos têm n bem acima de 30 (715 e 1.285), então a regra do TCL se cumpre para a média amostral, mas com essa cauda longa a mediana descreve melhor a operação típica.

O grupo não vira preditor. O R² vai de 0,8467 para 0,8469, um ganho de 0,00015. Isso era esperado, porque o grupo foi construído a partir de TEU e UNID, que já estão no modelo: ele só resume de forma categórica o que o modelo já recebe de forma contínua.

## Ligação com a pergunta do projeto

Para "quais variáveis contribuem para prever toneladas", o que este laboratório mostra é que o tamanho da operação (`TOTAL_TEU` e `TOTAL_UNID`, que são a mesma informação) é o eixo que organiza os dados e separa grupos com toneladas muito diferentes. Ano e mês não ajudaram a separar os grupos, e o efeito deles sobre as toneladas não foi testado diretamente aqui. Isso é coerente com a Aula 10, em que o ANO foi o primeiro a ser dispensado no GAM. A ficha da pergunta não muda: o agrupamento é uma exploração, e o modelo que responde à pergunta continua sendo o de regressão, validado por validação cruzada.

## Cuidados e limites

1. O R² dos dois modelos é calculado nos mesmos dados do ajuste, sem validação cruzada. A diferença de 0,00015 é pequena demais para qualquer conclusão além de "o grupo não acrescenta nada".
2. Tudo vem de uma única amostra de 2.000 registros com semente 1. Outra semente pode mudar os tamanhos dos grupos e a silhueta, ainda que o desenho geral (tamanho separando os grupos) deva se repetir.
3. O ANO inclui 2026, que é um ano incompleto na base.
4. O K means foi rodado com as quatro variáveis padronizadas, então duas das quatro dimensões (ano e mês) são calendário e entram com o mesmo peso que o tamanho. Uma variação a testar, sem resultado ainda, é repetir o agrupamento só com TEU e UNID e ver se a silhueta sobe.
5. O K means supõe grupos mais ou menos esféricos e é sensível à escala; por isso a padronização e o `log1p` antes das distâncias.

## O que foi aprendido

Aprendizado sem supervisão é achar estrutura nos preditores sem usar a resposta. Aqui a resposta (toneladas) ficou fora do PCA e do agrupamento e só foi usada depois, para checar se a estrutura encontrada significava algo. Significou, mas só porque tamanho da operação e toneladas andam juntas, e não por algum padrão novo.

O PCA só comprime quando as variáveis são correlacionadas. Das quatro variáveis, só TEU e UNID são, e por isso o PC1 resume duas em uma sem perder quase nada. Ano e mês, sendo independentes das outras, ficaram cada um com um eixo próprio de desvio padrão em torno de 1, que é o mesmo que uma variável padronizada original: nesses eixos o PCA não resume nada. Por isso os "75% em dois componentes" enganam um pouco, já que o PC2 é só o mês.

A silhueta serve para escolher K, mas também para medir se o agrupamento é convincente. Escolher o K de maior silhueta sempre devolve algum K; o valor absoluto (0,33) é que diz se há estrutura de verdade, e aqui há pouca.

Por fim, um grupo construído a partir das variáveis do modelo não é preditor novo. Para um agrupamento ajudar a prever, ele precisaria trazer informação que o modelo ainda não tem, por exemplo vindo de variáveis que não estão na regressão.
