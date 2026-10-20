# Entrega TAE, Aula 10: Splines e Modelos Aditivos

## Descrição

Aula 10 de Teoria do Aprendizado Estatístico (Prof. Dr. João Paulo Ferreira de Mello, 19 de outubro de 2026), sobre splines de regressão, splines de suavização e introdução aos modelos aditivos generalizados (GAM). Ela retoma as três contas abertas da Aula 9 (a média local achata nas pontas, não devolve fórmula e, com muitos preditores, a vizinhança some) e responde com polinômios por pedaços, emendados sem quina nos nós. A aula fecha com exercícios de cálculo, exercícios conceituais e um laboratório aplicado ao banco do projeto (carga conteinerizada do Porto de Santos).

## Principais etapas

Splines de regressão. Cortar o eixo em pedaços nos nós (aqui, os quartis da variável). Retas soltas saltam nos nós, retas emendadas fazem quina, e a solução é o polinômio cúbico por pedaço, emendado no valor, na inclinação e na curvatura: a spline cúbica. Com K nós ela tem K + 4 coeficientes (graus de liberdade), o mesmo custo de um polinômio de grau K + 3, mas com ajuste local. Por dentro é uma base de funções (x, x², x³ e um cubo truncado por nó) ajustada por MQO comum, a expansão de atributos da Aula 8. Em R, `bs()` faz isso com outra base (B-spline), mais estável, e o ajuste é o mesmo. A spline natural exige que a curva seja reta antes do primeiro nó e depois do último, o que elimina a oscilação nas pontas (`ns()` no R). Fora dos dados a cúbica despenca e a natural segue reta. Na simulação das pontas, o kernel errou sempre para dentro (viés de uns 16 em cada ponta) e a natural acertou na média, ao custo de mais variância. O número de nós se escolhe por validação cruzada, e a curva de CV sai serrilhada porque os nós mudam de lugar a cada df.

Splines de suavização. Em vez de escolher nós, coloca um nó em cada observação e freia a curvatura. A origem é a régua flexível: entre todas as curvas que passam pelos pontos, a que menos dobra (menor integral de g'') é a spline cúbica natural. Com ruído, troca os pinos por molas e minimiza RSS + λ vezes a integral de g''². O botão λ (rigidez da régua dividida pela rigidez das molas) é difícil de ler, então o R aceita o botão em graus de liberdade efetivos (df, o traço da matriz suavizadora). λ perto de 0 interpola os pontos, λ muito grande vira a reta de MQO. df grande treme (variância alta) e df pequeno achata (viés alto). A CV agora sai lisa, porque os nós ficam fixos e só o freio varia. Sem o argumento `df`, `smooth.spline` escolhe por validação cruzada generalizada (GCV).

Placar com um preditor (150 imóveis simulados, CV de 5 dobras): reta 1172, polinômio de grau 6 788, KNN 785, kernel 788, spline natural 780, spline de suavização 783, com piso de 625. As splines empatam em CV, mas o ganho está em serem um MQO (fórmula, predict, faixa de confiança), não terem o viés da média local nas pontas e somarem por preditor.

GAM. Cada preditor ganha a sua curva e a predição é a soma delas: y = β0 + f1(x1) + ... + fp(xp) + erro. A regressão múltipla é o caso em que toda curva é uma reta. O `gam()` do pacote mgcv monta uma base de spline por preditor, junta tudo numa matriz grande, ajusta um MQO penalizado e escolhe os λ por GCV. O resultado vem com graus de liberdade efetivos (edf) por curva: edf perto de 1 é reta. O preço é não ter interações, a menos que se peça (`ti(area, dist)`). No exemplo de três preditores (área, distância até a praia, idade), o GAM achou edf de 8,27 para a área, 4,12 para a praia e 1,00 para a idade, e o erro de CV foi de 1383 (MQO) para 723 (GAM), perto do piso de 625. O KNN com três preditores padronizados ficou em 1357, igual ao MQO, ou seja, a maldição da dimensionalidade já aparece com p igual a 3.

## Exercícios de cálculo

1. Spline cúbica com K = 4 nós: os 5 polinômios soltos têm 5 vezes 4 = 20 coeficientes. Cada nó impõe 3 restrições (valor, 1ª e 2ª derivadas), então 12 restrições, e sobram 8 parâmetros (K + 4). Spline natural com 4 nós internos e 2 de fronteira (6 nós): as duas pontas são retas (4 coeficientes) e os 5 pedaços do meio são cúbicos (20), total 24, menos 6 vezes 3 = 18 restrições, sobram 6 parâmetros.

2. f(x) = 100 + 2x + 3(x − 50)+ − 4(x − 80)+. Valores: f(40) = 180, f(50) = 200, f(60) = 250, f(100) = 370. Inclinações: 2 antes de 50, 5 entre 50 e 80 e 1 depois de 80. A curva é contínua em x = 50, porque (x − 50)+ vale 0 no nó. Só a inclinação muda.

