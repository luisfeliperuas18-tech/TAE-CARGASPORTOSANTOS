# Entrega 10 — Amostragem e Distribuições Amostrais

## Projeto

**T.A.E. — Porto da Baixada**

## Integrantes

- Lorenzo Ribeiro Louzada
- Arthur Davino
- Luis Felipe Ruas

## Material

`aula10-amostragem-distribuicoes-amostrais.md`

**Observação:** embora os slides estejam identificados como Aula 9, este conteúdo foi organizado como Aula 10 para diferenciá-lo da aula anterior sobre regressão KNN e suavização por kernel.

## Descrição

Consolidação da aula teórica de Teoria do Aprendizado Estatístico sobre amostragem, distribuições amostrais e introdução à inferência estatística. O material explica como utilizar estatísticas calculadas em uma amostra para estudar características de uma população. Não houve utilização de banco de dados ou execução de código em R nesta atividade.

## Atividades realizadas

- distinção entre população, amostra, parâmetros populacionais e estatísticas amostrais;
- estudo da média amostral como variável aleatória, com esperança igual à média populacional e erro padrão igual a `σ/√n`, sob as condições apresentadas na aula;
- compreensão de como o aumento do tamanho da amostra reduz o erro padrão;
- estudo do Teorema Central do Limite e da aproximação normal para médias amostrais;
- aplicação da aproximação normal à proporção amostral, verificando as condições `np ≥ 5` e `n(1-p) ≥ 5`;
- resolução de dois exercícios numéricos: probabilidades para a média do volume diário de pedidos e para a proporção de pedidos com conferência manual;
- resolução de dois exercícios teóricos: demonstração da esperança e variância da média amostral e dedução do erro padrão da proporção amostral.

## O que foi aprendido

Aprendemos que uma estatística amostral, como a média ou a proporção, varia de uma amostra aleatória para outra e, por isso, possui uma distribuição amostral. A média amostral estima a média da população sem viés nas condições estudadas, enquanto sua dispersão diminui conforme o tamanho da amostra cresce.

O Teorema Central do Limite permite aproximar a distribuição da média amostral por uma distribuição normal quando a amostra é suficientemente grande, conforme a regra prática apresentada no material (`n ≥ 30`). Também aprendemos a padronizar valores com o escore Z e calcular probabilidades associadas à média e à proporção amostrais.

A relação `σ/√n` mostrou que a precisão não cresce na mesma proporção do tamanho da amostra: para reduzir o erro padrão à metade, é necessário quadruplicar o tamanho da amostra. Os exercícios teóricos reforçaram a utilização da linearidade da esperança, da variância de somas independentes e das propriedades da distribuição binomial.

## Relação com a pergunta do artigo

Os conceitos ajudam a fundamentar a interpretação de estatísticas obtidas a partir de amostras de operações de cargas conteinerizadas do Porto de Santos, especialmente quanto à variabilidade das estimativas e à precisão amostral. Entretanto, esta aula, isoladamente, **não identifica quais variáveis contribuem para prever `TOTAL_TONELADAS`**; essa resposta depende das análises preditivas e da comparação dos modelos realizadas nas demais etapas do projeto.
