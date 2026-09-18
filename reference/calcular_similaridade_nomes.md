# Calcular similaridade entre nomes

Esta função calcula a similaridade entre dois nomes utilizando uma
combinação ponderada de algoritmos de distância de strings (Jaro-Winkler
e Damerau-Levenshtein) após pré-processamento fonético.

## Usage

``` r
calcular_similaridade_nomes(nome1, nome2)
```

## Arguments

- nome1:

  Primeiro nome para comparação (character)

- nome2:

  Segundo nome para comparação (character)

## Value

Um valor numérico entre 0 e 1 representando a similaridade entre os
nomes

## Details

A função realiza os seguintes passos:

- Limpeza dos nomes usando nomesbr::limpar_nomes

- Codificação fonética usando metaphonebr::metaphonebr

- Cálculo da similaridade usando Jaro-Winkler (peso 0.7) e
  Damerau-Levenshtein (peso 0.3)

## Examples

``` r
calcular_similaridade_nomes("Maria", "Mary")
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.006 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.005 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.002 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.004 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.006 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.002 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0.001 sec elapsed
#> All substeps: 0.04 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.004 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> [1] 0.8933333
calcular_similaridade_nomes("José", "Jose")
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.002 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.003 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.002 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.003 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.024 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.003 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.076 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.002 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0.001 sec elapsed
#> All substeps: 0.096 sec elapsed
#> [1] 1
```
