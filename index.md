---
title: Introdução
date: '2017-01-19'
---





> "(...) The fact that data science exists as a field is a colossal failure of statistics. To me, [what I do] is what statistics is all about. It is gaining insight from data using modelling and visualization. Data munging and manipulation is hard and statistics has just said that’s not our domain."
> 
> Hadley Wickham


## Pacotes `dplyr` e `tidyr`

A transformação de dados é uma tarefa dolorosa e demorada, tomando muitas vezes a maior parte do tempo de uma análise estatística.

O `dplyr` é um dos pacotes mais úteis para realizar transformação de dados, aliando simplicidade e eficiência de uma forma elegante. Os scripts em `R` que fazem uso inteligente dos verbos `dplyr` e as facilidades do operador _pipe_ tendem a ficar mais legíveis e organizados, sem perder velocidade de execução.

Por ser um pacote que se propõe a realizar um dos trabalhos mais árduos da análise estatística, e por atingir esse objetivo de forma elegante, eficaz e eficiente, o `dplyr` pode ser considerado como uma revolução no `R`.

### Trabalhando com `tibble`s

A `tibble` nada mais é do que um `data.frame`, mas com um método de impressão mais adequado. Outras diferenças podem ser estudadas [neste link](http://r4ds.had.co.nz/tibbles.html).

Vamos assumir que temos a seguinte base de dados:




```
## # A tibble: 35,977 × 57
##                         arq_pag id_pag                             arq
##                           <chr>  <int>                           <chr>
## 1  data-raw/pags/pag_00609.html      3 data-raw/pessoas_pjs/10000.html
## 2  data-raw/pags/pag_00107.html     12 data-raw/pessoas_pjs/10001.html
## 3  data-raw/pags/pag_00056.html     15 data-raw/pessoas_pjs/10002.html
## 4  data-raw/pags/pag_00057.html      1 data-raw/pessoas_pjs/10003.html
## 5  data-raw/pags/pag_02314.html     15 data-raw/pessoas_pjs/10004.html
## 6  data-raw/pags/pag_00057.html      2 data-raw/pessoas_pjs/10005.html
## 7  data-raw/pags/pag_00280.html     13 data-raw/pessoas_pjs/10006.html
## 8  data-raw/pags/pag_00057.html      3 data-raw/pessoas_pjs/10007.html
## 9  data-raw/pags/pag_02307.html     10 data-raw/pessoas_pjs/10008.html
## 10 data-raw/pags/pag_01290.html      9 data-raw/pessoas_pjs/10009.html
## # ... with 35,967 more rows, and 54 more variables: id_condenacao <int>,
## #   id_processo <int>, id_pessoa <int>, tipo_pena <chr>, dt_pena <date>,
## #   assunto_cod_1 <int>, assunto_cod_2 <int>, assunto_cod_3 <int>,
## #   assunto_cod_4 <int>, assunto_cod_5 <int>, assunto_nm_1 <chr>,
## #   assunto_nm_2 <chr>, assunto_nm_3 <chr>, assunto_nm_4 <chr>,
## #   assunto_nm_5 <chr>, teve_inelegivel <chr>, teve_multa <chr>,
## #   teve_pena <chr>, teve_perda_bens <chr>, teve_perda_cargo <chr>,
## #   teve_proibicao <chr>, teve_ressarcimento <chr>, teve_suspensao <chr>,
## #   vl_multa <dbl>, vl_perda_bens <dbl>, vl_ressarcimento <dbl>,
## #   duracao_pena <int>, duracao_proibicao <chr>, duracao_suspensao <chr>,
## #   de_pena <date>, de_proibicao <date>, de_suspensao <date>,
## #   ate_pena <date>, ate_proibicao <date>, ate_suspensao <date>,
## #   arq_pessoa <chr>, tipo_pessoa <chr>, nm_pessoa <chr>, sexo <chr>,
## #   publico <chr>, esfera <chr>, orgao <chr>, cargo <chr>, uf <chr>,
## #   cod <chr>, arq_processo <chr>, dt_cadastro <dttm>, n_processo <chr>,
## #   esfera_processo <chr>, tribunal <chr>, instancia <chr>,
## #   comarca_secao <chr>, vara_camara <chr>, dt_propositura <date>
```


```r
tidy_cnc
## # A tibble: 35,977 × 57
##                         arq_pag id_pag                             arq
##                           <chr>  <int>                           <chr>
## 1  data-raw/pags/pag_00609.html      3 data-raw/pessoas_pjs/10000.html
## 2  data-raw/pags/pag_00107.html     12 data-raw/pessoas_pjs/10001.html
## 3  data-raw/pags/pag_00056.html     15 data-raw/pessoas_pjs/10002.html
## 4  data-raw/pags/pag_00057.html      1 data-raw/pessoas_pjs/10003.html
## 5  data-raw/pags/pag_02314.html     15 data-raw/pessoas_pjs/10004.html
## 6  data-raw/pags/pag_00057.html      2 data-raw/pessoas_pjs/10005.html
## 7  data-raw/pags/pag_00280.html     13 data-raw/pessoas_pjs/10006.html
## 8  data-raw/pags/pag_00057.html      3 data-raw/pessoas_pjs/10007.html
## 9  data-raw/pags/pag_02307.html     10 data-raw/pessoas_pjs/10008.html
## 10 data-raw/pags/pag_01290.html      9 data-raw/pessoas_pjs/10009.html
## # ... with 35,967 more rows, and 54 more variables: id_condenacao <int>,
## #   id_processo <int>, id_pessoa <int>, tipo_pena <chr>, dt_pena <date>,
## #   assunto_cod_1 <int>, assunto_cod_2 <int>, assunto_cod_3 <int>,
## #   assunto_cod_4 <int>, assunto_cod_5 <int>, assunto_nm_1 <chr>,
## #   assunto_nm_2 <chr>, assunto_nm_3 <chr>, assunto_nm_4 <chr>,
## #   assunto_nm_5 <chr>, teve_inelegivel <chr>, teve_multa <chr>,
## #   teve_pena <chr>, teve_perda_bens <chr>, teve_perda_cargo <chr>,
## #   teve_proibicao <chr>, teve_ressarcimento <chr>, teve_suspensao <chr>,
## #   vl_multa <dbl>, vl_perda_bens <dbl>, vl_ressarcimento <dbl>,
## #   duracao_pena <int>, duracao_proibicao <chr>, duracao_suspensao <chr>,
## #   de_pena <date>, de_proibicao <date>, de_suspensao <date>,
## #   ate_pena <date>, ate_proibicao <date>, ate_suspensao <date>,
## #   arq_pessoa <chr>, tipo_pessoa <chr>, nm_pessoa <chr>, sexo <chr>,
## #   publico <chr>, esfera <chr>, orgao <chr>, cargo <chr>, uf <chr>,
## #   cod <chr>, arq_processo <chr>, dt_cadastro <dttm>, n_processo <chr>,
## #   esfera_processo <chr>, tribunal <chr>, instancia <chr>,
## #   comarca_secao <chr>, vara_camara <chr>, dt_propositura <date>
```

### As cinco funções principais do `dplyr`

- `filter`
- `mutate`
- `select`
- `arrange`
- `summarise`

### Características

- O _input_  é sempre uma `tibble`, e o _output_  é sempre um `tibble`.
- No primeiro argumento colocamos o `tibble`, e nos outros argumentos colocamos o que queremos fazer.
- A utilização é facilitada com o emprego do operador `%>%`

### Vantagens

- Utiliza `C` e `C++` por trás da maioria das funções, o que geralmente torna o código mais eficiente.
- Pode trabalhar com diferentes fontes de dados, como bases relacionais (SQL) e `data.table`.

### `select`

- Utilizar `starts_with(x)`, `contains(x)`, `matches(x)`, `one_of(x)`, etc.
- Possível colocar nomes, índices, e intervalos de variáveis com `:`.


```r
tidy_cnc %>% 
  select(id_condenacao, teve_multa, teve_pena, nm_pessoa)
## # A tibble: 35,977 × 4
##    id_condenacao teve_multa teve_pena                          nm_pessoa
##            <int>      <chr>     <chr>                              <chr>
## 1          10000       <NA>      <NA>            EDIMAR REZENDE DE SOUZA
## 2          10001       <NA>       sim ALEXANDER APARECIDO SALERI RIBEIRO
## 3          10002       <NA>       sim          AGENOR GENIVALDO DA SILVA
## 4          10003       <NA>       sim          AGENOR GENIVALDO DA SILVA
## 5          10004       <NA>       sim                   WAGNER JUNQUEIRA
## 6          10005       <NA>       sim          AGENOR GENIVALDO DA SILVA
## 7          10006        sim      <NA>        ARTUR FERNANDO ROCHA CORREA
## 8          10007       <NA>       sim          AGENOR GENIVALDO DA SILVA
## 9          10008        sim      <NA>              VITOR TERRA RODRIGUES
## 10         10009        sim      <NA>         JOSé LUIZ MARZULLO PATELLA
## # ... with 35,967 more rows
```


```r
tidy_cnc %>% 
  select(id_processo:tipo_pena, sexo)
## # A tibble: 35,977 × 4
##    id_processo id_pessoa           tipo_pena  sexo
##          <int>     <int>               <chr> <chr>
## 1         7618      8393 Trânsito em julgado     M
## 2         7619      8394 Trânsito em julgado     M
## 3         7620      8395 Trânsito em julgado     M
## 4         7621      8395 Trânsito em julgado     M
## 5         7621      8397 Trânsito em julgado     M
## 6         7623      8395 Trânsito em julgado     M
## 7         7622      8396     Órgão colegiado     M
## 8         7624      8395 Trânsito em julgado     M
## 9         7626      8399     Órgão colegiado     M
## 10        7627      1695     Órgão colegiado     M
## # ... with 35,967 more rows
```


```r
tidy_cnc %>% 
  select(n_processo, starts_with('teve_'))
## # A tibble: 35,977 × 9
##         n_processo teve_inelegivel teve_multa teve_pena teve_perda_bens
##              <chr>           <chr>      <chr>     <chr>           <chr>
## 1      04720038714             sim       <NA>      <NA>            <NA>
## 2    0472060112068             sim       <NA>       sim            <NA>
## 3    0472090235012             sim       <NA>       sim            <NA>
## 4    0472090241119             sim       <NA>       sim            <NA>
## 5    0472090241119             sim       <NA>       sim            <NA>
## 6    0472090258675             sim       <NA>       sim            <NA>
## 7   06310500019109            <NA>        sim      <NA>            <NA>
## 8    0472090258683             sim       <NA>       sim            <NA>
## 9   06311100001006            <NA>        sim      <NA>            <NA>
## 10 063109600013242            <NA>        sim      <NA>            <NA>
## # ... with 35,967 more rows, and 4 more variables: teve_perda_cargo <chr>,
## #   teve_proibicao <chr>, teve_ressarcimento <chr>, teve_suspensao <chr>
```

### `filter`

- Parecido com `subset`.
- Condições separadas por vírgulas é o mesmo que separar por `&`.


```r
tidy_cnc %>% 
  select(id_condenacao, nm_pessoa, uf) %>% 
  filter(uf == 'SP')
## # A tibble: 2,485 × 3
##    id_condenacao                 nm_pessoa    uf
##            <int>                     <chr> <chr>
## 1          10035              JOãO SANTANA    SP
## 2          10067    ROBERTO PIRES DA SILVA    SP
## 3          10069       AIRTON ANDRADE RAIS    SP
## 4          10070    EDMILSON SILVA DE LIMA    SP
## 5          10071 NEEMIAS MARIANO DE BARROS    SP
## 6          10089  DOUGLAS GURGEL DO AMARAL    SP
## 7          10091    LUIZ ANTONIO CAVALETTI    SP
## 8          10093        ERLEI LAGDEN FILHO    SP
## 9           1013          WALDEMAR CASSEZE    SP
## 10         10190   EDSON NERIS DE CARVALHO    SP
## # ... with 2,475 more rows
```


```r
library(lubridate)
## Loading required package: methods
## 
## Attaching package: 'lubridate'
## The following object is masked from 'package:base':
## 
##     date
tidy_cnc %>% 
  select(id_condenacao, nm_pessoa, uf, dt_propositura) %>% 
  filter(uf %in% c('SP', 'MG') &
         (day(dt_propositura) >= 29 | day(dt_propositura) < 25))
## # A tibble: 2,741 × 4
##    id_condenacao                 nm_pessoa    uf dt_propositura
##            <int>                     <chr> <chr>         <date>
## 1          10035              JOãO SANTANA    SP     2004-09-21
## 2          10067    ROBERTO PIRES DA SILVA    SP     2000-08-04
## 3          10069       AIRTON ANDRADE RAIS    SP     2007-11-05
## 4           1006      HéLIO FERRAZ PEREIRA    MG     2001-10-29
## 5          10070    EDMILSON SILVA DE LIMA    SP     2007-11-05
## 6          10071 NEEMIAS MARIANO DE BARROS    SP     2007-11-05
## 7          10089  DOUGLAS GURGEL DO AMARAL    SP     2007-10-05
## 8          10091    LUIZ ANTONIO CAVALETTI    SP     2003-06-11
## 9          10093        ERLEI LAGDEN FILHO    SP     2003-06-11
## 10          1013          WALDEMAR CASSEZE    SP     2007-10-14
## # ... with 2,731 more rows
```



```r
library(stringr)
tidy_cnc %>% 
  select(nm_pessoa) %>% 
  filter(str_detect(nm_pessoa, '^[gG]'))
## # A tibble: 1,399 × 1
##                       nm_pessoa
##                           <chr>
## 1      GABRIEL BARREIRA FEITOZA
## 2     GEISILON NUNES DE ALMEIDA
## 3         GNAILDA SAMPAIO LOPES
## 4           GILSON SANTOS COSTA
## 5      GEDIANY DE SOUZA MODESTO
## 6      GERALDO DE SOUZA MACHADO
## 7                GERSON GIANINI
## 8  GIUSEPE ANGELOS BARBOSA LIMA
## 9    GERSON GONçALVES CHICOUREL
## 10   GEOVANE MEDEIROS DE AGUIAR
## # ... with 1,389 more rows
```

### `mutate`

- Parecido com `transform`, mas aceita várias novas colunas iterativamente.
- Novas variáveis devem ter o mesmo `length` que o `nrow` do bd oridinal ou `1`.


```r
tidy_cnc %>% 
  select(id_condenacao, dt_propositura, vl_multa) %>% 
  mutate(ano_propositura = year(dt_propositura),
         vl_multa = log10(vl_multa))
## # A tibble: 35,977 × 4
##    id_condenacao dt_propositura vl_multa ano_propositura
##            <int>         <date>    <dbl>           <dbl>
## 1          10000     2004-07-06       NA            2004
## 2          10001     2003-10-16       NA            2003
## 3          10002     2009-07-01       NA            2009
## 4          10003     2009-07-29       NA            2009
## 5          10004     2009-07-29       NA            2009
## 6          10005     2009-10-30       NA            2009
## 7          10006     2005-11-07 4.636774            2005
## 8          10007     2009-10-30       NA            2009
## 9          10008     2011-01-12 4.021784            2011
## 10         10009     2006-07-24 5.102886            2006
## # ... with 35,967 more rows
```

### `arrange`

- Simplesmente ordena de acordo com as opções.
- Utilizar `desc` para ordem decrescente.


```r
library(stringr)
tidy_cnc %>% 
  select(id_condenacao, dt_propositura, vl_multa, nm_pessoa) %>% 
  mutate(ano_propositura = year(dt_propositura),
         log_multa = log10(vl_multa)) %>% 
  arrange(desc(vl_multa))
## # A tibble: 35,977 × 6
##    id_condenacao dt_propositura     vl_multa
##            <int>         <date>        <dbl>
## 1          31337     2002-05-17 111111111111
## 2          34186     2012-10-31    101947537
## 3          24150     2013-11-04    100731322
## 4           9057     2008-12-09     70225149
## 5           9058     2008-12-09     70225149
## 6           9061     2008-12-09     70225149
## 7          32910     1996-06-20     54662281
## 8          32939     1996-06-20     54642412
## 9           1751     2000-11-20     43708242
## 10          7966     2001-08-27     32606320
## # ... with 35,967 more rows, and 3 more variables: nm_pessoa <chr>,
## #   ano_propositura <dbl>, log_multa <dbl>
```

### `summarise`

- Retorna um vetor de tamanho `1` a partir de uma conta com as variáveis.
- Geralmente é utilizado em conjunto com `group_by`.
- Algumas funções importantes: `n()`, `n_distinct()`.


```r
tidy_cnc %>% 
  select(id_condenacao, dt_propositura, vl_multa, nm_pessoa, tribunal) %>% 
  mutate(ano_propositura = year(dt_propositura),
         log_multa = log10(vl_multa)) %>% 
  group_by(tribunal) %>% 
  summarise(n = n(), vl_medio = mean(vl_multa, na.rm = TRUE)) %>% 
  filter(n > 5) %>% 
  arrange(desc(vl_medio))
## # A tibble: 34 × 3
##                                                     tribunal     n
##                                                        <chr> <int>
## 1                 Tribunal de Justiça do Estado de São Paulo  3594
## 2  Tribunal de Justiça do Distrito Federal e dos Territórios 10162
## 3            Tribunal de Justiça do Estado do Rio de Janeiro   269
## 4                      Tribunal de Justiça do Estado do Acre    73
## 5                  Tribunal de Justiça do Estado do Maranhão   373
## 6                     Tribunal Regional Federal da 3ª Região   159
## 7              Tribunal de Justiça do Estado de Minas Gerais  2630
## 8                   Tribunal de Justiça do Estado de Roraima    10
## 9                   Tribunal de Justiça do Estado da Paraíba   101
## 10                    Tribunal de Justiça do Estado da Bahia    27
## # ... with 24 more rows, and 1 more variables: vl_medio <dbl>
```


```r
tidy_cnc %>% 
  count(tribunal, sort = TRUE) %>% 
  mutate(prop = n / sum(n), prop = scales::percent(prop))
## # A tibble: 34 × 3
##                                                     tribunal     n  prop
##                                                        <chr> <int> <chr>
## 1  Tribunal de Justiça do Distrito Federal e dos Territórios 10162 28.2%
## 2                    Tribunal de Justiça do Estado do Paraná  6246 17.4%
## 3            Tribunal de Justiça do Estado de Santa Catarina  4929 13.7%
## 4                 Tribunal de Justiça do Estado de São Paulo  3594 10.0%
## 5              Tribunal de Justiça do Estado de Minas Gerais  2630  7.3%
## 6                     Tribunal Regional Federal da 5ª Região  1848  5.1%
## 7                     Tribunal Regional Federal da 1ª Região  1249  3.5%
## 8         Tribunal de Justiça do Estado do Rio Grande do Sul   803  2.2%
## 9                  Tribunal de Justiça do Estado de Rondônia   765  2.1%
## 10                    Tribunal de Justiça do Estado de Goiás   523  1.5%
## # ... with 24 more rows
```

### `gather`

- "Empilha" o banco de dados


```r
library(tidyr)
tidy_cnc %>% 
  select(id_condenacao, starts_with('assunto_nm')) %>% 
  gather(key, value, -id_condenacao) %>% 
  arrange(id_condenacao)
## # A tibble: 179,885 × 3
##    id_condenacao          key                                   value
##            <int>        <chr>                                   <chr>
## 1              1 assunto_nm_1 Violação aos Princípios Administrativos
## 2              1 assunto_nm_2                                    <NA>
## 3              1 assunto_nm_3                                    <NA>
## 4              1 assunto_nm_4                                    <NA>
## 5              1 assunto_nm_5                                    <NA>
## 6              2 assunto_nm_1 Violação aos Princípios Administrativos
## 7              2 assunto_nm_2                                    <NA>
## 8              2 assunto_nm_3                                    <NA>
## 9              2 assunto_nm_4                                    <NA>
## 10             2 assunto_nm_5                                    <NA>
## # ... with 179,875 more rows
```

### `spread`

- "Joga" uma variável nas colunas
- É essencialmente a função inversa de `gather`


```r
tidy_cnc %>% 
  select(id_condenacao, starts_with('assunto_nm')) %>% 
  gather(key, value, -id_condenacao) %>% 
  arrange(id_condenacao) %>% 
  spread(key, value)
## # A tibble: 35,977 × 6
##    id_condenacao                            assunto_nm_1   assunto_nm_2
## *          <int>                                   <chr>          <chr>
## 1              1 Violação aos Princípios Administrativos           <NA>
## 2              2 Violação aos Princípios Administrativos           <NA>
## 3              3                          Dano ao Erário           <NA>
## 4              4                          Dano ao Erário           <NA>
## 5              5                          Dano ao Erário           <NA>
## 6              6                          Dano ao Erário           <NA>
## 7              7 Violação aos Princípios Administrativos Dano ao Erário
## 8              8                          Dano ao Erário           <NA>
## 9              9                          Dano ao Erário           <NA>
## 10            10                          Dano ao Erário           <NA>
## # ... with 35,967 more rows, and 3 more variables: assunto_nm_3 <chr>,
## #   assunto_nm_4 <chr>, assunto_nm_5 <chr>
```

### Funções auxiliares

- `unite` junta duas ou mais colunas usando algum separador (`_`, por exemplo).
- `separate` faz o inverso de `unite`, e uma coluna em várias usando um separador.

### Um pouco mais de transformação de dados

- Para juntar tabelas, usar `inner_join`, `left_join`, `anti_join`, etc.
- Para realizar operações mais gerais, usar `do`.
- Para retirar duplicatas, utilizar `distinct`.







<script src="https://cdn.datacamp.com/datacamp-light-latest.min.js"></script>




<script src="https://cdn.datacamp.com/datacamp-light-latest.min.js"></script>



1. Calcule o número de ouro no R.

$$
\frac{1 + \sqrt{5}}{2}
$$

<div data-datacamp-exercise data-height="300" data-encoded="true">eyJsYW5ndWFnZSI6InIiLCJzYW1wbGUiOiIjIERpZ2l0ZSBhIGV4cHJlc3NcdTAwZTNvIHF1ZSBjYWxjdWxhIG8gblx1MDBmYW1lcm8gZGUgb3Vyby4iLCJzb2x1dGlvbiI6IigxICsgc3FydCg1KSkvMiIsInNjdCI6InRlc3Rfb3V0cHV0X2NvbnRhaW5zKFwiMS42MTgwMzRcIiwgaW5jb3JyZWN0X21zZyA9IFwiVGVtIGNlcnRlemEgZGUgcXVlIGluZGljb3UgYSBleHByZXNzXHUwMGUzbyBjb3JyZXRhbWVudGU/XCIpXG5zdWNjZXNzX21zZyhcIkNvcnJldG8hXCIpIn0=</div>