3. Pedágios de g1 = 3 + 2x, g2 = x² e g3 = x³ em [0, 1]: a integral de g''² vale 0, 4 e 12. O slide indica pedágios 0, 4 e 30 para as três candidatas (RSS 52, 30 e 12). Com os valores do slide, o critério RSS + λ vezes pedágio dá: λ = 0,1 vence a terceira (15), λ = 1 vence a segunda (34), λ = 10 vence a primeira (52). Com 12 no lugar de 30, a terceira vence também em λ = 1 (24), e as demais conclusões se mantêm. Conclusão geral: λ pequeno deixa a curva flexível e λ grande puxa para a reta. O valor do pedágio de x³ merece conferência com o professor.

4. GAM com β0 = 340, f_área = −20, f_praia = +60, f_idade = +26: predição de 340 − 20 + 60 + 26 = 406 mil. A 2 km, com f_praia = −11: 340 − 20 − 11 + 26 = 335 mil, queda de 71 mil. Só um termo muda porque o modelo é aditivo, cada curva depende só do seu preditor e os outros ficam fixos.

## Exercícios conceituais

Global contra por pedaços. O polinômio de grau 10 é global: 11 coeficientes governam a curva inteira e nas pontas, onde há poucos dados, ele oscila. A spline natural com 10 df é local (cada pedaço responde aos dados do seu trecho) e vira reta fora dos nós de fronteira.

Os dois botões. Spline de regressão: o número de nós (df), e mais nós é mais flexível. Spline de suavização: o λ (em df efetivos), e λ maior é mais rígido, df maior é mais flexível. A CV da primeira sai serrilhada porque os nós mudam de lugar a cada df. A da segunda sai lisa porque os nós ficam fixos e só o freio varia.

Aditivo. O GAM supõe que o efeito de cada preditor é uma curva que não depende dos valores dos outros. Falha, por exemplo, quando o m² vale mais perto da praia: o efeito da área depende da distância e o GAM erra, subestimando imóveis grandes na orla. A saída é somar `ti(area, dist)`.

O efeito de 1 m². O GAM não responde com um número só, porque o efeito de 1 m² a mais é a inclinação da curva da área naquele ponto, que varia (uns 0,3 mil R$ por m² no patamar de 120 a 170 e 3 a 4 nos degraus). O efeito de 1 ano a mais de idade tem resposta única, porque a curva tem edf 1 (reta), de −1,68 mil R$ por ano.

## Laboratório no banco do projeto

Resposta y = TOTAL_TONELADAS, preditores x1 = TOTAL_TEU, x2 = TOTAL_UNID e x3 = ANO, no subconjunto CARGA CONTEINERIZADA, com amostra de 50.000 linhas (a mesma estratégia da Aula 7) e as mesmas 5 dobras para todos os modelos. O código completo, em blocos, foi entregue no chat. O núcleo é:

```r
library(splines); library(mgcv)
set.seed(1); dobra <- sample(rep(1:5, length = nrow(d)))
cv_de <- function(ajusta) mean(sapply(1:5, function(j) {
  tr <- d[dobra != j, ]; va <- d[dobra == j, ]
  mean((va$y - ajusta(tr, va))^2)
}))
cv_base <- cv_de(function(tr, va) mean(tr$y))
cv_mqo  <- cv_de(function(tr, va) predict(lm(y ~ x1 + x2 + x3, data = tr), va))
dfs <- 2:8
cv_spl  <- sapply(dfs, function(k)
  cv_de(function(tr, va) predict(lm(y ~ ns(x1, df = k) + x2 + x3, data = tr), va)))
cv_gam  <- cv_de(function(tr, va) predict(gam(y ~ s(x1) + s(x2) + s(x3), data = tr), va))
g <- gam(y ~ s(x1) + s(x2) + s(x3), data = d)
round(summary(g)$s.table[, "edf"], 2)
par(mfrow = c(1, 3), pty = "s"); plot(g, scheme = 1)
```

Pergunta do trabalho: quais variáveis da movimentação de cargas conteinerizadas contribuem para a previsão da quantidade de toneladas movimentadas no Porto de Santos?

Ficha da pergunta (laboratório): resposta y = TOTAL_TONELADAS (quantitativa contínua, toneladas); preditores x1 = TOTAL_TEU, x2 = TOTAL_UNID, x3 = ANO (p = 3); tipo supervisionado, regressão, predição com leitura de inferência sobre quais variáveis contribuem; métrica RMSE em toneladas; linha de base a bater: o RMSE de chutar sempre a média; dono do problema: quem planeja a operação portuária e precisa estimar a carga movimentada.

Para responder diretamente "quais variáveis contribuem", o GAM é refeito tirando um preditor de cada vez, com a mesma CV de 5 dobras. A piora do RMSE ao retirar a variável mede quanto ela contribui para a previsão:

