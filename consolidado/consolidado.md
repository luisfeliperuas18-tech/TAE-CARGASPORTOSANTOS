# Consolidado

## Projeto

**T.A.E. — Porto da Baixada**

## Integrantes

- Lorenzo Ribeiro Louzada
- Arthur Davino
- Luis Felipe Ruas

## Descrição

Este projeto apresenta a organização, o tratamento e a análise estatística de dados relacionados à movimentação de cargas portuárias. As atividades foram desenvolvidas em R, utilizando notebooks Jupyter, e contemplam análise exploratória, regressão logística e regressão linear.

## Arquivos do projeto

### `organizacao-dos-dados-analise-exploratoria.ipynb`

Notebook dedicado à preparação e à exploração inicial dos dados. Entre as atividades realizadas estão:

- verificação e importação do banco de dados;
- conferência das linhas, colunas e variáveis;
- visualização inicial dos registros;
- correção dos tipos das variáveis;
- conversão de variáveis numéricas;
- transformação de categorias em fatores;
- organização das variáveis de mês e data;
- elaboração de resumos estatísticos;
- realização da análise exploratória dos dados.

### `binario.ipynb`

Notebook destinado à construção e à avaliação de um modelo de regressão logística para uma variável de resposta binária. As principais etapas incluem:

- importação e verificação do banco de dados;
- criação da variável de resposta com base na natureza da carga;
- preparação das variáveis explicativas;
- seleção de uma amostra dos dados;
- ajuste do modelo de regressão logística;
- interpretação das razões de chance;
- previsão de probabilidades e classes;
- comparação de limiares de classificação;
- avaliação do modelo por meio da área sob a curva ROC (AUC).

### `regressao-linear-log-breusch-pagan.ipynb`

Notebook voltado à aplicação de modelos de regressão linear e à análise de seus pressupostos. As atividades realizadas incluem:

- importação e preparação dos dados;
- correção das variáveis numéricas;
- criação de um subconjunto para cargas conteinerizadas;
- ajuste de regressão linear simples;
- construção do gráfico com a reta ajustada;
- ajuste de regressão linear múltipla;
- diagnóstico dos resíduos;
- aplicação de transformação logarítmica;
- avaliação da homocedasticidade por meio do teste de Breusch–Pagan.

## Estrutura do repositório

- `codigo/`: contém os notebooks com os códigos e as análises desenvolvidas em R;
- `to-delete/`: armazena temporariamente arquivos destinados à exclusão;
- `consolidado.md`: reúne a descrição e a organização dos materiais do projeto.

## Tecnologias utilizadas

- R;
- Jupyter Notebook;
- métodos de análise exploratória de dados;
- regressão logística;
- regressão linear simples e múltipla;
- teste de Breusch–Pagan;
- curva ROC e AUC.
