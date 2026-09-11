# Dicionário de Dados Exportação de Cargas, Porto de Santos (2005 - 2026)

Dicionário descritivo elaborado a partir da estrutura e dos valores observados no arquivo `exportacao_cargas_pi3.csv`.

## Convenções adotadas

- Base analisada: **1.097.014 registros** e **16 variáveis**.
- A coluna **classe R** descreve a classe conceitualmente adequada para uso em R, sem executar conversões na base original.
- A coluna **tipo de variável** segue a classificação estatística vista em aula: **qualitativa (nominal ou ordinal)** e **quantitativa (discreta ou contínua)**. Variáveis que funcionam como identificador ou como referência temporal derivada são marcadas à parte, por não se enquadrarem nessa dicotomia.
- `TOTAL_TONELADAS` usa vírgula como separador decimal na base original; nenhuma conversão é realizada aqui.
- Não foram observados valores ausentes em nenhuma das 16 variáveis.

## Identificação e viagem

| Variável | Classe R | Tipo de variável | Explicação | Formato/domínio | Ausência |
|---|---|---|---|---|---|
| `NUMERO_VIAGEM` | `character` | Identificador (não se aplica a qualitativa/quantitativa) | Número da viagem do navio à qual o registro de carga pertence. | código numérico; 1 a 6227 | Sem valores ausentes observados |
| `TIPO_NAVEGACAO` | `character` | Qualitativa nominal | Classifica a navegação da viagem quanto à origem/destino. | categoria; CABOTAGEM \| LONGO CURSO | Sem valores ausentes observados |
| `SENTIDO` | `character` | Qualitativa nominal | Sentido do movimento da carga em relação ao navio. | categoria; DESEMBARQUE \| EMBARQUE \| MOVIMENTO A BORDO | Sem valores ausentes observados |
| `MOVIMENTO` | `character` | Qualitativa nominal | Tipo de operação de movimentação registrada. | categoria; CONTRABORDO \| CONVENCIONAL \| MALOGRO \| REMOÇÃO \| TRANSBORDO | Sem valores ausentes observados |

## Embarcação

| Variável | Classe R | Tipo de variável | Explicação | Formato/domínio | Ausência |
|---|---|---|---|---|---|
| `CLASSENAVIO` | `character` | Qualitativa nominal | Classe/tipo da embarcação responsável pela viagem. | categoria; 17 valores (ex.: PORTA-CONTAINERS, GRANELEIRO, PETROLEIRO, TANKER...) | Sem valores ausentes observados |

## Tempo

| Variável | Classe R | Tipo de variável | Explicação | Formato/domínio | Ausência |
|---|---|---|---|---|---|
| `ANO` | `integer` | Quantitativa discreta | Ano de referência da movimentação. | AAAA; 2005 a 2026 | Sem valores ausentes observados |
| `MES` | `character` | Qualitativa ordinal | Mês de referência da movimentação, com dois dígitos. | MM; 01 a 12 | Sem valores ausentes observados |
| `ANO_MES` | `Date` | Temporal derivada (não se aplica a qualitativa/quantitativa) | Competência mensal da movimentação, já consolidada no primeiro dia do mês. | AAAA-MM-01 | Sem valores ausentes observados |

## Localização e infraestrutura portuária

| Variável | Classe R | Tipo de variável | Explicação | Formato/domínio | Ausência |
|---|---|---|---|---|---|
| `TERMINAIS` | `character` | Qualitativa nominal | Terminal portuário onde a movimentação ocorreu. | categoria; 72 valores (ex.: BTP, SANTOS BRASIL, ADM, BUNGE...) | Sem valores ausentes observados |
| `TIPO_INSTALACAO` | `character` | Qualitativa nominal | Natureza jurídico-administrativa da instalação portuária. | categoria; OUTROS \| PORTO ORGANIZADO \| TUP | Sem valores ausentes observados |
| `BERCOS` | `character` | Qualitativa nominal | Berço de atracação onde a movimentação ocorreu. | categoria; 73 valores (ex.: ARM 15, AL 01, AGEO SP...) | Sem valores ausentes observados |

## Carga transportada

| Variável | Classe R | Tipo de variável | Explicação | Formato/domínio | Ausência |
|---|---|---|---|---|---|
| `NATUREZA_CARGA` | `character` | Qualitativa nominal | Categoria geral da carga movimentada. | categoria; CARGA CONTEINERIZADA \| CARGA GERAL \| GRANEL LIQUIDO \| GRANEL SOLIDO | Sem valores ausentes observados |
| `MERCADORIAS` | `character` | Qualitativa nominal | Tipo específico de mercadoria movimentada. | categoria; 67 valores (ex.: AÇÚCAR, CAFÉ, ALGODÃO, CARNE BOVINA...) | Sem valores ausentes observados |

## Medidas de movimentação

| Variável | Classe R | Tipo de variável | Explicação | Formato/domínio | Ausência |
|---|---|---|---|---|---|
| `TOTAL_TEU` | `integer` | Quantitativa discreta | Quantidade total de TEUs (unidade padrão de contêiner) movimentados no registro. | contagem (n); 0 a 5.445 | Sem valores ausentes observados |
| `TOTAL_TONELADAS` | `numeric` | Quantitativa contínua | Peso total da carga movimentada no registro. | toneladas, vírgula decimal; 0 a 397.286 | Sem valores ausentes observados |
| `TOTAL_UNID` | `integer` | Quantitativa discreta | Quantidade total de unidades de carga movimentadas no registro. | contagem (n); 0 a 1.461.627 | Sem valores ausentes observados |

