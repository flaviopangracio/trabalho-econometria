## Base de dados

A base de dados contém diversas informações sobre as 853 cidades
mineiras. Precisamos de algumas informações relacionadas ao crime nessas
cidades.

    ## Carregando a base de dados com informações sobre cidades mineiras de um arquivo CSV.
    base_crime <- read.csv("base_crime.csv") |>
      tibble()

    ## Carregando o nome dos municipios para cruzar com a base de dados.
    cidades <- read.csv("cidades.csv") |>
      tibble()

    ## Cruzando os dados e extraíndo variáveis que utilizaremos posteriormente.

    base_raw <- readxl::read_xlsx("base_crime.xlsx", sheet = "Painel")

    ## New names:
    ## * `Tx mort doen cer-vasc 45-59` -> `Tx mort doen cer-vasc 45-59...37`
    ## * `Tx mort doen cer-vasc 45-59` -> `Tx mort doen cer-vasc 45-59...38`

    dados_pib <- base_raw |>
      rename(c("municipio" = "município", "pib" = "PIB per capita")) |> 
      select("municipio", "ano", "pib") |>
      inner_join(cidades, c("municipio" = "codigo")) |>
      select("ano", "nome", "pib") |>
      rename("municipio" = "nome")

    base_crime_joined <- inner_join(base_crime, cidades, c("municipio" = "codigo")) |>
      select(
        "ano",
        "nome", 
        "populacao",
        "homicidio",
        "gastos_educacao",
        "renda_setor_formal",
        "gastos_seguranca_publica"
      ) |>
      rename("municipio" = "nome")

## Sobre as variáveis do modelo:

-   homicidio (*double*): Taxa de homicídio doloso para cada 100
    habitantes
-   gastos\_educacao (*double*): Gasto per capita com educação
-   renda\_setor\_formal (*double*): Rendimento per capita do setor
    formal
-   gastos\_seguranca\_publica (*double*): Gasto per capita com
    segurança pública

## Análise descritiva

    ## Filtrando dados de 2017
    base_crime_2017 <- base_crime_joined |> filter(ano == 2017)

    ## Análise descritiva das variáveis numéricas
    modelsummary::datasummary_skim(base_crime_2017[4:7])

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
Unique (#)
</th>
<th style="text-align:right;">
Missing (%)
</th>
<th style="text-align:right;">
Mean
</th>
<th style="text-align:right;">
SD
</th>
<th style="text-align:right;">
Min
</th>
<th style="text-align:right;">
Median
</th>
<th style="text-align:right;">
Max
</th>
<th style="text-align:right;">
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
homicidio
</td>
<td style="text-align:right;">
485
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
15.3
</td>
<td style="text-align:right;">
18.9
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
10.2
</td>
<td style="text-align:right;">
151.2
</td>
<td style="text-align:right;">
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" class="svglite" width="48.00pt" height="12.00pt" viewBox="0 0 48.00 12.00">
<defs>
<style type="text/css">
    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {
      fill: none;
      stroke: #000000;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-miterlimit: 10.00;
    }
    .svglite text {
      white-space: pre;
    }
  </style>
</defs><rect width="100%" height="100%" style="stroke: none; fill: none;"></rect><defs><clipPath id="cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw"><rect x="0.00" y="0.00" width="48.00" height="12.00"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw)">
</g><defs><clipPath id="cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw"><rect x="0.00" y="2.88" width="48.00" height="9.12"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw)"><rect x="1.78" y="3.22" width="2.94" height="8.44" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="4.72" y="8.34" width="2.94" height="3.32" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="7.65" y="9.34" width="2.94" height="2.32" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="10.59" y="10.36" width="2.94" height="1.30" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="13.53" y="10.88" width="2.94" height="0.78" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="16.47" y="11.30" width="2.94" height="0.36" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="19.41" y="11.44" width="2.94" height="0.22" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="22.35" y="11.54" width="2.94" height="0.12" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="25.29" y="11.58" width="2.94" height="0.080" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="28.22" y="11.62" width="2.94" height="0.040" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="31.16" y="11.60" width="2.94" height="0.060" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="34.10" y="11.66" width="2.94" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="37.04" y="11.66" width="2.94" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="39.98" y="11.66" width="2.94" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="42.92" y="11.66" width="2.94" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="45.85" y="11.64" width="2.94" height="0.020" style="stroke-width: 0.38; fill: #000000;"></rect></g>
</svg>
</td>
</tr>
<tr>
<td style="text-align:left;">
gastos\_educacao
</td>
<td style="text-align:right;">
844
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
645.6
</td>
<td style="text-align:right;">
260.8
</td>
<td style="text-align:right;">
212.9
</td>
<td style="text-align:right;">
594.8
</td>
<td style="text-align:right;">
3659.3
</td>
<td style="text-align:right;">
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" class="svglite" width="48.00pt" height="12.00pt" viewBox="0 0 48.00 12.00">
<defs>
<style type="text/css">
    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {
      fill: none;
      stroke: #000000;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-miterlimit: 10.00;
    }
    .svglite text {
      white-space: pre;
    }
  </style>
