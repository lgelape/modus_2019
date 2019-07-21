# Exercício 5

Neste exercício, vamos utilizar amostras estratificadas de candidaturas de 2018 e do Atlas do Desenvolvimento Humano.

```
set.seed(1234)
library(splitstackshape)

# Populacao

banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")

banco_atlas <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/AtlasBrasil_modus2019.csv")

# Amostra

amostra_tse <- stratified(banco_tse, group = c("DS_GRAU_INSTRUCAO", "DS_CARGO"), size = 0.015)

amostra_atlas <- stratified(banco_atlas, group = "regiao", size = 0.02)
```

## Teste t pareado

**1. Utilizando o banco de dados do Atlas do Desenvolvimento Humano, teste, por meio de um teste t pareado, a hipótese de que o índice de gini diminuiu entre os anos de 1991 e 2000, sob um nível de significância de 10%. Não se esqueça de investigar graficamente a distribuição dessas variáveis antes de realizar o teste. Descreva os resultados do seu teste de hipótese.**

## Teste t para amostras independentes

**2. Agora utilizando o banco de candidaturas em 2018, teste por meio de um teste t para amostras independentes se a média de idade dos candidatos varia entre homens e mulheres, sob um nível de confiança de 95%. Descreva os resultados do seu teste de hipótese.**

## Teste Qui-Quadrado

**3. Também utilizando o banco de candidaturas em 2018, teste por meio de um teste qui-quadrado se a disputa pela reeleição está associada ao gênero do candidato, sob um nível de confiança de 90%. Descreva os resultados do seu teste de hipótese.**