## Perfil descritivo das variáveis

A tabela abaixo registra cardinalidade e ausência observadas, sem qualquer transformação da base.

| Variável | Distintos não ausentes | Ausentes | Ausentes (%) | Valores observados |
|---|---:|---:|---:|---|
| `NUMERO_VIAGEM` | 6222 | 0 | 0,00 | Ex.: 4659 \| 3888 \| 4731 \| 4646 \| 5010 \| 4856 |
| `TIPO_NAVEGACAO` | 2 | 0 | 0,00 | CABOTAGEM \| LONGO CURSO |
| `SENTIDO` | 3 | 0 | 0,00 | DESEMBARQUE \| EMBARQUE \| MOVIMENTO A BORDO |
| `MOVIMENTO` | 5 | 0 | 0,00 | CONTRABORDO \| CONVENCIONAL \| MALOGRO \| REMOÇÃO \| TRANSBORDO |
| `CLASSENAVIO` | 17 | 0 | 0,00 | BALSA \| BARCAÇA \| CARGUEIRO COMUM \| CHATA \| DRAGA \| EMBARCACAO DE APOIO \| FRIGORIFICO \| GAS LIQUEFEITO \| GRANELEIRO \| OUTROS \| PETROLEIRO \| PORTA-CONTAINERS \| QUIMICO \| REBOCADOR EMPURRADOR \| ROLL-ON/ROLL-OFF \| TANKER \| TANQUE |
| `ANO` | 22 | 0 | 0,00 | 2005 \| 2006 \| 2007 \| ... \| 2024 \| 2025 \| 2026 |
| `MES` | 12 | 0 | 0,00 | 01 \| 02 \| 03 \| 04 \| 05 \| 06 \| 07 \| 08 \| 09 \| 10 \| 11 \| 12 |
| `ANO_MES` | 258 | 0 | 0,00 | Ex.: 2005-01-01 \| 2005-02-01 \| 2005-03-01 \| 2005-04-01 \| 2005-05-01 \| 2005-06-01 |
| `TERMINAIS` | 72 | 0 | 0,00 | Ex.: ACT (ARM 38) \| ADM \| ADONAI \| AGEO \| AGEO LESTE \| AGEO NORTE - COPAPE |
| `TIPO_INSTALACAO` | 3 | 0 | 0,00 | OUTROS \| PORTO ORGANIZADO \| TUP |
| `BERCOS` | 73 | 0 | 0,00 | Ex.: ABASTECIMENTO \| AGEO 1 \| AGEO SP \| AL 01 \| AL 02 \| AL 03 |
| `NATUREZA_CARGA` | 4 | 0 | 0,00 | CARGA CONTEINERIZADA \| CARGA GERAL \| GRANEL LIQUIDO \| GRANEL SOLIDO |
| `MERCADORIAS` | 67 | 0 | 0,00 | Ex.: ACESSÓRIOS DE VEÍCULOS AUTOMÓVEIS \| ADITIVOS \| ALGODÃO \| AMÔNIA \| ANIMAIS VIVOS \| AÇÚCAR |
| `TOTAL_TEU` | 2791 | 0 | 0,00 | Ex.: 92 \| 28 \| 598 \| 30 \| 317 \| 14 (mín. 0, máx. 5.445) |
| `TOTAL_TONELADAS` | 458745 | 0 | 0,00 | Ex.: 1504,855 \| 190,55 \| 5631,35 \| 596,37 \| 4601,841 \| 276,87 (mín. 0, máx. 397.286) |
| `TOTAL_UNID` | 6057 | 0 | 0,00 | Ex.: 76 \| 14 \| 335 \| 24 \| 227 \| 14 (mín. 0, máx. 1.461.627) |

## Observações específicas

- **`NUMERO_VIAGEM`:** Tratado como identificador, não como medida numérica; um mesmo número de viagem se repete em vários registros, pois uma viagem pode envolver mais de uma movimentação de carga.
- **`ANO_MES`:** Campo derivado temporal já presente na fonte, no formato AAAA-MM-01 (sempre o primeiro dia do mês); não é recalculado neste dicionário.
- **`MES`:** Mantido como `character` para preservar o zero à esquerda, mesma lógica aplicada a `ano_sinistro`/`mes_sinistro` no dicionário de referência.
- **`TOTAL_TONELADAS`:** No arquivo original o separador decimal é vírgula; nenhuma conversão é realizada aqui. Uma parcela dos registros traz o valor sem casas decimais (ex.: `300`, `25`, `417`), o que é mantido como está.
- **`CLASSENAVIO`, `TERMINAIS`, `BERCOS`, `MERCADORIAS`:** Variáveis qualitativas nominais de alta cardinalidade; a tabela de perfil traz apenas amostras dos valores observados, não a lista completa.
- **Registros duplicados:** foram observadas 3 linhas com todos os 16 campos idênticos a outra linha da base (ex.: viagens com `ANO_MES` 2014-10 e 2016-03). Nenhuma remoção foi feita aqui, apenas o registro da ocorrência.
- Este dicionário é descritivo: documenta a estrutura observada na base de exportação de cargas do Porto de Santos, sem limpar, recodificar ou transformar o conteúdo original.