</defs><rect width="100%" height="100%" style="stroke: none; fill: none;"></rect><defs><clipPath id="cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw"><rect x="0.00" y="0.00" width="48.00" height="12.00"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw)">
</g><defs><clipPath id="cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw"><rect x="0.00" y="2.88" width="48.00" height="9.12"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw)"><rect x="-0.97" y="8.09" width="6.45" height="3.57" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="5.48" y="3.22" width="6.45" height="8.44" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="11.93" y="10.79" width="6.45" height="0.87" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="18.38" y="11.60" width="6.45" height="0.061" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="24.82" y="11.66" width="6.45" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="31.27" y="11.65" width="6.45" height="0.015" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="37.72" y="11.66" width="6.45" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="44.17" y="11.65" width="6.45" height="0.015" style="stroke-width: 0.38; fill: #000000;"></rect></g>
</svg>
</td>
</tr>
<tr>
<td style="text-align:left;">
renda\_setor\_formal
</td>
<td style="text-align:right;">
849
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1632.5
</td>
<td style="text-align:right;">
383.5
</td>
<td style="text-align:right;">
232.8
</td>
<td style="text-align:right;">
1530.1
</td>
<td style="text-align:right;">
5046.6
</td>
<td style="text-align:right;">
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" class="svglite" width="48.00pt" height="12.00pt" viewBox="0 0 48.00 12.00">
<defs>
<style type="text/css">
    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {
      fill: none;
      stroke: #000000;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-miterlimit: 10.00;
    }
    .svglite text {
      white-space: pre;
    }
  </style>
</defs><rect width="100%" height="100%" style="stroke: none; fill: none;"></rect><defs><clipPath id="cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw"><rect x="0.00" y="0.00" width="48.00" height="12.00"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw)">
</g><defs><clipPath id="cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw"><rect x="0.00" y="2.88" width="48.00" height="9.12"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw)"><rect x="-0.37" y="11.64" width="4.62" height="0.021" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="4.25" y="11.66" width="4.62" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="8.86" y="4.27" width="4.62" height="7.39" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="13.48" y="3.22" width="4.62" height="8.44" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="18.09" y="10.19" width="4.62" height="1.47" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="22.71" y="11.39" width="4.62" height="0.27" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="27.33" y="11.43" width="4.62" height="0.23" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="31.94" y="11.60" width="4.62" height="0.063" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="36.56" y="11.66" width="4.62" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="41.18" y="11.66" width="4.62" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="45.79" y="11.64" width="4.62" height="0.021" style="stroke-width: 0.38; fill: #000000;"></rect></g>
</svg>
</td>
</tr>
<tr>
<td style="text-align:left;">
gastos\_seguranca\_publica
</td>
<td style="text-align:right;">
515
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
5.8
</td>
<td style="text-align:right;">
10.9
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
3.7
</td>
<td style="text-align:right;">
168.3
</td>
<td style="text-align:right;">
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" class="svglite" width="48.00pt" height="12.00pt" viewBox="0 0 48.00 12.00">
<defs>
<style type="text/css">
    .svglite line, .svglite polyline, .svglite polygon, .svglite path, .svglite rect, .svglite circle {
      fill: none;
      stroke: #000000;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-miterlimit: 10.00;
    }
    .svglite text {
      white-space: pre;
    }
  </style>
