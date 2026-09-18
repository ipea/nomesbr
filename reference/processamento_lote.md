# Processamento em lote de nomes

Processa um vetor de nomes em lotes para encontrar nomes similares,
otimizado para grandes volumes de dados.

## Usage

``` r
processamento_lote(vetor_nomes, chunk_size = 10000)
```

## Arguments

- vetor_nomes:

  Vetor de nomes para processar (character vector)

- chunk_size:

  Tamanho de cada lote para processamento (default = 10000)

## Value

Um data.frame combinado com todos os resultados dos lotes

## Details

A função:

- Remove duplicatas exatas primeiro

- Processa os dados em blocos (chunks) para otimizar memória

- Pode ser facilmente paralelizada modificando o loop interno

## Examples

``` r
if (FALSE) { # \dontrun{
processamento_lote(c("Maria", "João", "Ana", "Pedro", "Francisco"))
nomes_grande_vetor <- sample(c("Maria", "João", "Ana", "Pedro", "Francisco"),100,replace = TRUE)
processamento_lote(nomes_grande_vetor, chunk_size = 50)
} # }
```
