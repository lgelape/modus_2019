# Exercícios de Fixação #1 - Estatísticas descritivas

Neste exercício, vamos retomar algumas das principais funções que utilizamos para calcular estatísticas descritivas.

## Variáveis categóricas

Para fixar aspectos de descrição de variáveis categórias, vamos recorrer a um recorte do banco de candidatos às eleições de 2018, divulgado pelo Tribunal Superior Eleitoral (código de variáveis [disponível aqui](https://github.com/lgelape/modus_2019/blob/master/Bancos/leiame_tse.pdf)). 

```
banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")
```

**1. Faça tabelas de frequência absoluta para descrever as seguintes variáveis: (a) partido; (b) gênero; (c) grau de instrução; (d) cargo que ele está disputando.**

**2. Agora, faça uma tabela de frequência relativa para descrever somente as variáveis (a) gênero e (b) grau de instrução.**

**3. Crie tabelas com frequências absoluta e relativa para as variáveis gênero, grau de instrução e reeleição**.

**4. Faça gráficos de barra para representação das variáveis (a) gênero e (b) reeleição. Não se esqueçam de incluir título e alterar a descrição dos eixos dos gráficos.**

## Variáveis contínuas

Para retomar as estatísticas descritivas de variáveis contínuas, utilizaremos um recorte do banco de dados do Atlas do Desenvolvimento Humano no Brasil, no qual eu selecionei variáveis referentes ao índice de Gini, população total, renda *per capita* e percentual de pobres em 5.565 municípios brasileiros (um pequeno dicionário dessas variáveis está [disponível](https://github.com/lgelape/modus_2019/blob/master/Bancos/VariaveisAtlasBrasil.md)). 

```
banco_atlas <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/AtlasBrasil_modus2019.csv")
```

**1. Calcule os valores mínimo e máximo e mediana para a variável com os valores de renda per capita nos três anos disponíveis (1991, 2000, 2010), usando (a) as funções exclusivas para essas operações; e (b) outras funções que também tragam este resultado.**

**2. Calcule os quartis da distribuição da variável do percentual de pobres por município no ano de 2000, e calcule somente o valor da mediana, usando a função exclusiva para esta operação.**

**3. Calcule os quintis e os decis da distribuição da mesma variável do exercício anterior (percentual de pobres por município no ano 2000).**

**4. Faça os boxplots que descrevem graficamente as estatísticas de ordenamento das variáveis referentes à renda per capita. Inclua títulos em todos esses gráficos.**

**5. Calcule a média e a mediana da variável para o indíce de Gini nos 3 anos disponíveis. O que os resultados nos dizem sobre a distribuição dessa variável?**

**6. Calcule a variância e o desvio-padrão das mesmas variaveis do exercício anterior.**

**7. Calcule a mediana, média, desvio-padrão e variância da variável percentual de pobres por município no ano 2010. Qual resultado você encontrou? Ele parece correto?**

**8.1 Faça o cálculo das seguintes estatísticas descritivas: mínimo, máximo, mediana, quartis, média, desvio-padrão para a variável rpc em 2010, utilizando as funções exclusivas para essas estatísticas e uma das funções "resumidas" que vimos no Tutorial 2.**

**8.2 A partir dessas estatísticas, como você descreveria a variável renda per capita em 2010?**

**8.3 Para descrever as principais estatísticas descritivas, precisamos usar todas as funções que foram solicitadas no enunciado do exercício?**

**8.4 Faça, agora, um histograma e um gráfico de densidade de kernel desta variável. A descrição que você fez anteriormente desta distribuição está refletida nesses gráficos?**