</defs><rect width="100%" height="100%" style="stroke: none; fill: none;"></rect><defs><clipPath id="cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw"><rect x="0.00" y="0.00" width="48.00" height="12.00"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwwLjAwfDEyLjAw)">
</g><defs><clipPath id="cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw"><rect x="0.00" y="2.88" width="48.00" height="9.12"></rect></clipPath></defs><g clip-path="url(#cpMC4wMHw0OC4wMHwyLjg4fDEyLjAw)"><rect x="1.78" y="3.22" width="5.28" height="8.44" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="7.06" y="11.45" width="5.28" height="0.22" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="12.34" y="11.58" width="5.28" height="0.083" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="17.62" y="11.66" width="5.28" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="22.91" y="11.65" width="5.28" height="0.010" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="28.19" y="11.64" width="5.28" height="0.021" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="33.47" y="11.66" width="5.28" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="38.75" y="11.66" width="5.28" height="0.00" style="stroke-width: 0.38; fill: #000000;"></rect><rect x="44.04" y="11.65" width="5.28" height="0.010" style="stroke-width: 0.38; fill: #000000;"></rect></g>
</svg>
</td>
</tr>
</tbody>
</table>

## Tratamento dos dados

Inicialmente, vamos tentar remover *outliers* que possam viesar nosso
modelo.

Removendo outliers baseado na análise dos *boxplots* e selecionando uma
amostra com 95% dos dados, para analisar o impacto que pequenas
variações na amostra geram na estimação do modelo.

    # Removendo outliers baseado na análise do boxplot

    # Ao final, selecionamos aleatoriamente uma amostra de 95% dos dados,
    # para verificar como os parâmetros do se comportam fazendo pequenas alterações na amostra.

    base_final <- base_crime_joined |>
      filter(ano == 2017) |>
      filter(gastos_seguranca_publica > 0) |>
      filter(homicidio > 0) |>
      filter(gastos_educacao > 200 & gastos_educacao < 1500) |>
      filter(renda_setor_formal > 1000 & renda_setor_formal < 2500) |>
      sample_frac(0.95, replace = FALSE)

    ##  write.csv("backup.csv", base_final)

    backup <- read.csv("backup.csv")

Ao final, temos uma amostra de 384 cidades mineiras.

## O modelo

Buscamos entender se o log da taxa de homicídios (homicídios para cada
100 mil habitantes) é explicado pela combinação de: gasto per capita com
segurança pública, gasto per capita com educação e renda média do setor
formal.

    model <- lm(formula = "log(homicidio) ~ gastos_seguranca_publica + renda_setor_formal + gastos_educacao", data = backup)

    summary(model)

    ## 
    ## Call:
    ## lm(formula = "log(homicidio) ~ gastos_seguranca_publica + renda_setor_formal + gastos_educacao", 
    ##     data = backup)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.71773 -0.44120 -0.00946  0.48123  2.11435 
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)               3.2372364  0.2217455  14.599  < 2e-16 ***
    ## gastos_seguranca_publica -0.0124158  0.0043113  -2.880 0.004204 ** 
    ## renda_setor_formal       -0.0004674  0.0001271  -3.678 0.000269 ***
    ## gastos_educacao           0.0009867  0.0001870   5.277 2.21e-07 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6651 on 380 degrees of freedom
    ## Multiple R-squared:  0.1092, Adjusted R-squared:  0.1022 
    ## F-statistic: 15.53 on 3 and 380 DF,  p-value: 1.507e-09

## Testando a presença de multicolinearidade

Por do cálculo do Fator de Inflacionamento da variância, podemos
verificar se há multicolinearidade entre as variáveis explicativas,
valores superiores ou iguais a 10 indica a presença de
multicolinearidade prejudicial.

    vif(model)

    ## gastos_seguranca_publica       renda_setor_formal          gastos_educacao 
    ##                 1.053530                 1.036118                 1.030252

