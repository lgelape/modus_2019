# Breve introdução ao R

# 1. Introdução à linguagem R

Nesta parte inicial do curso, vamos apresentar alguns elementos fundamentais da linguagem e, simultaneamente, discutir algumas convenções que facilitam a  legibilidade do código e evitam erros. 

Este tutorial deve ser bastante útil para os dias desse curso. **Volte a ele sempre que necessário**.

## 1.1 Objetos, Vetores e Funções

Começaremos pela compreensão do que são objetos, vetores e funções, três elementos fundamentais para a utilização do R. 

### 1.1.1 Objetos

Objetos são nomes que guardam informações (como números, textos,bancos de dados, etc) que podem ser acessados a qualquer momento da sua sessão.

Podemos criar um objeto com os operadores `<-` ou `=`. Apesar de ambas as possibilidades, recomendo a utilização do `<-` uma vez que o `=` será utilizado para outros fins, evitando confusões.

```
x <- 1
y = 4
```

Se não colocarmos nada após o operador, o que acontece?

```
x <- 
```

Caso o objetivo seja criar um objeto vazio, isso é indicado com `NULL`.

```
x <- NULL
```

Existem algumas recomendações para se nomear objetos:

* O que o R não permite?

Não é possível criar nomes que começam por (1) números, (2) caracteres especiais ou (3) com espaços:

```
# Exemplos

1x <- 1 # (1)

_a <- 1 # (2)
.1 <- 1

meu objeto <- 1 # (3)
```

* O que devemos evitar?

Devemos evitar (1) o uso de letras maiúsculas, pois o R é *case sensitive*, (2) o uso de nomes iguais aos de funções, (3) evitar acentos ou caracteres especiais, pois eles podem não abrir em outras sessões do R, a depender do *encoding* adotado pelo usuário, (4) usar o nome de objetos já existentes no seu ambiente, pois o R sobrescreverá o objeto existente.

```
# Exemplos

MAIUSCULA <- 5 # (1)
maiuscula <- 5 

rm <- 1 # (2)

ação <- 1 # (3)
```

* Quais são boas práticas de nomeação de objetos?

Além de evitar as práticas descritas acimas, uma importante dica para auxiliar o usuário e futuros leitores do código é a utilização do `_` para espaçamento em nomes de objetos.

```
# Exemplos

meuobjeto <- 1 # Ruim
meu_objeto <- 1 # Bom
```

Para verificar quais os nomes de objetos estão sendo utilizados, você pode checar seu *global environment*, ou usar a funcao `ls`, que imprimirá esses nomes no *console* do R.

```
ls()
```

### 1.1.2 Vetores e introdução de classe de objetos

Objetos comportam uma série de informações. Dentre elas, uma daquelas que usaremos com grande frequência são os **vetores**. Vetores são um conjunto de informações atribuídas em uma única linha.

As informações guardadas em objetos podem ser de diferentes *classes*. Começaremos pelas classes numérica (`numeric`) e texto (`character`).

Vetores numéricos podem ser criados de diversas formas, e podem conter valores positivos, negativos, inteiros ou decimais:

```
vetor_1 <- 1:10
vetor_2 <- c(0.1, -3.5, 2.556, 5.1)
```

Vetores `character` contém textos. Textos são definidos pelo uso de `" "`. Assim como em informações da classe `numeric`, podemos criar vetores com textos:

```{r vetores_2}
exemplo <- "texto"
vetor_3 <- c("Meu", "exemplo", "de", "vetor")
```

Estas não são as únicas classes de objetos que existem e que utilizaremos. Outras serão apresentados à medida que progredirmos no curso.

### 1.1.3 Apresentando funções e retornando às classes de objetos

Funções são as principais ferramentas do R para o desempenho de tarefas. O R apresenta algumas funções básicas, mas usuários podem criar suas próprias funções. Como exemplos para compreender a estrutura básica de uma função, veremos a função `class` que nos diz qual a classe de um objeto.

```
class(vetor_1) # integer
class(vetor_4) # numeric
class(vetor_5) # character
```

