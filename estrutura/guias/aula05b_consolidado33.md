# Consolidado — Teoria do Aprendizado Estatístico — Aula 05b (Poisson) — 2026-10-25
*guia versão 1 · tutora: Claude (Sonnet 5.5) · sessão única*
**Aluno:** Arthur Davino Rizzo · **presentes na sessão:** Arthur Davino Rizzo, Luis Felipe Ruas do Nascimento e Lorenzo Ribeiro Louzada · **digitou:** Arthur Davino Rizzo · **teste final:** respondido pelos três

## 1. O que foi passado
- M1 — contagens e a Poisson
- M2 — o log da média como reta; $e^{\beta}$ como razão de taxas
- M3 — glm(family = poisson) e predict(type = "response")
- M4 — o offset
- M5 — sobredispersão e quase-Poisson
- M6 — Poisson contra MQO na validação cruzada

Os seis módulos foram entregues prontos, não construídos em conversa módulo a módulo, e o aluno rodou o código no Colab. O teste final foi aplicado ao fim, por escrito.

## 2. Como foi o aprendizado — opinião da tutora
Eu não conduzi esta aula como o guia pede, em blocos curtos e com um checkpoint por módulo: o Arthur pediu o material pronto, e eu entreguei os seis módulos. Conferi o código numa sessão nova do R e depois o notebook que ele rodou, e os números bateram com o guia (as somas 836, 775 e 550, $\hat\phi=3{,}37$ e o RMSE de validação cruzada de $3{,}99$, $2{,}39$ e $1{,}76$). Por isso não tenho como dizer onde ele travou ou como reagiu aos erros previstos, porque os checkpoints não foram feitos. O que posso dizer vem do teste final: as seis respostas vieram certas e com a conta mostrada, inclusive nos pontos em que o guia espera erro, como ler $e^{\beta}$ como multiplicador (e não como soma), usar o logaritmo do tempo no *offset* e corrigir o erro padrão por $\sqrt{\hat\phi}$. As respostas vieram numa mensagem só, e não uma por vez, e eu não tenho como confirmar que ele não consultou o material.

**Teste final:** o Arthur acertou M1, M2, M3, M4, M5 e M6; nada a revisar. O Luis Felipe e o Lorenzo também responderam o teste e, segundo o relato do grupo, acertaram tudo; as respostas deles não passaram por mim, então a correção que fiz vale só para as respostas do Arthur.

## 3. Observações para a frente
- **Revisar antes da Parte D:** nada pelo teste final. O que ficou sem fazer foram os checkpoints durante a explicação.
- **Para a próxima tutora:** o aluno prefere receber o material pronto e rodar o código, e responde bem a perguntas de cálculo. Numa sessão futura, vale pedir a previsão do resultado antes de rodar o código, como o guia manda.
- **Perguntas guardadas:** nenhuma.
- **Produzido nesta sessão:** as previsões e o placar de validação cruzada das visitas aos anúncios: $3{,}99$ / $2{,}39$ / $1{,}76$, reproduzidos no Colab.
- **Parte D:** feita com o grupo (Arthur Davino Rizzo, Luis Felipe Ruas do Nascimento e Lorenzo Ribeiro Louzada), com o código em `estrutura/codigo/aula05b_poisson.ipynb`.