## Testando a presença de autocorrelação residual

Podemos realizar o teste Durbin-Watson para detectar autocorrelação
residual:

-   *H*<sub>0</sub>: ausência de autocorrelação
-   *H*<sub>1</sub>: autocorrelação serial de primeira ordem

<!-- -->

    dwtest(model)

    ## 
    ##  Durbin-Watson test
    ## 
    ## data:  model
    ## DW = 1.873, p-value = 0.1062
    ## alternative hypothesis: true autocorrelation is greater than 0

Como o p-valor = 0.1062, não podemos rejeitar a hipótese nula (ausência
de autorrelação).

## Testando a presença de heterocedasticidade nos residuos

Utilizamos o teste Breuch-Pagan para identificar heterocedasticidades no
resíduos.

-   *H*<sub>0</sub>: variância constante
-   *H*<sub>1</sub>: variância não-constante

<!-- -->

    bptest(model)

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  model
    ## BP = 4.1559, df = 3, p-value = 0.2451

Como o p-value do teste é igual a 0.2451, não podemos rejeitar a
hipótese nula (variância constante)

## Testando a normalidade dos residuos

Por meio do teste de normalidade Shapiro-Wilk, podemos testar os
resíduos são normalmente distribuídos.

-   *H*<sub>0</sub>: Erros normalmente distribuídos
-   *H*<sub>1</sub>: Erros não são normalmente distribuídos

<!-- -->

    residuos <- model$residuals

    shapiro.test(residuos)

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  residuos
    ## W = 0.99447, p-value = 0.181

Como o p-value = 0.181, não podemos rejeitar a hipótese nula (de que os
erros são distribuídos normalmente)

## Testando endogeneidade

Se descrevermos o modelo de equações simultâneas como:

*l**o**g*(*H*)<sub>*i*</sub> = *β*<sub>0</sub> + *β*<sub>1</sub>*S*<sub>*i*</sub> + *β*<sub>2</sub>*E*<sub>*i*</sub> + *β*<sub>3</sub>*R*<sub>*i*</sub> + *μ*<sub>*i*</sub>

*S*<sub>*i*</sub> = *α*<sub>0</sub> + *α*<sub>1</sub>*l**o**g*(*H*)<sub>*i*</sub> + *α*<sub>2</sub>*P* + *μ*<sub>2*i*</sub>

em que *l**o**g*(*H*)<sub>*i*</sub>= logaritmo da taxa de homicídio
observada, *S*<sub>*i*</sub>= gasto per capita com segurança pública
observada, *E*<sub>*i*</sub>= gasto per capita com educação observada,
*R*<sub>*i*</sub>= renda per capita do setor formal observada e
*μ*<sub>*i*</sub> o resíduo observado.

Utilizamos *S*<sub>*i*</sub> = *l**o**g*(*H*)<sub>*i*</sub> + *P* como
uma equação auxiliar do modelo.

Podemos verificar se *S*<sub>*i*</sub> é endógena, ou seja, se
*S*<sub>*i*</sub> é correlacionada com o resíduo *μ*<sub>*i*</sub>.

Regredindo, por MQO, a variável explicativa endógena, gasto per capita
com segurança pública, em função das varíveis exógenas
*E*<sub>*i*</sub>, *R*<sub>*i*</sub> e do PIB per capita *P*, variável
assumida como exógena, excluída do modelo, obtemos os valores estimados
de $\\hat{S\_i}$ e do resíduo $\\hat{v\_i}$, definidos por (1) e (2):

$$
S\_i = \\hat{\\beta\_0} + \\hat{\\beta\_1} E  + \\hat{\\beta\_2} R + \\hat{\\beta\_3} P + \\hat{v\_i}     (1)
$$