Além da função que nos diz a classe de um objeto, podemos "perguntar" se ele é de certa classe. O resultado dessas funções nos trazem um nova classe de objeto: `logical`. Objetos lógicos são resultados *verdadeiro/falso* (`TRUE` ou `FALSE`) de operadores lógicos.

```
is.numeric(vetor_1) # TRUE
is.numeric(vetor_3) # FALSE

objeto_logico <- is.numeric(vetor_1)
class(objeto_logico) # logical
```

O R permite a criação de objetos/vetores formados por elementos de classes diferentes. Contudo, ao uní-los em um único vetor, a classe do objeto se torna aquela que permite conversão e manipulação dos dados. 

```
a_1 <- c(2, "character") # R converte para character
a_2 <- c(FALSE, 3) # R converte para numeric (TRUE vira 1, FALSE vira 0)
a_3 <- c("Texto", T)  # R converte para character
a_4 <- c(1.3, -2) # R converte para numeric
```

Podemos usar funções para forçar a conversão de uma classe para outra

```
as.numeric(TRUE) # Transforma TRUE (que e' logical) para numeric
as.character(1.2) # Transforma 1.2 em character
```

Isso nem sempre funciona. Se tentarmos converter texto para números, por exemplo, o R não saberá o que fazer (pois a operação não faz sentido) e retornará um aviso.

```
as.numeric("Meu texto")
```

O resultado da última operação é `NA`: o *missing* do R (geralmente, missings são indicados em bases de dados como 99999999 ou semelhantes). Note, também, que `NA` é uma classe própria.

```
is.numeric(NA) # NA != numerico
is.character(NA) # NA != texto
is.na(NA) # NA = NA!
```

## 1.2 Manipulando objetos

Vimos que objetos podem conter diferentes classes de informação e que podemos aplicar funções a eles. Veremos agora diferentes formas em que é possivel manipular objetos (e vetores, por extensão).

Com objetos numéricos, podemos fazer qualquer operação matemática. Vamos então criar um objeto numérico, acessar diferentes valores dentro dele e fazer operações.

```
# Criar o objeto
meu_objeto <- c(0:50, 60, 70, 80, 90)
meu_objeto

# "Acessar" o valor de determinado elemento do vetor
meu_objeto[1] # acessa o 1o elemento do vetor 'meu_objeto'
meu_objeto[55] # acessa 55o elemento do vetor 'meu_objeto'

# Por meio dessa selecao de valores, podemos fazer operacoes:
meu_objeto[1] + meu_objeto[10] + meu_objeto[55] 
meu_objeto[1] + meu_objeto[10] * meu_objeto[55]
meu_objeto[1] - meu_objeto[10] 
meu_objeto[10] ^ meu_objeto[3]
```

Podemos ainda usar funções para calcular algumas estatísticas descritivas, guardá-las em objetos e unir todas essas informações em um vetor.

```
# Calcular algumas estatisticas descritivas:
mean(meu_objeto) # media
max(meu_objeto)  # maximo
min(meu_objeto)  # minimo

# Guardar essas informacoes em objetos
media  <- mean(meu_objeto)
maximo <- max(meu_objeto)
minimo <- min(meu_objeto)

# Unir em um vetor
descritivas <- c(media, maximo, minimo)
descritivas
```

### 1.2.1 Matrizes

Para explorar mais a manipulação de objetos, vamos trabalhar com um nova classe de objeto: as **matrizes**. Basicamente, matrizes são vetores com 2 dimensões: x linhas e y colunas, cuja *estrutura é semelhante àquela de bancos de dados*.

```
matrix(nrow = 2, ncol = 2)
```

Por exemplo, podemos criar uma matriz com duas colunas (ou "variáveis", caso fosse um banco de dados) e 100 linhas ("observações"). Até o momento, estudamos funções que exigiam somente um argumento: o nome dos objetos. Porém, certas funções exigem mais de um argumento para funcionarem, como a função `matrix`. No caso, o primeiro argumento (1) dá o valor a ser utilizado para preenchimento da matriz, o segundo (100) é o número de linhas, e o terceiro (2) o número de colunas.

