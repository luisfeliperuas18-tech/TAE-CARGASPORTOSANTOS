# Consolidado Entrega 1

# Dicionário de Dados: Exportação de Cargas Porto de Santos

## Projeto

**T.A.E. — Porto da Baixada**

## Integrantes

- Lorenzo Ribeiro Louzada
- Arthur Davino
- Luis Felipe Ruas

## Arquivo de Referência

`dicionario_dados_exportacao_cargas_pi3.md`

## Descrição

Documento descritivo que mapeia e classifica todas as variáveis presentes na base de exportação de cargas do Porto de Santos (2005–2026). Este dicionário é o ponto de partida do projeto, estabelecendo a nomenclatura, os tipos estatísticos, os domínios de valores e as características de cada coluna dos dados.

## Estrutura dos Dados

- **Total de registros:** 1.097.014 observações
- **Total de variáveis:** 16 colunas
- **Período coberto:** 2005 a 2026
- **Valores ausentes:** Nenhum detectado em qualquer variável

## Atividades Realizadas

- Classificação de todas as 16 variáveis segundo tipagem estatística: qualitativa (nominal/ordinal) e quantitativa (discreta/contínua);
- Mapeamento de domínios de valores para cada variável (range numérico, categorias, formato de data);
- Identificação de variáveis especiais: identificadores (`NUMERO_VIAGEM`), ordinais (`MES`), temporais derivadas (`ANO_MES`);
- Documentação de convenções de formatação (exemplo: `MES` como character com zero à esquerda; `TOTAL_TONELADAS` com vírgula decimal);
- Análise de cardinalidade e frequência de valores distintos;
- Registro de anomalias observadas (exemplo: 3 registros totalmente duplicados);
- Elaboração de exemplos de valores para referência rápida em análises posteriores.

## Variáveis Principais por Categoria

### Identificação e Viagem (4 variáveis)
- `NUMERO_VIAGEM`: identificador da viagem (6.222 valores distintos)
- `TIPO_NAVEGACAO`: CABOTAGEM ou LONGO CURSO (nominal)
- `SENTIDO`: DESEMBARQUE, EMBARQUE, MOVIMENTO A BORDO (nominal)
- `MOVIMENTO`: CONTRABORDO, CONVENCIONAL, MALOGRO, REMOÇÃO, TRANSBORDO (nominal)

### Embarcação (1 variável)
- `CLASSENAVIO`: 17 tipos de navios (PORTA-CONTAINERS, GRANELEIRO, PETROLEIRO, etc.)

### Tempo (3 variáveis)
- `ANO`: 2005 a 2026 (discreta)
- `MES`: 01 a 12 em formato character (ordinal)
- `ANO_MES`: data derivada no formato AAAA-MM-01 (temporal)

### Localização e Infraestrutura (3 variáveis)
- `TERMINAIS`: 72 terminais portuários distintos
- `TIPO_INSTALACAO`: PORTO ORGANIZADO, TUP ou OUTROS (nominal)
- `BERCOS`: 73 berços de atracação distintos

### Carga Transportada (2 variáveis)
- `NATUREZA_CARGA`: CARGA CONTEINERIZADA, CARGA GERAL, GRANEL LÍQUIDO, GRANEL SÓLIDO (nominal)
- `MERCADORIAS`: 67 tipos de mercadorias específicas (AÇÚCAR, CAFÉ, ALGODÃO, etc.)

### Medidas de Movimentação (3 variáveis)
- `TOTAL_TEU`: quantidade de containers (discreta; 0 a 5.445)
- `TOTAL_TONELADAS`: peso total em toneladas (contínua; 0 a 397.286; com vírgula decimal)
- `TOTAL_UNID`: quantidade de unidades de carga (discreta; 0 a 1.461.627)

## Aprendizados e Decisões de Tipagem

### Identificadores não são medidas
- `NUMERO_VIAGEM` foi tratado como `character` e não como `integer`, pois funciona como rótulo identificador de viagens, não como quantidade mensurável.

### Ordinais precisam de ordem explícita
- `MES` foi mantido como `character` (não convertido para inteiro) para preservar o zero à esquerda (01, 02, ..., 12), essencial para ordenação correta e para manter compatibilidade com padrões temporais.

### Valores decimais com vírgula exigem cuidado
- `TOTAL_TONELADAS` usa vírgula como separador decimal no formato original (ex.: 1.504,855 toneladas). Conversões futuras devem substituir vírgula por ponto antes de transformar para `numeric`.

### Dados sem faltantes é raro
- A ausência completa de valores ausentes em todas as 16 variáveis é uma característica notável e facilita o pré-processamento em etapas subsequentes.

### Duplicação é mínima mas existe
- Foram identificadas 3 linhas totalmente duplicadas. Decisão de limpeza fica para análises futuras conforme o objetivo.

## Relação com Aulas de Teoria do Aprendizado Estatístico

Este dicionário implementa os conceitos da **Aula 2** — Dados e Variáveis:

- ✓ Classificação estatística de cada coluna (qualitativa nominal/ordinal, quantitativa discreta/contínua)
- ✓ Documentação de domínio e formato esperado para cada variável
- ✓ Identificação de tipos R apropriados (`character`, `integer`, `numeric`, `Date`, `factor`, `ordered`)
- ✓ Registro de convenções especiais (separadores decimais, formatação de datas, zero à esquerda)
- ✓ Preparação para a **Entrega 01** (Organização dos Dados e Análise Exploratória)

## Próximas Etapas

Este dicionário serve como referência para:

1. **Entrega 01:** Verificação de tipos e conversão apropriada de variáveis em R
2. **Entrega 02:** Seleção de preditores e criação de variáveis de resposta para regressão logística
3. **Entrega 03:** Análise de pressupostos em regressão linear (homocedasticidade, linearidade)

## Observações Finais

- Este dicionário é **descritivo**, não prescritivo: documenta a estrutura observada sem realizar limpeza, recodificação ou transformação do conteúdo original.
- Funciona como contrato de dados: qualquer análise subsequente deve validar as tipagens contra este documento de referência.
- A compatibilidade com padrões IBGE (códigos UF de 2 dígitos, formato de data ISO) facilita integração com outras bases públicas de dados portuários e regionais.
