# Busca otimizada de nomes similares com uso de índice reverso Realiza uma busca eficiente por nomes similares em uma grande base de dados, utilizando uma abordagem de duas etapas: primeiro seleciona candidatos via índice invertido no DuckDB e, em seguida, refina os resultados usando cálculos de distância de strings fonéticas.

Busca otimizada de nomes similares com uso de índice reverso Realiza uma
busca eficiente por nomes similares em uma grande base de dados,
utilizando uma abordagem de duas etapas: primeiro seleciona candidatos
via índice invertido no DuckDB e, em seguida, refina os resultados
usando cálculos de distância de strings fonéticas.

## Usage

``` r
buscar_similares_indice(
  nome,
  n_candidatos = 2000,
  limite_similaridade = 0.85,
  indice = "dic_palavras_metaphone.duckdb",
  central = "nomes_limpos_master.duckdb"
)
```

## Arguments

- nome:

  Character. O nome (ou parte de nome) para o qual se deseja encontrar
  similares.

- n_candidatos:

  Integer. O número máximo de candidatos a serem recuperados do índice
  invertido na primeira etapa. Padrão é 2000. Aumentar este valor pode
  melhorar a precisão (encontrando nomes mais raros), mas diminui a
  performance.

- limite_similaridade:

  Numeric (0.0 a 1.0). O limiar mínimo de similaridade para que um nome
  seja incluído no resultado final. Padrão é 0.85.

- indice:

  Character. Caminho para o arquivo do banco de dados DuckDB contendo o
  índice invertido de palavras fonéticas (ex:
  'dic_palavras_metaphone.duckdb').

- central:

  Character. Caminho para o arquivo do banco de dados DuckDB contendo a
  tabela central de nomes limpos (ex: 'nomes_limpos_master.duckdb').

## Value

Um `data.table` ordenado por similaridade decrescente, contendo as
colunas:

- `id`: O hash identificador único do nome encontrado.

- `nome_original`: O nome completo original encontrado na base central.

- `nome_metaphonebr`: A representação fonética pré-calculada do nome
  encontrado.

- `id_str`: O ID original convertido para string (para junção).

- `palavras_encontradas`: Inteiro indicando quantos tokens fonéticos do
  nome de entrada coincidiram com este candidato.

- `similaridade`: Score numérico (0-1) indicando o grau de similaridade
  final.

Retorna um `data.table` vazio se nenhum candidato for encontrado ou se o
nome de entrada for inválido.

## Details

Esta função é projetada para performar em bases com milhões de nomes,
evitando varreduras completas (full table scans) e cálculos de distância
de string em toda a base.

O processo ocorre nas seguintes etapas:

1.  **Configuração:** Conecta ao banco de índice e anexa o banco central
    em modo somente leitura.

2.  **Pré-processamento da Entrada:** O `nome` de entrada é convertido
    para sua forma fonética (usando `metaphonebr`) e dividido em tokens
    (palavras).

3.  **Seleção de Candidatos (Índice Invertido):** Uma consulta SQL busca
    no banco de `indice` quaisquer IDs de nomes que contenham pelo menos
    um dos tokens de entrada. Os resultados são agrupados por ID, e os
    `n_candidatos` com maior número de tokens coincidentes são
    selecionados.

4.  **Recuperação de Dados Brutos:** Uma segunda consulta SQL busca os
    dados completos (nome original, metaphone pré-calculado) no banco
    `central` apenas para os IDs candidatos selecionados.

5.  **Re-rankeamento Fino:** Para o conjunto reduzido de candidatos, a
    função calcula a similaridade exata entre a forma fonética da
    entrada e a forma fonética do candidato usando a função auxiliar
    [`calcular_similaridade_nomes`](https://ipea.github.io/nomesbr/reference/calcular_similaridade_nomes.md).

6.  **Filtragem:** Os resultados abaixo do `limite_similaridade` são
    descartados e o restante é ordenado.

**Pré-requisitos:** A função assume a existência de dois arquivos DuckDB
estruturados especificamente:

- `indice`: Deve conter a tabela `indice_palavras_metaphone` com
  mapeamento de palavras fonéticas para listas de IDs.

- `central`: Deve conter a tabela `nomes_limpos` com as colunas
  `nome_original_hash`, `nome_original` e `nome_metaphonebr`.

## See also

[`calcular_similaridade_nomes`](https://ipea.github.io/nomesbr/reference/calcular_similaridade_nomes.md)
para detalhes sobre o cálculo do score final.
