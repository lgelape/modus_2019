# Tutorial 2

Antes de iniciarmos a próxima etapa, vamos limpar o ambiente de trabalho. A função `rm` serve para remover objetos do environment. Ela deve vir acompanhada do argumento `list`, que incluirá a lista de objetos a serem removido. No caso, removeremos todos os objetos do ambiente de trabalho, que são listados pela função `ls`.

```
rm(list = ls())
```

Pronto, agora nosso environment está sem nenhum objeto.

# 1. Estatísticas descritivas e tabelas de frequência

O cálculo de estatísticas descritivas no R é bastante simples. Existem funções para o cálculo das principais estatísticas descritivas, além de funções que apresentam um resumo destas.

Para calculá-las, vamos usar outras variáveis do questionário respondido pelos colegas. Contudo, dessa vez, para abrirmos o banco de dados, vamos usar a função `read.csv2`, ao invés da `read.table`. A `read.csv2` é uma função já programada para abrir arquivos em formato .csv separados por `;`, o que exige a inclusão de menos argumentos.

```
banco <- read.csv2("")
```

Começaremos com o cálculo de estatísticas descritivas de variáveis contínuas, destacando as estatísticas de ordenamento e as estatísticas de momento. Por fim, vamos descrever variáveis categóricas.

A representação visual dessas estatísticas será vista no Tutorial 3.

## 1.1 Estatísticas de ordenamento

Os nomes das funções para o cálculo de estatísticas descritivas são, em geral, o nome em inglês ou uma abreviatura do nome dessa estatística.

### 1.1.1 Mediana

Assim, para o cálculo da **mediana** de uma distribuição, usamos a função `median`. Vamos então calcular a mediana de minutos de deslocamento até a UFMG dos alunos dessa oficina e também a mediana do número de livros lidos por eles.

```
median(banco$minutos_deslocamento)

median(banco$livros_lidos)
```

## 1.1.2 Mínimo e máximo

As estatísticas de valores **mínimo** e **máximo** são convenientes para a compreensão do ordenamento e alcance dos valores de uma variável contínua. Elas também podem ser úteis para identificação de erros ou valores discrepantes no banco de dados (por exemplo, se o valor máximo de uma variável "idade" é 135 anos, isso sugere que houve um erro de preenchimento).

```
min(banco$minutos_deslocamento)
max(banco$minutos_deslocamento)

range(banco$minutos_deslocamento) # apresenta os valores minimo e maximo

min(banco$livros_lidos)
max(banco$livros_lidos)

range(banco$livros_lidos)
```

## 1.1.3 Quantis

Como vimos, algumas das principais estatísticas para descrever uma distribuição de variável contínua são os quantis. O R nos dá grande flexibilidade para o seu cálculo. Para tanto, usamos a função `quantiles`. Geralmente, os quantis utilizados para descrever uma distribuição são os *quartis*.

```
# Quartis
quantile(banco$minutos_deslocamento, probs = seq(0, 1, 0.25))
quantile(banco$minutos_deslocamento, probs = c(0, 0.25, 0.5, 0.75, 1))

# Quintis
quantile(banco$minutos_deslocamento, probs = seq(0, 1, 0.2))
quantile(banco$minutos_deslocamento, probs = c(0, .2, .4, .6, .8, 1))

# Decis
quantile(banco$minutos_deslocamento, probs = seq(0, 1, .1))
quantile(banco$minutos_deslocamento, probs = c(0, 0.1, 0.2, 0.3, 0.5,
                                 0.6, 0.7, 0.8, 0.9, 1))

# Percentis
quantile(banco$minutos_deslocamento, probs = seq(0, 1, 0.01))
```

A função `IQR` calcula o intervalo interquartil (IIQ), isto é, a diferença entre os valores do terceiro e do primeiro quartil da distribuição.

```
IQR(banco$minutos_deslocamento)
```

## 1.2 Estatísticas de momento

### 1.2.1 Média

A principal estatística de momento é a **média**. Para calculá-la, usamos a função `mean`. 

```
var(banco$minutos_deslocamento)
sd(banco$minutos_deslocamento)
```