```r
nomes <- c(x1 = "TOTAL_TEU", x2 = "TOTAL_UNID", x3 = "ANO")
cv_sem <- sapply(names(nomes), function(v) {
  f <- as.formula(paste("y ~", paste0("s(", setdiff(names(nomes), v), ")", collapse = " + ")))
  cv_de(function(tr, va) predict(gam(f, data = tr), va))
})
contrib <- data.frame(variavel_retirada = nomes[names(cv_sem)],
                      RMSE_sem = round(sqrt(cv_sem), 1),
                      RMSE_completo = round(sqrt(cv_gam), 1),
                      piora_pct = round(100 * (sqrt(cv_sem) / sqrt(cv_gam) - 1), 1))
contrib[order(-contrib$piora_pct), ]
```

Contribuição de cada variável (saída do Colab), RMSE do GAM completo de 1133 toneladas:

| variável retirada | RMSE sem ela | piora |
|---|---|---|
| TOTAL_UNID | 1171,3 | 3,4% |
| TOTAL_TEU | 1134,5 | 0,1% |
| ANO | 1133,5 | 0,0% |

Como TOTAL_TEU e TOTAL_UNID são quase a mesma informação (correlação de 0,984), tirar uma delas quase não piora, porque a outra cobre. Por isso o bloco seguinte mede cada variável sozinha contra a linha de base (RMSE de 2315,9 toneladas):

| variável sozinha | RMSE | melhora sobre a base |
|---|---|---|
| TOTAL_UNID | 1135,0 | 51,0% |
| TOTAL_TEU | 1171,5 | 49,4% |
| ANO | 2309,3 | 0,3% |

Leitura: TOTAL_UNID e TOTAL_TEU contribuem cada uma com cerca de metade da redução do erro, mas são redundantes entre si (juntas não melhoram quase nada além de uma só, 1133 contra 1135). O ANO não acrescenta nada, nem sozinho (0,3%) nem somado às outras (0,0%). Isso responde à pergunta "alguma curva faz rever um preditor?" com sim: o ANO sai. A conclusão vale só para as três variáveis numéricas testadas e descreve associação com a previsão, não causa.

Resultados (saída do Colab, CV de 5 dobras, amostra de 50.000 linhas de carga conteinerizada, erro em toneladas):

| método | CV5 | RMSE |
|---|---|---|
| linha de base | 5.363.422 | 2315,9 |
| MQO (x1 + x2 + x3 retos) | 1.308.404 | 1143,9 |
| melhor spline natural em x1 (df = 4) | 1.303.727 | 1141,8 |
| GAM | 1.283.730 | 1133,0 |

edf do GAM: s(x1) = 9,00 (TOTAL_TEU), s(x2) = 8,66 (TOTAL_UNID), s(x3) = 5,64 (ANO). O edf de x1 chegou a 9,00, o teto da base padrão do `s()` (k = 10), então a curva de TOTAL_TEU está batendo no limite de flexibilidade.

Frase da entrega: TOTAL_TEU e TOTAL_UNID não são retas (edf de 9,0 e 8,7): as duas curvas ficam perto de zero nos valores baixos, sobem forte (TEU entre uns 2.000 e 3.200, UNID até uns 1.200) e depois caem nos valores mais altos. O ANO tem edf de 5,6, mas a curva é praticamente plana. Em CV, porém, o ganho sobre a reta é pequeno: o GAM reduz o RMSE do MQO em menos de 1% (1143,9 para 1133,0), então a curvatura existe mas pesa pouco na previsão. A queda nos valores altos deve ser lida com cautela, porque TEU e UNID têm correlação de 0,984 e as curvas individuais se confundem entre si, com poucos dados nas pontas.

O que isso indica para a pergunta: o GAM bate a linha de base da ficha? Sim, o RMSE cai de 2315,9 para 1133,0 toneladas (queda de 51,1%). Bate também o MQO, mas por pouco (1143,9 para 1133,0). Alguma curva faz rever um preditor? Sim, o ANO: nem sozinho (0,3% de melhora) nem somado às outras (0,0%) ele ajuda a prever as toneladas, então sai do modelo. TOTAL_TEU e TOTAL_UNID ficam, mas contam como uma informação só.

## O que foi aprendido

Que a solução para as três contas abertas da Aula 9 é trocar a média local por polinômios por pedaços ajustados por MQO. Isso devolve uma fórmula, uma predição com faixa de confiança e um comportamento controlado nas pontas, onde a natural vira reta em vez de oscilar ou despencar. Em CV, as splines empatam com polinômio, KNN e kernel, então o ganho não está no erro com um preditor, e sim no que a spline entrega a mais e em como ela se estende a vários preditores.

Que existem dois caminhos para o mesmo U de flexibilidade. Na spline de regressão o botão é o número de nós, e a CV sai serrilhada porque os nós mudam de lugar. Na de suavização o botão é o λ, medido em df efetivos, e a CV sai lisa porque os nós ficam fixos. Em ambos, df maior é mais flexível, e o dilema entre viés e variância é o mesmo do k e do h da Aula 9.

Que o GAM contorna a maldição da dimensionalidade ao assumir aditividade: uma curva por preditor, somadas, ainda é um MQO penalizado. O edf indica quais preditores são retas (perto de 1) e quais são curvas, e cada curva se lê com os outros preditores fixos. O limite é não enxergar interações, que a aula 11 (árvores) passa a pegar com perguntas em sequência.