```
minha_matriz <- matrix(1, 100, 2)
```

Na ajuda de uma função podemos ver a sua estrutura básica e identificar quais os argumentos vinculados a ela. Além disso, a ajuda nos descreve o que a função faz e apresenta exemplos de utilização. Para acessar a ajuda utilizamos uma interrogação na frente do nome da função ou utilizamos a função `help`. A ajuda do R será útil em boa parte das vezes em que você recorrer a ela. Porém, ela não é infalível. Muitas vezes precisamos de informações que não se encontram na ajuda. Nesses casos, podemos recorrer ao Google [e a uma série de fóruns e blogs](http://denissonsilva.com/programando-em-r/11-pedindo-ajud), como o [stackoverflow](https://stackoverflow.com/) e o [R-bloggers](https://www.r-bloggers.com/).

```
?matrix
help(matrix)
```

Poderíamos reescrever a função que criou o objeto `minha_matriz` utilizando o nome dos argumentos. Ao usar esses nomes, os argumentos não precisam estar na ordem "correta", indicada na descrição da função.

```
minha_matriz <- matrix(ncol = 2, data = 1:200, nrow = 100)
```

Como matrizes funcionam de forma semelhante a vetores, podemos acessar cada elemento dela do mesmo jeito que fazemos com vetores normais. Mas, se quisermos acessar uma coluna ou linha inteira, precisamos usar um indexador mais complexo: [x, y], onde **x** indica o número da linha que queremos acessar, e **y** o número da coluna. Embora pareça complexo, este sistema de indexação é muito útil para se trabalhar com o R, principalmente com bases de dados (data frames). 

```
# Acessando elementos individuais da matriz:
minha_matriz[1]

# Seleciona a primeira linha inteira da matriz:
minha_matriz[1, ]

# Seleciona a segunda coluna da matriz, tambem em formato de vetor
minha_matriz[, 2] # retorna um vetor

# Porem, ao usarmos o argumento drop = F, a selecao retorna uma matriz, com uma coluna
minha_matriz[, 2, drop = FALSE]

# Se quisermos acessar o elemento que se encontra na 1a linha da 2a coluna:
minha_matriz[1, 1]

# Podemos ainda guardar os elementos acessados em um objeto:
m1 <- minha_matriz[2, 1]
m2 <- minha_matriz[1, ]
```

## 1.3 Pacotes

Até o momento, trabalhamos somente com funções "embutidas" no R, o que é conhecido como *R Base*. Porém, uma das características mais atrativas do R é o extenso numero de **pacotes** desenvolvidos por usuários, que possuem as mais diversas utilidades. Para vocês terem uma pequena ideia de alguns pacotes úteis para pesquisas em ciências sociais (ou áreas afins), [o pesquisador Denisson Silva apresenta alguns deles](http://denissonsilva.com/programando-em-r/18-kit-pacotes-r-para-cientistas-sociais). Dentre eles, encontram-se pacotes para trabalhar com dados eleitorais, do IBGE ou do SUS, por exemplo.

Para carregar um pacote no R, usamos a função `library`. Como argumento, incluímos o nome do pacote que desejamos carregar. Caso o nome do pacote esteja errado, o R retornará um erro. Este procedimento deve ser repetido sempre que uma nova sessão do R for iniciada.

Vamos carregar um pacote que usaremos bastante daqui para frente: o dplyr. Caso ele não esteja instalado no seu computador, o R apresentará uma mensagem de erro. Nesse caso, é necessário instalar o pacote antes de utilizá-lo, por meio da função `install.packages`. 

```
# No caso da funcao install.packages, o nome do pacote deve vir entre aspas.
install.packages("dplyr") 
library(dplyr)
```

Uma boa prática de redação de scripts é sempre redigir, no topo deles, os pacotes que serão utilizados para conduzir os procedimentos programados. Assim, ao se executar o script desde o início, teremos todas as habilitado todas funções necessárias.

# Pausa

Pare, respire, beba uma água, esclareça suas dúvidas e vamos seguir!

# 2. Carregar e visualizar bancos de dados

O R é um software extremamente flexível no que se refere aos formatos de arquivos com os quais pode trabalhar. Dessa forma, ele consegue abrir bancos de dados oriundos de diferentes programas, de maneira simples e (na maior parte das vezes) rápida.

Neste curso, vamos trabalhar somente com dados em formato .csv. Porém, se você tiver necessidade de abrir arquivos em outro formato, leia [este capítulo do livro de Fernando Meireles e Denisson Silva](http://electionsbr.com/livro/importacao.html).

## 2.1 Carregando um banco de dados

Uma funcão "coringa" para se abrir bancos é a `read.table`. Vamos abrir um banco de dados de exemplo direto do repositório do curso.

```
banco <- read.table("https://raw.githubusercontent.com/lgelape/Curso_2018_ENAP/master/bancos/AtlasBrasil/AtlasBrasil_Consulta3_tratado.csv")
```

Aparentemente, funcionou. Mas será que ele realmente abriu o banco de dados corretamente? Vamos clicar na janelinha que está no final da linha determinada por "banco" no seu Environment.

Ao abrirmos o banco de dados, ele claramente não está correto. Aparentemente, ele só tem 2 variáveis, os nomes dos municípios não estão escritos corretamente e os valores da segunda variável não parecem fazer sentido.

O que pode ter dado errado?

A função `read.table` possui diversos argumentos que podem ser acrescentados para permitir a abertura correta de um banco de dados. Quais seriam eles? 

Normalmente, trata-se do argumento `sep`, que indica qual o separador das células do banco. Outros  argumentos importantes são:

* `dec` estabelece qual o símbolo dos decimais;
* `header` diz se a 1ª linha do banco traz os nomes das variáveis; 
* `na.strings` estabelece como os missings estão escritos no banco original, e que serão traduzido para o  R como `NA`; e
* `skip` indica o n. de linhas que deve ser pulado no inicio da leitura do banco.

Porém, como descobrimos isto? Se a pessoa que produziu o banco de dados seguiu os melhores procedimentos para tanto, existirá um arquivo "leia-me" com essas informações. Caso o banco não venha acompanhado de um arquivo desse tipo, podemos abrir o arquivo e verificar tais informações. Mas, o arquivo pode ser muito grande e de difícil manuseio. Nesses casos, a tentativa e erro (ou o pedido de ajuda para algum colega que já tenha trabalhado com o banco!) é uma opção válida.

Para este banco de dados, que é um recorte do [Atlas do Desenvolvimento Humano no Brasil](http://atlasbrasil.org.br/2013/pt/), que eu converti para o formato .csv, as células estão separadas por `;`.

```
banco <- read.table("https://raw.githubusercontent.com/lgelape/Curso_2018_ENAP/master/bancos/AtlasBrasil/AtlasBrasil_Consulta1.csv", 
                    sep = ";")
```

Incluir o argumento `sep = ";"` não foi o suficiente! Por quê?

O argumento `encoding` é utilizado para [especificar a codificação](https://support.rstudio.com/hc/en-us/articles/200532197-Character-Encoding) segundo a qual os caracteres devem ser lidos. No nosso caso (e em vários casos de bancos de dados produzidos no Brasil), ele deve ser usado para permitir a leitura do banco sob a codificação `"latin1"`, que permite a [leitura do alfabeto latino](https://pt.wikipedia.org/wiki/ISO/IEC_8859-1). Outras opções que podem ser tentadas são a `"windows-1252"` ou a `"utf-8"`.

Além deles, vamos também incluir os argumentos `header = T` e `dec = ","` para especificar que a primeira linha do banco traz os nomes das variáveis e que o marcador que define os decimais é a vírgula.

```
banco <- read.table("https://raw.githubusercontent.com/lgelape/Curso_2018_ENAP/master/bancos/AtlasBrasil/AtlasBrasil_Consulta1.csv", 
                    sep = ";", encoding = "latin1", header = T, dec = ",")
```

## 2.2 Exploração preliminar de um banco de dados

Como vimos antes, ao guardarmos as informações de um banco de dados em um objeto, podemos visualizar esse banco ao clicar no ícone correspondente. Para realizar a mesma operação por meio de um código, podemos usar a função `View`.

```
View(banco) # nao se esquecam que o V e maiusculo!
```

Contudo, no R precisamos evitar trabalhar com um olhar constante para o banco, uma vez que uma das principais vantagens (a capacidade de se trabalhar com um alto volume de dados em relativamente pouco tempo) acabará se perdendo. 

Sendo assim, para não precisarmos olhar constantemente para o banco, o R apresenta algumas funções que nos permitem "espiá-lo" e verificar, ao menos preliminarmente, se ele foi aberto de forma correta. Aqui veremos 2 delas.

A primeira dessas funções é a `head`, que apresenta os nomes das variaveis e algumas observações iniciais do banco em questão.

```
head(banco)
```

Além da `head`, temos a função `glimpse`, que pode ser utilizada quando carregamos o pacote `dplyr`.

```
library(dplyr)
glimpse(banco)
```

## 2.3 Identificação de variáveis

Ao explorarmos o banco com o qual estamos trabalhando, vimos que é possivel identificar, de forma geral, o nome e tipos de variáveis.

Porém, por vezes é necessário identificá-los em contextos mais aplicados, que não do panorama do banco como um todo.

Para verificarmos o nome de todas as variáveis do nosso banco,  podemos usar a função `names`, que nos retorna um vetor (lembra-se dele?) com os nomes das variáveis.

```
names(banco)
```

E se quisermos saber qual o tipo dessa variável (categórica x contínua)? Assim como para os vetores, utilizamos a funcao `class`.

A função `class` aplicada ao banco nos retorna a classe do objeto completo do banco de dados (um data.frame, portanto).

```
class(banco)
```

Para acessarmos uma das variáveis desse banco, utilizamos o operador `$`.
```
class(banco$Índice.de.Gini.1991)
class(banco$Espacialidades)
```

Opa, a variavel 'Espacialidades' é de uma classe diferente `factor`. Esta classe é utilizada para se trabalhar com variaveis categóricas no R (assim como a `character`). Veremos um pouco mais sobre ela futuramente.

Além disso, vocês devem ter observado que os nomes dessas variáveis vão contra todas as dicas que colocamos sobre como criar nomes de objetos (e, por extensão, de variáveis) no R. Como corrigir isto? Ao longo do curso vou mostrar como isso pode ser feito, mas vocês não precisam se preocupar, pois todos os bancos de dados que usaremos estarão com nomes que nos evitarão problemas.

# Resumo do conteúdo trabalhado no Tutorial 1:

* Nos familiarizamos com a interface do *R Studio*.

* Aprendemos a criar objetos e guardar informações neles (com '<-').

* Discutimos algumas dicas na criação de nomes de objetos.

* Vimos que os objetos podem ser de várias classes (character, numeric, NA...).

* Conhecemos as funções, os *verbos* do R, e sua estrutura.

* Exploramos vetores, realizando operações e seleções a partir deles.

* Aprendemos a pedir ajuda (help e ?) dentro do R e entendê-la.

* Trabalhamos o básico de matrizes, objetos com lógica de funcionamento semelhante à bases de dados.

* Conhecemos a ideia de pacotes, que aumentam substancialmente as potencialidades do R.

* Aprendemos a abrir um banco de dados no R, com alguns cuidados que podem ser necessários.

* Utilizamos algumas funções para fazer uma exploração inicial do banco: `View`, `head` e `glimpse`.

* Aprendemos como acessar os nomes e tipos das variáveis da base de dados.

# Orientações Finais

Revise o material para o caso de dúvidas. Se estiver confortável, siga para o [Tutorial 2](), onde vamos calcular algumas variáveis do banco de dados gerado a partir do questionário respondido pelos colegas.
