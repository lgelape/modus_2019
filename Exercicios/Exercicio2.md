# Exercício de fixação n. 2

Neste exercício de fixação, vamos testar novamente ideias de amostras para demonstrar o funcionamento do Teorema do Limite Central.

Para tanto, vamos retomar a seleção do banco de dados de candidatos nas eleições de 2018 usada no exercício 1.

```
banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")
```

**Sorteie 10.000 amostras de tamanho n = 250 da variável idade na data da posse dos candidatos em 2018 (não se esqueça de incluir a função `set.seed()` antes de executar os códigos, além de incluir o argumento `replace = T` ao sortear cada amostra). Assim como fizemos para os resultados de dados que sorteamos, salve em objetos a média e o desvio-padrão dessa variável em cada uma das amostras.**

```
set.seed(1234)

medias_amostrais <- NA
sd_amostrais <- NA

n_amostra <- 250

for(i in 1:10000){
  
  amostra_idades      <- sample(banco_tse$NR_IDADE_DATA_POSSE, size=n_amostra, replace=T)
  medias_amostrais[i] <- mean(amostra_idades)
  sd_amostrais[i]     <- sd(amostra_idades)
  
}
```

**Compare os valores da média e do desvio-padrão populacional e a média e o erro-padrão das médias amostrais. Eles estão próximos?**

```
mean(banco_tse$NR_IDADE_DATA_POSSE)
mean(medias_amostrais)

sd(medias_amostrais)
mean(sd_amostrais)/sqrt(n_amostra)
```

Sim, ambos estão muito próximos aos valores populacionais.

**Faça o gráfico de densidade de kernel da distribuição das idades de todos os candidatos em 2018 e das médias amostrais. Como você descreveria cada um deles?**

```
plot(density(banco_tse$NR_IDADE_DATA_POSSE),
     main = "Gráfico de densidade das idades de candidatos (TSE, 2018)",
     xlab = "Idade dos candidatos (em anos)",
     ylab = "Densidade",
     xlim = c(0,100))

plot(density(medias_amostrais),
     main = "Gráfico de densidade das médias amostrais das idades\nde candidatos em amostras aleatórias de candidatos (TSE, 2018)",
     xlab = "Idade dos candidatos (em anos)",
     ylab = "Densidade")
```

O gráfico de densidade das idades de candidatos em 2018 tem uma distribuição que se aproxima de uma forma de sino, mas que apresenta maior variabilidade nas idades menores que a média/mediana. Já o gráfico de densidade das médias amostrais revela uma distribuição em forma de sino que é bastante próxima de uma normal. A variabilidade dela é bastante menor que aquela da distribuição de idades, pois a maioria dos seus casos está próxima à média/mediana.








