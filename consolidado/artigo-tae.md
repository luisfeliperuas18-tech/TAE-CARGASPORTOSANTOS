# Previsão da movimentação de cargas conteinerizadas no Porto de Santos

**Pergunta do trabalho:** Em que medida o ano de movimentação e a categoria da mercadoria contribuem para prever o volume, em toneladas, das cargas conteinerizadas movimentadas no Porto de Santos entre 2005 e 2025, e qual desses fatores apresenta maior relevância preditiva?

**Autores:** Arthur Davino Rizzo (RA 0051352511016); Lorenzo Ribeiro Louzada (RA 0051352511030); Luis Felipe Ruas do Nascimento (RA 0051352511032)

**Instituição:** Fatec Baixada Santista – Rubens Lara  
**Curso:** Tecnologia em Ciência de Dados  
**Disciplina:** Teoria do Aprendizado Estatístico  
**Professor:** Prof. Dr. João Paulo Ferreira de Mello  
**Local e data:** Santos-SP, 23 de outubro de 2026  
**Repositório:** <https://github.com/luisfeliperuas18-tech/TAE-CARGASPORTOSANTOS>

## 1. Introdução

Os portos desempenham papel estratégico nas cadeias logísticas ao conectar os fluxos de mercadorias a diferentes regiões e mercados. No Brasil, fatores como infraestrutura, localização, conexões terrestres e frequência de navios influenciam a escolha e a competitividade dos portos, especialmente no transporte de contêineres. Em estudo sobre o mercado portuário brasileiro, de Souza, Pitombo e Yang (2021) analisaram esses fatores considerando o Porto de Santos entre os portos da região Sudeste.

No Porto de Santos, Cruz e Degobbi (2023) compararam o desempenho operacional de dois terminais de contêineres e discutiram indicadores de produtividade e aspectos de infraestrutura relacionados às operações. Esses estudos mostram a importância de compreender os fatores associados à atividade portuária e à movimentação de cargas conteinerizadas.

Nesse contexto, este artigo investiga se o ano de movimentação e a categoria da mercadoria podem contribuir para prever o volume, em toneladas, das cargas conteinerizadas movimentadas no Porto de Santos entre 2005 e 2025. A variável-alvo (*target*) é `TOTAL_TONELADAS`, e os preditores são `ANO` e `MERCADORIAS`.

## 2. O banco de dados e o problema

Os dados utilizados foram obtidos a partir das bases estatísticas da Autoridade Portuária de Santos (APS), incluindo o Mensário Estatístico e a área de Estatísticas do Porto de Santos. A APS disponibiliza informações de movimentação de cargas e mantém integração com a base operacional portuária (Autoridade Portuária de Santos, 2026a, 2026b).

O arquivo analisado contém 1.097.014 registros e 16 variáveis. Cada linha representa uma movimentação de carga associada a atributos operacionais, como viagem, tipo de navegação, movimento, terminal, berço, natureza da carga, mercadoria, quantidade de TEUs, número de unidades e total de toneladas.

O recorte temporal considera os anos de 2005 a 2025, pois os registros de 2026 ainda representam um período incompleto na base disponível. Para a análise preditiva, o conjunto deve ser filtrado para manter apenas registros de cargas conteinerizadas. As variáveis selecionadas são `ANO` e `MERCADORIAS` como preditores e `TOTAL_TONELADAS` como variável-alvo.

## 3. Pergunta de pesquisa

A pergunta central é: **em que medida o ano de movimentação e a categoria da mercadoria contribuem para prever o volume, em toneladas, das cargas conteinerizadas movimentadas no Porto de Santos entre 2005 e 2025, e qual desses fatores apresenta maior relevância preditiva?**

## 4. Análise descritiva da série histórica disponível

A série anual apresentada no material de origem registra a movimentação total de cargas no Porto de Santos, sem restringir os dados às cargas conteinerizadas. Nessa série, foram movimentadas aproximadamente 73,7 milhões de toneladas em 2005 e 186,5 milhões em 2025, crescimento de 153,1%. A trajetória apresenta oscilações em alguns anos e crescimento expressivo no longo prazo.

> **Nota de escopo:** esses valores descrevem o total de cargas do porto e servem apenas como contexto. Eles não representam ainda a análise filtrada de cargas conteinerizadas nem os resultados de um modelo preditivo.

### Participação acumulada por natureza da carga

| Natureza da carga | Participação (%) |
|---|---:|
| Granel sólido | 48,48 |
| Carga conteinerizada | 32,99 |
| Granel líquido | 13,62 |
| Carga geral | 4,91 |

### Principais mercadorias por tonelagem acumulada

A categoria agregada “Outras Mercadorias” foi desconsiderada no material de origem para destacar produtos identificados individualmente.

| Mercadoria | Milhões de toneladas |
|---|---:|
| Açúcar | 368,4 |
| Soja em grãos | 337,7 |
| Milho | 209,6 |
| Farelo de soja | 104,8 |
| Celulose | 82,6 |

Os resultados descritivos do material de origem mostram a composição geral da movimentação do Porto de Santos no período. A carga conteinerizada correspondeu a 32,99% do volume acumulado, enquanto açúcar, soja em grãos e milho apareceram entre as mercadorias de maior tonelagem total. Esses resultados são contextuais e não identificam, por si só, quais preditores contribuem mais para a previsão de toneladas de cargas conteinerizadas.

## 5. Referências

AUTORIDADE PORTUÁRIA DE SANTOS. *Mensário Estatístico do Porto de Santos*. Santos, SP, 2026. Disponível em: <https://mensario.portodesantos.com.br/>. Acesso em: 2 out. 2026.

AUTORIDADE PORTUÁRIA DE SANTOS. *Estatísticas — Porto de Santos*. 2026. Área de consulta e download de dados de movimentação de cargas e passageiros, integrada à base de movimentação portuária. Disponível em: <https://www.portodesantos.com.br/informacoes-operacionais/estatisticas/>. Acesso em: 2 out. 2026.

CRUZ, Scheilla Maria de Araújo; DEGOBBI, Antonio Fernando. Desempenho operacional de terminais de contêineres no Porto de Santos: estudo comparativo entre um terminal do porto organizado e outro de uso privado. *InGeTec – Inovação, Gestão & Tecnologia*, v. 2, n. 5, p. 79–96, dez. 2023. Disponível em: <https://www.fatecbarueri.edu.br/revista/index.php/ingetec/article/view/105>. Acesso em: 23 out. 2026.

DE SOUZA, Felipe Lobo Umbelino; PITOMBO, Cira Souza; YANG, Dong. Port choice in Brazil: a qualitative research related to in-depth interviews. *Journal of Shipping and Trade*, v. 6, art. 13, 2021. DOI: <https://doi.org/10.1186/s41072-021-00094-2>.

## 6. Pontos a alinhar antes da versão final do artigo

- Filtrar a base para cargas conteinerizadas antes de calcular os resultados apresentados como resultados do estudo.
- A série anual, as participações por natureza de carga e o ranking de mercadorias do material original abrangem todas as naturezas de carga. Manter esses números apenas como contexto ou recalculá-los após o filtro.
- A descrição da base informa 1.097.014 registros totais. Se esse total não for apenas de cargas conteinerizadas, informar também a quantidade de registros após o filtro.
- Incluir a avaliação do modelo preditivo e a medida usada para comparar a relevância de `ANO` e `MERCADORIAS`. Os arquivos enviados ainda não apresentam esses resultados.
