# Exercício de fixação n. 3

Neste exercício de fixação, vamos estimar proporções e médias de variáveis de interesse nos bancos de candidatos do TSE e do Atlas, que temos usado neste curso. Além disso, vamos sortear uma amostra para cada um desses bancos

```
set.seed(1234)

# Populacao

banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")

banco_atlas <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/AtlasBrasil_modus2019.csv")

# Amostra

amostra_tse_casos <- sample(1:29145, 450, replace = F) # Sorteia o numero das observacoes
amostra_tse <- banco_tse[amostra_tse_casos,] # Faz um subset do banco a partir dos n. sorteados
  
amostra_atlas_casos <- sample(1:5565, 300, replace = F)
amostra_atlas <- banco_atlas[amostra_atlas_casos,]
```

## Estimando proporções

**Estime a proporção de indivíduos na nossa amostra de candidatos do gênero feminino, calcule seu erro-padrão, margem de erro e intervalo de confiança (com nível de confiança = 95%)**

```
proporcao <- prop.table(table(amostra_tse$DS_GENERO))[[1]]
erro_padrao <- sqrt((proporcao*(1-proporcao))/nrow(amostra_tse))

margem_erro_95 <- 1.96*erro_padrao

limite_inferior_ic_95 <- proporcao - margem_erro_95
limite_superior_ic_95 <- proporcao + margem_erro_95
```

Para usuários da versão 3.6 do R, a partir do nosso `set.seed(1234)`, os resultados são:

* Proporção de mulheres na amostra: 0.318
* Erro-padrão dessa estimativa: 0.022
* Margem de erro (nível de confiança de 95%): 0.043

E o intervalo de confiança para este nível de confiança mostra que a proporção de mulheres na população estaria entre 27,48% e 36,08%.

**Compare seus resultados com a proporção populacional (`banco_tse`).**

```
proporcao_pop <- prop.table(table(banco_tse$DS_GENERO))[[1]]
```

A proporção de mulheres em nossa amostra (0.318, ou seja, 31,8% de mulheres) é bem próxima da proporção de mulheres nesta população (0.316, ou seja, 31,6% de mulheres).

**Estime agora a proporção de indivíduos nesta amostra de candidatos que se candidatam a deputado federal, calculando também o erro-padrão, margem de erro e intervalo de confiança (agora com nível de confiança = 99%).**

```
proporcao <- prop.table(table(amostra_tse$DS_CARGO))[[5]]
erro_padrao <- sqrt((proporcao*(1-proporcao))/nrow(amostra_tse))

margem_erro_99 <- 2.576*erro_padrao

limite_inferior_ic_99 <- proporcao - margem_erro_99
limite_superior_ic_99 <- proporcao + margem_erro_99
```

Para usuários da versão 3.6 do R, a partir do nosso `set.seed(1234)`, os resultados são:

* Proporção de candidatos a deputado federal na amostra: 0,304
* Erro-padrão dessa estimativa: 0,022
* Margem de erro (nível de confiança de 99%): 0,056

E o intervalo de confiança para este nível de confiança mostra que a proporção de candidatos a deputado federal na população estaria entre 24,86% e 36,03%.

**Compare seus resultados com a proporção populacional.**

```
proporcao_pop <- prop.table(table(banco_tse$DS_CARGO))[[5]]
```

Conforme esperado, a proporção de candidatos a deputado federal em nossa amostra (0.304, ou seja, 30,4% dos candidatos concorreram ao cargo de deputado federal) é próxima da proporção desses candidatos na população (0,295, ou seja, 29,5% dos candidatos concorreram a deputado federal).

## Estimando médias

Estime a média do percentual de pobres no ano 2000 por município, calculando seu erro-padrão, margem de erro e intervalo de confiança (com nível de confiança 90%, 95% e 99%).

```
media_amostra <- mean(amostra_atlas$pobres_00)
erro_padrao <- sd(amostra_atlas$pobres_00)/sqrt(nrow(amostra_atlas))

margem_erro_90 <- 1.645*erro_padrao
margem_erro_95 <- 1.96*erro_padrao
margem_erro_99 <- 2.576*erro_padrao

limite_inferior_ic_90 <- media_amostra - margem_erro_90
limite_superior_ic_90 <- media_amostra + margem_erro_90

limite_inferior_ic_95 <- media_amostra - margem_erro_95
limite_superior_ic_95 <- media_amostra + margem_erro_95

limite_inferior_ic_99 <- media_amostra - margem_erro_99
limite_superior_ic_99 <- media_amostra + margem_erro_99
```

Para usuários da versão 3.6 do R, a partir do nosso `set.seed(1234)`, os resultados são:

* Média do percentual de pobres por município na amostra: 41,06%
* Erro-padrão dessa estimativa: 1,318

As margens de erro (para os nível de confiança de 90%, 95% e 99%):

* 90%: 2,17%
* 95%: 2,58%
* 99%: 3,39%

E os intervalo de confiança para estes três nível de confiança:

* 90%: a média do percentual de pobres na população estaria entre 38,89% e 43,22%
* 95%: a média do percentual de pobres na população estaria entre 38,47% e 43,64%
* 99%: a média do percentual de pobres na população estaria entre 37,66% e 44,45%

**Compare seus resultados com a média populacional (`banco_atlas`).**

```
media_pop <- mean(banco_atlas$pobres_00)
```

Conforme esperado, a média populacional e a média da nossa amostra aleatória simples estão bastante próximas (amostral = 41,0576% e populacional = 41,0570%).
