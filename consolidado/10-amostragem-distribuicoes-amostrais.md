# Entrega TAE - Amostragem e Distribuições Amostrais

Observação: o slide da aula está rotulado "Aula 9", mas o conteúdo (amostragem, distribuição amostral da média e do Teorema Central do Limite) é diferente do que já foi tratado como aula 9 neste curso (o laboratório de KNN-regressão e kernel smoothing). Pelo encadeamento do material, essa é a aula seguinte àquela, só com a numeração do slide desatualizada.

## Descrição

Aula teórica de Teoria do Aprendizado Estatístico sobre o bloco 2 do curso: inferência estatística. O foco é inverter a pergunta do bloco 1 (conhecendo o modelo, o que esperar dos dados) para a pergunta do bloco 2 (conhecendo os dados, o que dizer da população). Os pilares apresentados são população x amostra, a média amostral como variável aleatória, o erro padrão (sigma sobre raiz de n) e o Teorema Central do Limite, que garante que a média amostral se aproxima de uma normal mesmo quando a população não é normal, desde que n seja grande (regra prática do curso, n maior ou igual a 30). O mesmo resultado é estendido para a proporção amostral. Não há base de dados nem código R envolvido, a aula é toda analítica, fechando com 4 exercícios (2 de cálculo numérico, 2 de demonstração teórica).

## Principais etapas

Revisão do vocabulário da inferência: parâmetro (grego, fixo e desconhecido, pertence à população) versus estatística (latino, calculável, pertence à amostra). Exemplos: média populacional mu versus média amostral x-barra, desvio-padrão sigma versus s, proporção p versus p-chapéu.

Apresentação do teorema central do bloco: se X1,...,Xn é uma amostra aleatória de uma população com média mu e desvio-padrão sigma, então E(X-barra) = mu (a média amostral não tem viés) e DP(X-barra) = sigma/raiz de n (o erro padrão). A consequência prática é que a precisão cresce com a raiz de n, não com n: para dobrar a precisão é preciso quadruplicar a amostra.

Apresentação do Teorema Central do Limite: para n grande (regra prática, n maior ou igual a 30), X-barra se aproxima de uma Normal(mu, sigma²/n), qualquer que seja a forma da população. O mesmo raciocínio vale para somas de parcelas independentes (por isso pesos de carga consolidados e tempos somados tendem a ficar normais) e para a proporção amostral p-chapéu, que se aproxima de uma Normal(p, p(1-p)/n) quando np e n(1-p) são maiores ou iguais a 5.

Resolução dos 4 exercícios propostos ao final da aula, descritos a seguir.

Exercício de cálculo 1, volume diário de pedidos (mu = 80, sigma = 15, n = 36 dias):
a) como n = 36 é maior que 30, vale o TCL: X-barra aproximadamente Normal(80, 6,25), com erro padrão sigma/raiz de n = 15/6 = 2,5.
b) P(X-barra < 75): z = (75-80)/2,5 = -2, logo P = 0,0228.
c) P(78 < X-barra < 84): z1 = -0,8 e z2 = 1,6, logo P = Phi(1,6) - Phi(-0,8) = 0,9452 - 0,2119 = 0,7333.
d) o teorema usado é o Central do Limite, válido porque a amostra é grande o suficiente (n maior ou igual a 30) para que X-barra se comporte como normal mesmo sem conhecer a distribuição exata do volume diário de pedidos.

Exercício de cálculo 2, proporção de pedidos com conferência manual (p = 0,20, n = 100):
condição para a normal valer, np = 20 e n(1-p) = 80, os dois maiores que 5. p-chapéu aproximadamente Normal(0,20; 0,0016), com DP(p-chapéu) = 0,04. P(p-chapéu menor ou igual a 0,26): z = (0,26-0,20)/0,04 = 1,5, logo P = 0,9332.

Exercício teórico 1, centro e dispersão de X-barra: a partir de X-barra = (X1+...+Xn)/n, mostrado que E(X-barra) = mu usando só a linearidade da esperança (vale mesmo sem independência) e que Var(X-barra) = sigma²/n usando a independência das Xi para eliminar os termos de covariância na variância da soma, restando Var(soma das Xi) = n vezes sigma².

Exercício teórico 2, erro padrão da proporção: a partir de p-chapéu = X/n com X seguindo Binomial(n,p), usando E(X) = np e Var(X) = np(1-p), deduzido que E(p-chapéu) = p e DP(p-chapéu) = raiz de p(1-p)/n.

## O que foi aprendido

A virada conceitual do semestre: a mesma estatística que no primeiro semestre só resumia dados observados (uma média, uma proporção) passa a ser tratada como variável aleatória, com distribuição, esperança e desvio-padrão próprios, porque seu valor depende de qual amostra aleatória calhou de ser sorteada. É isso que permite fazer uma pergunta de probabilidade sobre o quanto x-barra pode errar ao estimar mu, em vez de só reportar o valor observado.

O Teorema Central do Limite é o que viabiliza essa inferência na prática: não é preciso conhecer a distribuição da população para saber como a média amostral se comporta, basta ter uma amostra razoavelmente grande. A mesma lógica explica por que somas de parcelas independentes (pesos consolidados, tempos de operação, erros de medida) tendem a ficar normais, e por que a própria aproximação normal da binomial (vista antes como caso isolado) é só um caso particular do TCL aplicado a somas de Bernoulli.

Também ficou clara a relação de custo entre precisão e tamanho de amostra: como o erro padrão cai com a raiz de n, ganhar precisão fica cada vez mais caro quanto mais precisão já se tem, o que é exatamente o tipo de conta que depois dimensiona tamanho de amostra para auditorias e pesquisas (apontado como assunto da aula 11).

Por fim, o encadeamento do curso fica mais explícito: os dois exercícios teóricos (centro e dispersão de X-barra, erro padrão da proporção) são extensões diretas de propriedades já demonstradas antes (linearidade da esperança, variância da soma de independentes, média e variância da binomial), reaproveitadas agora para justificar formalmente os resultados que a aula apresenta, e que serão usados sem redemonstração nas aulas seguintes sobre intervalo de confiança e teste de hipótese.
