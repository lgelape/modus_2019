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

Estime a proporção de indivíduos na nossa amostra de candidatos do gênero feminino, calcule seu erro-padrão, margem de erro e intervalo de confiança (com nível de confiança = 95%).

Compare seus resultados com a proporção populacional (`banco_tse`). 

Estime agora a proporção de indivíduos nesta amostra de candidatos que se candidatam a deputado federal, calculando também o erro-padrão, margem de erro e intervalo de confiança (agora com nível de confiança = 99%).

Compare seus resultadoos com a proporção populacional.

## Estimando médias

Estime a média da proporção de pobres no ano 2000 por município, calculando seu erro-padrão, margem de erro e intervalo de confiança (com nível de confiança 90%, 95% e 99%).

Compare seus resultados com a média populacional (`banco_atlas`).
