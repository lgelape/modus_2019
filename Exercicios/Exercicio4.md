# Exercício 4

Neste exercício 4, vamos trabalhar com os dados (que a essa altura já devem ser bastante familiares) de candidaturas em 2018 e o recorte do Atlas do Desenvolvimento Humano no Brasil. Assim como em exercícios anteriores, vamos retirar amostras desses bancos. Porém, neste exercício 4, vamos trabalhar com amostras estratificadas.

Vamos fazer a estratificação com a função `stratified` do pacote `splitstackshape` (caso você não tenha o pacote não se esqueça de instalá-lo!). Na função `stratified` devemos especificar alguns argumentos para realizar a estratificação:

* `group`: deve ser um vetor em texto com o nome das variáveis a serem usadas na estratificação;
* `size`: tamanho em números absolutos ou em proporção que cada grupo deve ter da população amostrada;
* `replace`: nossa amostra é com ou sem reposição? Ao contrário da função `sample`, o default deste argumento na função `stratified` é `replace = F`.

Para a população de candidaturas do TSE, vamos estratificar nossa amostra pelo cargo disputado e grau de instrução, especificando que queremos que o tamanho da amostra seja proporcional ao número de observações por grupo, com um n que corresponda a cerca de 1% do tamanho da população (aproximadamente 291 candidaturas).

Já para o banco do Atlas do Desenvolvimento Humano, vamos fazer uma estratificação pela região do país, especificando uma amostra proporcional ao número de municípios em cada região, com um n que corresponda a 2% do tamanho da população (aproximadamente 111 municípios).

```
set.seed(1234)
library(splitstackshape)

# Populacao

banco_tse <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/candidatos2018_filtrado.csv")

banco_atlas <- read.csv2("https://raw.githubusercontent.com/lgelape/modus_2019/master/Bancos/AtlasBrasil_modus2019.csv")

# Amostra

amostra_tse <- stratified(banco_tse, group = c("DS_GRAU_INSTRUCAO", "DS_CARGO"), size = 0.01)

amostra_atlas <- stratified(banco_atlas, group = "regiao", size = 0.02)
```

## Testes de hipóteses

Lembrando dos 5 passos para realizarmos testes de hipótese/significância:

* **Suposição**: qual é a minha variável de interesse (quantitativa ou categórica)? Minha amostra é aleatória/probabilística? Qual é o tamanho da minha amostra?
* **Hipóteses**: definir H0 e Ha.
* **Estatística-teste**: Calcule a estatística teste (seja ela Z ou t) para a sua estimativa
* **Valor p**: qual é o peso da evidência contra a sua H0?
* **Conclusão**: relate a sua estimativa, estatística-teste, valor p e tome uma decisão formal sobre a rejeição ou não de H0.

**1. Vamos começar testando a hipótese de que a proporção de candidaturas do sexo feminino é menor ou igual a 30% (limite legal mínimo para candidaturas, nas eleições proporcionais, por chapa), sob um nível de significância de 10%.**

Sendo assim, nossa variável de interesse é o gênero dos candidatos, uma variável categórica. Nossa amostra foi estratificada por cargo disputado e grau de instrução dos candidatos, com n = 287.

A hipótese que desejamos testar é se a proporção de candidaturas femininas é menor ou igual a 30% do total. Ou seja, H0: Proporcao_Mulheres <= 0.3 e Ha: Proporcao_Mulheres > 0.3.

```
n_mulheres <- table(amostra_tse$DS_GENERO)[[1]]

prop.test(n_mulheres, n = 287, p = 0.3, alternative = "greater", conf.level = 0.90, correct = F)

#	1-sample proportions test without continuity correction
#
#data:  n_mulheres out of 287, null probability 0.3
#X-squared = 0.61739, df = 1, p-value = 0.784
#alternative hypothesis: true p is greater than 0.3
#90 percent confidence interval:
# 0.2461588 1.0000000
#sample estimates:
#        p 
#0.2787456 
```

Nosso teste revelou que não podemos rejeitar a H0 de que a proporção de candidaturas de mulheres em 2018 é menor ou igual a 0.30 (30% das candidaturas). Isso porque o p-valor desse teste revela um número bastante alto, p-valor = 0.784 (isto é, a chance de cometermos um erro de tipo I é altíssima, caso rejeitemos a hipótese nula), bastante superior ao alpha de 0.10 que colocamos como threshold para avaliar a H0. Além disso, nossa estimativa do parâmetro populacional (0.278) está na área da não rejeição de H0, bem como seu intervalo de confiança.

**2. Compare o resultado do nosso teste de hipótese com a realidade das candidaturas de 2018. Nossa decisão a partir do teste de hipótese foi acertada ou cometemos algum erro? Caso tenhamos cometido algum erro, ele é de Tipo I ou Tipo II?**

Contudo, se observássemos a proporção de candidaturas de mulheres em nossa população, vemos que ela é superior a 0.30 (sendo 0.316). Ou seja, apesar do nosso teste não ter sido capaz de rejeitar a H0, na realidade H0 deveria ter sido rejeitada. Sendo assim, cometemos um erro de Tipo II ao não rejeitarmos uma H0 que na realidade é falsa.

```
prop.table(table(banco_tse$DS_GENERO))
```

**3. Em seguida, utilizando nossa amostra do Atlas do Desenvolvimento Humano, vamos testar a hipótese de que o percentual de pobres em 2010 nos municípios brasileiros é menor ou igual que 20%, com um nível de significância de 5%.**

Iniciando nosso teste de hipótese, verificamos que a nossa variável de interesse é quantitativa (percentual de pobres), que nossa amostra é estratificada por região com aleatorização simples dentro dos estratos e de tamanho n = 111.

Nossa H0 portanto é H0: Percentual_Pobres <= 20 e Ha: Percentual_Pobres > 20.

```{r}
t.test(amostra_altas$pobres_10, alternative = "greater", mu = 20)

#One Sample t-test
#
#data:  amostra_altas$pobres_10
#t = 2.7387, df = 276, p-value = 0.003285
#alternative hypothesis: true mean is greater than 20
#95 percent confidence interval:
# 21.1808     Inf
#sample estimates:
#mean of x 
# 22.97144  
```

Nosso teste revelou podemos rejeitar a H0 de que a média do percentual de pobres nos municípios brasileiros em 2010 é menor ou igual a 20% da população. Isso porque o p-valor desse teste revela um número baixo, p-valor = 0.003 (isto é, a chance de cometermos um erro de tipo I é baixa, de menos de 1%), inferior ao alpha de 0.05 que colocamos como threshold para avaliar a H0. Além disso, nossa estimativa do parâmetro populacional (22,97%) está na área de rejeição de H0, bem como seu intervalo de confiança, cujo limite inferior está em 21,18%.

**4. Compare o resultado do nosso teste de hipótese com a realidade do percentual de pobres em todos os municípios brasileiros no ano de 2010. Nossa decisão a partir do teste de hipótese foi acertada ou cometemos algum erro? Caso tenhamos cometido algum erro, ele é de Tipo I ou Tipo II?**

```
mean(banco_atlas$pobres_10, na.rm = T)
```

Ao rejeitarmos H0 nesta situação não estamos cometendo nenhum erro, pois na realidade a média do percentual de pobres na população brasileira é maior que 20%, corroborando nossa Ha.
