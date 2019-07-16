# Exercício de fixação n. 1

Neste exercício, vamos retomar algumas das principais funções que utilizamos para calcular estatísticas descritivas.

## Variáveis categóricas

Para fixar aspectos de descrição de variáveis categórias, vamos recorrer a um recorte do banco de candidatos às eleições de 2018, divulgado pelo Tribunal Superior Eleitoral (código de variáveis [disponível aqui](https://github.com/lgelape/modus_2019/blob/master/Bancos/leiame_tse.pdf)). 

```
banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")
```

**1. Faça tabelas de frequência absoluta para descrever as seguintes variáveis: (a) partido; (b) gênero; (c) grau de instrução; (d) cargo que ele está disputando.**

```{r}
table(banco_tse$SG_PARTIDO)
table(banco_tse$DS_GENERO)
table(banco_tse$DS_GRAU_INSTRUCAO)
table(banco_tse$DS_CARGO)
```

**2. Agora, faça uma tabela de frequência relativa para descrever somente as variáveis (a) gênero e (b) grau de instrução.**

```
prop.table(table(banco_tse$DS_GENERO))*100
prop.table(table(banco_tse$DS_GRAU_INSTRUCAO))*100
```

**3. Crie tabelas com frequências absoluta e relativa para as variáveis gênero, grau de instrução e reeleição**.

```
tabela_genero <- rbind(addmargins(table(banco_tse$DS_GENERO)), addmargins(prop.table(table(banco_tse$DS_GENERO))*100))
row.names(tabela_genero) <- c("Frequência absoluta", "Frequência relativa")

tabela_instrucao <- rbind(addmargins(table(banco_tse$DS_GRAU_INSTRUCAO)), addmargins(prop.table(table(banco_tse$DS_GRAU_INSTRUCAO))*100))
row.names(tabela_instrucao) <- c("Frequência absoluta", "Frequência relativa")

tabela_reeleicao <- rbind(addmargins(table(banco_tse$ST_REELEICAO)), addmargins(prop.table(table(banco_tse$ST_REELEICAO))*100))
row.names(tabela_reeleicao) <- c("Frequência absoluta", "Frequência relativa")

colnames(tabela_genero) <- c("Masculino", "Feminino", "Total")
colnames(tabela_instrucao) <- c("Fundamental Completo", "Fundamental Incompleto", "Médio Completo", "Médio Incompleto", "Lê e escreve", "Superior Completo", "Superior Incompleto", "Total")
colnames(tabela_reeleicao) <- c("Não", "Sim", "Total")

tabela_genero
tabela_instrucao
tabela_reeleicao
```

**4. Faça gráficos de barra para representação das variáveis (a) gênero e (b) reeleição. Não se esqueçam de incluir título e alterar a descrição dos eixos dos gráficos.**

```
tabela_genero <- table(banco_tse$DS_GENERO)

barplot(tabela_genero, 
        main = "N. de candidatos por gênero (2018)",
        xlab = "Gênero",
        ylab = "N. de candidatos")

tabela_reeleicao <- table(banco_tse$ST_REELEICAO)

barplot(tabela_reeleicao, 
        main = "N. de candidatos disputando a reeleição (2018)",
        xlab = "O candidato está disputando a reeleição?",
        ylab = "N. de candidatos")
```

## Variáveis contínuas

Para retomar as estatísticas descritivas de variáveis contínuas, utilizaremos um recorte do banco de dados do Atlas do Desenvolvimento Humano no Brasil, no qual eu selecionei variáveis referentes ao índice de Gini, população total, renda *per capita* e percentual de pobres em 5.565 municípios brasileiros (um pequeno dicionário dessas variáveis está [disponível](https://github.com/lgelape/modus_2019/blob/master/Bancos/VariaveisAtlasBrasil.md)). 

```
banco_atlas <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/AtlasBrasil_modus2019.csv")
```

**1. Calcule os valores mínimo e máximo e mediana para a variável com os valores de renda per capita nos três anos disponíveis (1991, 2000, 2010), usando (a) as funções exclusivas para essas operações; e (b) outras funções que também tragam este resultado.**

```
min(banco_atlas$rpc_91)
min(banco_atlas$rpc_00)
min(banco_atlas$rpc_10)

max(banco_atlas$rpc_91)
max(banco_atlas$rpc_00)
max(banco_atlas$rpc_10)

median(banco_atlas$rpc_91)
median(banco_atlas$rpc_00)
median(banco_atlas$rpc_10)
```

**2. Calcule os quartis da distribuição da variável do percentual de pobres por município no ano de 2000, e calcule somente o valor da mediana, usando a função exclusiva para esta operação.**

```
quantile(banco_atlas$pobres_00, seq(0,1,.25))

median(banco_atlas$pobres_00)
```

**3. Calcule os quintis e os decis da distribuição da mesma variável do exercício anterior (percentual de pobres por município no ano 2000).**

```
quantile(banco_atlas$pobres_00, seq(0,1,.1))

quantile(banco_atlas$pobres_00, seq(0,1,.2))
```

**4. Faça os boxplots que descrevem graficamente as estatísticas de ordenamento das variáveis referentes à renda per capita. Inclua títulos em todos esses gráficos.**

```
boxplot(banco_atlas$rpc_91,
        main = "Distribuição da variável renda per capita (1991)",
        ylab = "Renda per capita (em R$)")

boxplot(banco_atlas$rpc_00,
        main = "Distribuição da variável renda per capita (2000)",
        ylab = "Renda per capita (em R$)")

boxplot(banco_atlas$rpc_10,
        main = "Distribuição da variável renda per capita (2010)",
        ylab = "Renda per capita (em R$)")
```

**5. Calcule a média e a mediana da variável para o indíce de Gini nos 3 anos disponíveis. O que os resultados nos dizem sobre a distribuição dessa variável?**

```
mean(banco_atlas$gini_91)
median(banco_atlas$gini_91)

mean(banco_atlas$gini_00)
median(banco_atlas$gini_00)

mean(banco_atlas$gini_10)
median(banco_atlas$gini_10)
```

**6. Calcule a variância e o desvio-padrão das mesmas variaveis do exercício anterior.**

```
sd(banco_atlas$gini_91)
var(banco_atlas$gini_91)

sd(banco_atlas$gini_00)
var(banco_atlas$gini_00)

sd(banco_atlas$gini_10)
var(banco_atlas$gini_10)
```

**7. Calcule a mediana, média, desvio-padrão e variância da variável percentual de pobres por município no ano 2010. Qual resultado você encontrou? Ele parece correto?**

```
mean(banco_atlas$pobres_10)
median(banco_atlas$pobres_10)
sd(banco_atlas$pobres_10)
var(banco_atlas$pobres_10)
```

**8. Faça o cálculo das seguintes estatísticas descritivas: mínimo, máximo, mediana, quartis, média, desvio-padrão para a variável rpc em 2010, utilizando as funções exclusivas para essas estatísticas e uma das funções "resumidas" que vimos no Tutorial 2.**

```
min(banco_atlas$rpc_10)
max(banco_atlas$rpc_10)
median(banco_atlas$rpc_10)
mean(banco_atlas$rpc_10)
sd(banco_atlas$rpc_10)

library(skimr)
skim(banco_atlas$rpc_10)

library(describer)
describe(banco_atlas$rpc_10)
```

**A partir dessas estatísticas, como você descreveria a variável renda per capita em 2010?**

Trata-se de uma variável concentrada à esquerda da distribuição, isto é, em valores majoritariamente baixos de renda per capita. Isso pode ser verificado pela comparação entre os valores de média (cerca de R$ 494) e mediana (aproximadamente R$ 468): a mediana é menor que a média. Além disso, que os valores do terceiro quartil (R$ 651) e o valor máximo (R$ 2044) estão muito mais distantes entre si do que o terceiro quartil está da mediana da distribuição, o que reforça a assimetria identificada.

**Para descrever as principais estatísticas descritivas, precisamos usar todas as funções que foram solicitadas no enunciado do exercício?**

Não, bastaria a função que resume os resultados. As funções individuais são úteis para inspeções rápidas de aspectos específicos do banco de dados.

**Faça, agora, um histograma e um gráfico de densidade de kernel desta variável. A descrição que você fez anteriormente desta distribuição está refletida nesses gráficos?**

```
histograma_rpc00 <- hist(banco_atlas$rpc_00)
histograma_rpc00$density <- histograma_rpc00$counts/sum(histograma_rpc00$counts)*100
plot(histograma_rpc00, freq = F,
     main = "Renda per capita por município brasileiro (2000)",
     xlab = "Renda per capita (em R$)",
     ylab = "Frequência relativa")

plot(density(banco_atlas$rpc_00),
     main = "Renda per capita por município brasileiro (2000)",
     xlab = "Renda per capita (em R$)",
     ylab = "Densidade")
```

