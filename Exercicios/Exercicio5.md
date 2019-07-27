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

**1. Utilizando o banco de dados do Atlas do Desenvolvimento Humano, teste, por meio de um teste t pareado, a hipótese de que o índice de gini aumentou entre os anos de 1991 e 2000, sob um nível de significância de 10%. Não se esqueça de investigar graficamente a distribuição dessas variáveis antes de realizar o teste. Descreva os resultados do seu teste de hipótese.**

```
boxplot(amostra_atlas$gini_91, amostra_atlas$gini_00,
        main = "Distribuição do Indíce de Gini medido nos censos de 1991 e 2000",
        names = c("1991", "2000"),
        ylab = "Índice de Gini",
        ylim = c(0,1))

t.test(amostra_atlas$gini_91, amostra_atlas$gini_00, 
       paired = T, conf.level = 0.90, alternative = "less")
       
# Paired t-test
# 
# data:  amostra_atlas$gini_91 and amostra_atlas$gini_00
# t = -4.1041, df = 110, p-value = 0.00003909
# alternative hypothesis: true difference in means is less than 0
# 90 percent confidence interval:
#        -Inf -0.02051378
# sample estimates:
# mean of the differences 
#            -0.02990991 
```
Sob um nível de significância de 10% (0.10), podemos rejeitar a H0 de que a média do índice de gini dessas amostras são idênticas (isto é que a diferença entre as médias é igual a zero) antes (1991) e depois (2000), dado o nosso valor-p (0.000039), em favor da hipótese alternativa de que esta média aumentou entre os dois anos analisados.

## Teste t para amostras independentes

**2. Agora utilizando o banco de candidaturas em 2018, teste por meio de um teste t para amostras independentes se a média de idade dos candidatos varia entre homens e mulheres, sob um nível de confiança de 95%. Descreva os resultados do seu teste de hipótese.**

```
boxplot(amostra_tse[which(amostra_tse$DS_GENERO == "MASCULINO"), amostra_tse$NR_IDADE_DATA_POSSE], 
        amostra_tse[which(amostra_tse$DS_GENERO == "FEMININO"), amostra_tse$NR_IDADE_DATA_POSSE],
        main = "Distribuição das idades de candidatos segundo o gênero (2018)",
        names = c("Masculino", "Feminino"),
        ylab = "Idade dos candidatos")

# Antes, precisamos testar o pressuposto de mesma variância das nossas duas "amostras" 
var.test(NR_IDADE_DATA_POSSE ~ DS_GENERO, data = amostra_tse)

t.test(NR_IDADE_DATA_POSSE ~ DS_GENERO, data = amostra_tse, 
       conf.level = 0.95, var.equal = T)
       
#       Two Sample t-test
#
# data:  NR_IDADE_DATA_POSSE by DS_GENERO
# t = -2.9216, df = 429, p-value = 0.003667
# alternative hypothesis: true difference in means is not equal to 0
# 95 percent confidence interval:
#  -6.181528 -1.209303
# sample estimates:
#  mean in group FEMININO mean in group MASCULINO 
#               45.86014                49.55556
```

Sob um nível de confiança de 95% (alpha = 0.05), podemos rejeitar a H0 de que essas medias não sejam diferentes (isto é, que a diferença entre a média de idade de homens e mulheres é igual a zero), dado o nosso p-valor (0.003) e a estatística-teste (t = -2.9216).

## Teste Qui-Quadrado

**3. Também utilizando o banco de candidaturas em 2018, teste por meio de um teste qui-quadrado se a disputa pela reeleição está associada ao gênero do candidato, sob um nível de confiança de 90%. Descreva os resultados do seu teste de hipótese.**

```
chisq.test(amostra_tse$DS_GENERO, amostra_tse$ST_REELEICAO)

# Pearson's Chi-squared test with Yates' continuity correction
# 
# data:  amostra_tse$DS_GENERO and amostra_tse$ST_REELEICAO
# X-squared = 1.3747, df = 1, p-value = 0.241
```

Neste teste, não podemos rejeitar a H0 de que as variáveis gênero e disputa pela reeleição são independentes, dado o p-valor (0.241) e a estatística-teste (X-squared = 1.374) encontrados.
