# Exercício de fixação n. 2

Neste exercício de fixação, vamos testar novamente ideias de amostras para demonstrar o funcionamento do Teorema do Limite Central.

Para tanto, vamos retomar a seleção do banco de dados de candidatos nas eleições de 2018 usada no exercício 1.

```
banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")
```

Sorteie 10.000 amostras de tamanho n = 250 da variável idade na data da posse dos candidatos em 2018 (não se esqueça de incluir a função `set.seed()` antes de executar os códigos, além de incluir o argumento `replace = T` ao sortear cada amostra). Assim como fizemos para os resultados de dados que sorteamos, salve em objetos a média e o desvio-padrão dessa variável em cada uma das amostras.

Compare os valores da média e do desvio-padrão populacional e a média e o erro-padrão das médias amostrais. Eles estão próximos?

Faça o gráfico de densidade de kernel da distribuição das idades de todos os candidatos em 2018 e das médias amostrais. Como você descreveria cada um deles?