### 1.2.2 Variância e Desvio-Padrão

O cálculo da **variância** (`var`) e do **desvio-padrão** (`sd`) seguem a mesma lógica das funções anteriores.

```
var(banco$minutos_deslocamento)
sd(banco$minutos_deslocamento)

var(banco$livros_lidos)
sd(banco$livros_lidos)
```

## 1.3 Resumo de estatísticas descritivas

Existem também funções que trazem um **resumo das nossas estatísticas descritivas**, gerando um output com várias das estatísticas referidas acima.

A função `summary`, do R base, nos retorna o mínimo, 1o quartil, mediana, média, 3o quartil e máximo da distribuição de uma variável.

```
summary(banco$minutos_deslocamento)
```

Ela também apresenta um resumo de todas as variáveis do banco:

```
summary(banco)
```

Uma função semelhante, porém mais completa, é a `skim` do pacote `skimr`.

```
#install.packages("skimr")
library(skimr)
skim(banco$minutos_deslocamento)
```

Podemos usar as ferramentas de manipulação de vetores, que já conhecemos, para selecionar somente as informações que nos interessam.

```
descritivas_minutos <- skim(banco$minutos_deslocamento)

# Vamos selecionar somente os elementos n, mean, sd, p0, p25, p50, p75, p100:

descritivas_minutos <- descritivas_minutos[c("n", "mean", "sd", "p0", 
                                           "p25", "p50", "p75", "p100")]

# Agora, basta renomear a linha e as colunas e temos uma tabela pronta

names(descritivas_minutos) <- c("N. obs.", "Média", "Desvio-Padrão", "Mínimo", 
                               "1o quartil", "Mediana", "3o quartil", "Máximo")
descritivas_minutos
```

Outra opção é a função `describe` do pacote `describer`. Ela faz um rersumo das estatísticas descritivas de um banco de dados. Vamos testá-la com nosso `banco` completo.

```
# install.packages("describer")
library(describer)

describe(banco)
```

Ele ficou com muita informação. Por que não selecionamos somente as variáveis que se referem aos minutos de deslocamento?

```
describe(banco$minutos_deslocamento)
```

Se quisermos, podemos renomear as colunas desse output, assim como fizemos com a `skim`. Tente fazer isso!

## 1.4 Tabelas de Frequência

**Tabelas de frequência** com contagem simples são facilmente realizadas com funções do R base:

```
table(banco$time)                   # frequencia absoluta
prop.table(table(banco$time)) * 100 # frequencia relativa

table(banco$area_atuacao)
prop.table(table(banco$area_atuacao)) * 100
```

Por fim, nós podemos fazer um **cruzamento de 2 variáveis categóricas** numa mesma tabela:

```
table(banco$area_atuacao, banco$meio_transporte)
prop.table(table(banco$area_atuacao, banco$meio_transporte)) * 100
```

# Resumo do conteúdo trabalhado:

* Neste tutorial, aprendemos a calcular estatísticas descritivas das nossas variáveis contínuas e categóricas.

* Para realizar esses cálculos  de variáveis contínuas, usamos as funções:

    * `median` (mediana);
    * `min` (mínimo);
    * `max` (máximo);
    * `range` (mínimo e máximo);
    * `quantile` (quantis);
    * `IQR` (intervalo interquartil);
    * `mean` (média);
    * `var` (variância);
    * `sd` (desvio-padrão).

* Vimos ainda três funções diferentes que retornam um conjunto de estatísticas descritivas: a `summary`, a `skim` (do pacote `skimr`) e a `describe` (do pacote `describer`).

* Para descrever nossas variáveis categóricas, conhecemos as funções `table` e `prop.table`, usadas para produzir tabelas de frequencia.

# Orientações Finais

Revise com cuidado o [Tutorial 1](https://github.com/lgelape/modus_2019/blob/master/Tutoriais/Tutorial1.md) e este tutorial 2. Caso exista alguma dúvida, pergunte! Senão, fique a vontade para voltar para casa, ou já começar o [Exercício de Fixação 1]().
