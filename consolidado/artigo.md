# A pergunta do trabalho: *Quais variáveis da movimentação de cargas conteinerizadas contribuem para a previsão da quantidade de toneladas movimentadas no Porto de Santos?*

Fatec Baixada Santista, Rubens Lara
Tecnologia em Ciência de Dados | Teoria do Aprendizado Estatístico | Prof. Dr. João Paulo Ferreira de Mello

Arthur Davino Rizzo, RA 0051352511016
Lorenzo Ribeiro Louzada, RA 0051352511030
Luis Felipe Ruas do Nascimento, RA 0051352511032

## 1. Introdução

Os portos ocupam posição estratégica nas cadeias logísticas ao concentrar fluxos de mercadorias, infraestrutura e conexões com diferentes regiões. A literatura sobre desenvolvimento portuário mostra que a atuação dos portos ultrapassa os limites físicos do cais e se relaciona com redes logísticas e áreas de influência mais amplas, Notteboom e Rodrigue (2005). Nesse contexto, o Porto de Santos apresenta relevância para o comércio exterior brasileiro e para a movimentação de cargas de diferentes naturezas.

Estudos específicos sobre Santos reforçam a importância de analisar sua movimentação e seus processos operacionais. Komoto (2013) investigou os determinantes da movimentação de contêineres no comércio exterior com foco no Porto de Santos, enquanto Furlan e Pinto (2015) analisaram procedimentos de fronteira críticos na importação de cargas conteinerizadas. Esses trabalhos evidenciam a complexidade da operação portuária e a utilidade de análises quantitativas aplicadas aos dados de movimentação.

Este artigo tem como objetivo analisar a evolução da movimentação de cargas no Porto de Santos entre 2005 e 2025 e identificar quais naturezas de carga e mercadorias apresentaram maior participação no volume total movimentado.

## 2. O banco de dados e o problema

Os dados utilizados foram obtidos a partir das bases estatísticas da Autoridade Portuária de Santos (APS), incluindo o Mensário Estatístico e a área de Estatísticas do Porto de Santos. A APS disponibiliza informações de movimentação de cargas e mantém integração com a base operacional portuária, Autoridade Portuária de Santos (2026a, 2026b).

O arquivo analisado contém 1.097.014 registros e 16 variáveis. Cada linha representa uma movimentação de carga associada a atributos operacionais, como viagem, tipo de navegação, movimento, terminal, berço, natureza da carga, mercadoria, quantidade de TEUs, número de unidades e total de toneladas.

Para manter o artigo compatível com o limite de três páginas, foram selecionadas quatro variáveis centrais: `ANO`, `TOTAL_TONELADAS`, `NATUREZA_CARGA` e `MERCADORIAS`. O recorte temporal considera 2005 a 2025, pois os registros de 2026 ainda representam um período incompleto na base disponível.

## 3. A pergunta

A pergunta central é: *como a movimentação de cargas no Porto de Santos evoluiu entre 2005 e 2025 e quais tipos de carga e mercadorias concentraram o maior volume em toneladas?*

A Figura 1 apresenta a soma anual de `TOTAL_TONELADAS`. Em 2005, foram registrados aproximadamente 73,7 milhões de toneladas. Em 2025, o valor alcançou aproximadamente 186,5 milhões de toneladas, correspondendo a um crescimento de 153,1% no período.

![Figura 1, Movimentação anual de cargas no Porto de Santos, 2005 a 2025](figura1-1.png)

*Figura 1, Movimentação anual de cargas no Porto de Santos, 2005 a 2025. Fonte: elaborada pelos autores a partir dos dados da APS.*

Embora a trajetória apresente oscilações em alguns anos, observa-se crescimento expressivo no longo prazo. O aumento do volume movimentado confirma a relevância de acompanhar séries históricas e a composição das cargas como instrumento de análise do desempenho portuário.

## 4. Defesa da pergunta

A composição acumulada entre 2005 e 2025 mostra predominância do *granel sólido*, com aproximadamente 48,48% das toneladas movimentadas. A *carga conteinerizada* aparece em seguida, com 32,99%, enquanto o *granel líquido* representa 13,62% e a *carga geral*, 4,91%.

**Tabela 1, Participação acumulada por natureza da carga, 2005 a 2025**

| Natureza da carga | Participação (%) |
|---|---:|
| Granel sólido | 48,48 |
| Carga conteinerizada | 32,99 |
| Granel líquido | 13,62 |
| Carga geral | 4,91 |

*Fonte: elaborada pelos autores a partir dos dados da APS.*

Na análise das mercadorias, a categoria agregada "Outras Mercadorias" foi desconsiderada para destacar produtos identificados individualmente. Açúcar, soja em grãos e milho apresentaram os maiores volumes acumulados, seguidos por farelo de soja e celulose.

**Tabela 2, Principais mercadorias identificadas por tonelagem acumulada, 2005 a 2025**

| Mercadoria | Milhões de toneladas |
|---|---:|
| Açúcar | 368,4 |
| Soja em grãos | 337,7 |
| Milho | 209,6 |
| Farelo de soja | 104,8 |
| Celulose | 82,6 |

*Fonte: elaborada pelos autores a partir dos dados da APS.*

Os resultados sustentam a pergunta proposta ao mostrar, de forma simultânea, a evolução do volume total e a composição da movimentação. O crescimento observado ao longo da série histórica é acompanhado por forte participação de granéis sólidos e de cargas conteinerizadas. A presença de açúcar, soja e milho entre as mercadorias de maior tonelagem também evidencia a importância de produtos ligados ao agronegócio na composição da movimentação analisada.

A análise é descritiva e, portanto, não busca estabelecer relações causais. Ainda assim, o recorte permite sintetizar a evolução e a estrutura da movimentação do Porto de Santos com base em dados oficiais, complementando a literatura que discute tanto a dinâmica portuária quanto aspectos específicos das operações e da movimentação de contêineres em Santos, Notteboom e Rodrigue (2005), Komoto (2013), Furlan e Pinto (2015).

## Referências Bibliográficas

AUTORIDADE PORTUÁRIA DE SANTOS. *Estatísticas, Porto de Santos*. 2026. Área de consulta e download de dados de movimentação de cargas e passageiros, integrada à base de movimentação portuária. Disponível em: <https://www.portodesantos.com.br/informacoes-operacionais/estatisticas/>. Acesso em: 2 out. 2026.

AUTORIDADE PORTUÁRIA DE SANTOS. *Mensário Estatístico do Porto de Santos*. Santos, SP: [s.n.], 2026. Disponível em: <https://mensario.portodesantos.com.br/>. Acesso em: 2 out. 2026.

FURLAN, P. K.; PINTO, M. M. d. O. Identificação dos procedimentos de fronteira críticos na importação de cargas conteinerizadas: estudo do porto de santos. *Production*, v. 25, n. 1, p. 183 a 189, 2015.

KOMOTO, N. T. G. *Determinantes da movimentação de contêineres no comércio exterior: estudo de caso do Porto de Santos*. Dissertação (Mestrado em Economia), Universidade Federal de Santa Catarina, Florianópolis, 2013.

NOTTEBOOM, T. E.; RODRIGUE, J.-P. Port regionalization: towards a new phase in port development. *Maritime Policy & Management*, v. 32, n. 3, p. 297 a 313, 2005.