$$
S\_i = \\hat{S\_i} + \\hat{v\_i}   (2)
$$

    ## Enriquecendo base com dados do PIB per capita das cidades
    base_final_pib <- backup |>
      inner_join(dados_pib, c("municipio" = "municipio", "ano" = "ano"))

    ## Estimando (1)
    model_s <- lm(gastos_seguranca_publica ~ gastos_educacao + renda_setor_formal + pib, base_final_pib)

    summary(model_s)

    ## 
    ## Call:
    ## lm(formula = gastos_seguranca_publica ~ gastos_educacao + renda_setor_formal + 
    ##     pib, data = base_final_pib)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -14.608  -3.276  -1.556   1.203  75.705 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)        9.968e-01  2.843e+00   0.351    0.726    
    ## gastos_educacao    3.621e-03  2.219e-03   1.632    0.104    
    ## renda_setor_formal 4.672e-04  1.730e-03   0.270    0.787    
    ## pib                1.588e-04  3.452e-05   4.601 5.73e-06 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 7.702 on 380 degrees of freedom
    ## Multiple R-squared:  0.1009, Adjusted R-squared:  0.09381 
    ## F-statistic: 14.22 on 3 and 380 DF,  p-value: 8.46e-09

    ## Gasto per capita com segurança pública estimado
    s_estimado <- model_s$fitted.values

    residuo_estimado <- model_s$residuals

Agora, retornamos ao modelo estrutural e regredimos
*l**o**g*(*H*)<sub>*i*</sub> em função dos valores estimados
$\\hat{S\_i}$ e do resíduo estimado $\\hat{v\_i}$:

$$
log(H)\_i = \\hat{\\beta\_0} + \\hat{\\beta\_1} \\hat{S\_i} + \\hat{\\beta\_2} \\hat{v\_i} + \\hat{u\_{2i}}
$$

    teste_endogeneidade <- lm(log(homicidio) ~ s_estimado + residuo_estimado, base_final_pib)

    summary(teste_endogeneidade)

    ## 
    ## Call:
    ## lm(formula = log(homicidio) ~ s_estimado + residuo_estimado, 
    ##     data = base_final_pib)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -2.2634 -0.4387  0.0463  0.4447  1.9723 
    ## 
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       3.200874   0.096984  33.004   <2e-16 ***
    ## s_estimado       -0.035728   0.013805  -2.588   0.0100 *  
    ## residuo_estimado -0.008899   0.004625  -1.924   0.0551 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6943 on 381 degrees of freedom
    ## Multiple R-squared:  0.02657,    Adjusted R-squared:  0.02147 
    ## F-statistic: 5.201 on 2 and 381 DF,  p-value: 0.005911

Como $\\hat{\\beta\_2}$ é estatisticamente diferente de zero, rejeitamos
a hipótese nula (de que não há simultaneidade).

Neste caso, regredimos o modelo com MQ2E, substituindo *S*<sub>*i*</sub>
pelos valores estimados $\\hat{S\_i}$ no modelo estrutural:

$$
log(H)\_i = \\beta\_0 + \\beta\_1 \\hat{S\_i} + \\beta\_2 E\_i + \\beta\_3 R\_i + \\mu\_i
$$

    modelo_mq2e <- lm(log(homicidio) ~ s_estimado + gastos_educacao + renda_setor_formal, base_final_pib)

    summary(modelo_mq2e)

    ## 
    ## Call:
    ## lm(formula = log(homicidio) ~ s_estimado + gastos_educacao + 
    ##     renda_setor_formal, data = base_final_pib)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -2.19425 -0.42487  0.03067  0.46225  2.10004 
    ## 
    ## Coefficients:
    ##                      Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)         2.9390423  0.2354558  12.482  < 2e-16 ***
    ## s_estimado         -0.0755321  0.0185704  -4.067 5.78e-05 ***
    ## gastos_educacao     0.0013828  0.0002170   6.372 5.41e-10 ***
    ## renda_setor_formal -0.0001647  0.0001527  -1.078    0.282    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6581 on 380 degrees of freedom
    ## Multiple R-squared:  0.1277, Adjusted R-squared:  0.1209 
    ## F-statistic: 18.55 on 3 and 380 DF,  p-value: 2.991e-11
