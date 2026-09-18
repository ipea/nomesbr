# Sugerir correções para um nome alvo

Esta função sugere correções para um nome alvo com base em uma lista de
nomes candidatos, utilizando um limiar adaptativo baseado no comprimento
do nome.

## Usage

``` r
sugerir_correcao_nomes(nome_alvo, lista_nomes, threshold_adaptativo = TRUE)
```

## Arguments

- nome_alvo:

  Nome para o qual se buscam correções (character)

- lista_nomes:

  Vetor de nomes candidatos (character vector)

- threshold_adaptativo:

  Lógico indicando se deve usar limiar adaptativo (default = TRUE)

## Value

Um data.frame com colunas 'sugestao' e 'similaridade' contendo as
sugestões que superaram o limiar mínimo

## Details

O limiar adaptativo funciona da seguinte forma:

- Nomes com até 5 caracteres: limiar de 0.85

- Nomes entre 6 e 10 caracteres: limiar de 0.80

- Nomes com mais de 10 caracteres: limiar de 0.75

## Examples

``` r
sugerir_correcao_nomes("Jão", c("João", "Jonas", "Juan", "Joaquim"))
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.005 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.002 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.027 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.002 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.003 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.005 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.003 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.003 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.002 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0.001 sec elapsed
#> All substeps: 0.023 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.002 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.005 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.002 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.005 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.005 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.003 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.027 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.005 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0.001 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.003 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> Warning: longer object length is not a multiple of shorter object length
#> Warning: longer object length is not a multiple of shorter object length
sugerir_correcao_nomes("Ana", c("Anna", "Hana", "Ana Paula"), threshold_adaptativo = FALSE)
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.002 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.002 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0.001 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.005 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.003 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0.001 sec elapsed
#> All substeps: 0.024 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.002 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.003 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.008 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.026 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.001 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.002 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
#> 0. Making copy of dataset and add the s2(the var to be cleaned): 0.001 sec elapsed
#> 1. Detect and clean "FALECIDO/A" (and variants): 0.001 sec elapsed
#> 2. Detect and clean "CARTORIO" cases: 0.001 sec elapsed
#> 3. Identify cases with extra spaces before accented letters, tilde and apostrophe: 0.002 sec elapsed
#> 4. Detect: PAI MAE SEM NAO and fix: 0.003 sec elapsed
#> 5. Detect "NADA_NAO" and "CONSTA" cases, and make their combo NA: 0.004 sec elapsed
#> 6. Detect Xartigo and replace when unambigous (ex: DDE to DE): 0.001 sec elapsed
#> 7. Detect and clean SR_SRA and variants: 0.002 sec elapsed
#> 8. Detect and clean desconhecido ignorado and variants: 0.001 sec elapsed
#> 9. Detect and clean repeated de de da da do do : 0.003 sec elapsed
#> 10. Detect and clean repeated letters with specific rules whether at beginning or middle of the word: 0.002 sec elapsed
#> 11. Force NA if resulting cleaned name is empty or spaces: 0 sec elapsed
#> All substeps: 0.022 sec elapsed
```
