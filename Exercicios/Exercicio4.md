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

**2. Compare o resultado do nosso teste de hipótese com a realidade das candidaturas de 2018. Nossa decisão a partir do teste de hipótese foi acertada ou cometemos algum erro? Caso tenhamos cometido algum erro, ele é de Tipo I ou Tipo II?**

**3. Em seguida, utilizando nossa amostra do Atlas do Desenvolvimento Humano, vamos testar a hipótese de que o percentual de pobres em 2010 nos municípios brasileiros é menor ou igual que 20%, com um nível de significância de 5%.**

**4. Compare o resultado do nosso teste de hipótese com a realidade do percentual de pobres em todos os municípios brasileiros no ano de 2010. Nossa decisão a partir do teste de hipótese foi acertada ou cometemos algum erro? Caso tenhamos cometido algum erro, ele é de Tipo I ou Tipo II?**
