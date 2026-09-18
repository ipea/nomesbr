# Adiciona Nome Próprio Validado de \`nomes_proprios_compostos\` .

Adiciona Nome Próprio Validado de \`nomes_proprios_compostos\` .

## Usage

``` r
identificar_adicionar_nome_proprio(dt, s)

add_nome_proprio_to_word1_and_word2p(dt, s)
```

## Arguments

- dt:

  Um \`data.table\`.

- s:

  Nome da coluna (string) base para derivação das colunas de palavras
  (por exemplo, se \`s = "nome_simpl"\`, espera \`nome_simpl1\`,
  \`nome_simpl2p\`).

## Value

O \`data.table\` \`dt\` com colunas \`\_v2\` adicionadas.

## Examples

``` r
if (FALSE) { # \dontrun{
dt_nomes <- data.table::data.table(nome=c("MARIA DO SOCORRO SILVA",
"ANA PAULA DE OLIVEIRA","JOSE DAS FLORES"))
dt_nomes <- identificar_adicionar_nome_proprio(dt_nomes,"nome")
print(dt_nomes)
} # }
```
