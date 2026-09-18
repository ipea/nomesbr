# AGENTS.md

Guidance for AI agents working in the **nomesbr** repository.

## What this package is

`nomesbr` is an R package (CRAN-published, Ipea / ipeadata-lab) that cleans,
simplifies, and phonetically encodes Brazilian person names to support
record linkage when no unambiguous keys exist. Documentation, comments,
messages, and tests are mostly written in **Portuguese** — keep new content
in that language to match.

## Essential commands

```r
devtools::load_all()        # develop interactively
devtools::document()        # regenerate NAMESPACE + man/ (roxygen2 7.3.2)
devtools::test()            # run testthat suite (3rd edition)
rcmdcheck::rcmdcheck(".", args = c("--as-cran"))   # full CRAN-style check
pkgdown::build_site()       # docs site (pkgdown/_pkgdown.yml)
```

CI (`.github/workflows/`): `check.yaml` (R CMD check matrix incl. oldrel-2,
devel), `test-coverage.yaml` (covr → Codecov), `pkgdown.yaml`.

## Architecture / data flow

Two pipelines in `R/`:

1. **Cleaning pipeline** (main entry `limpar_nomes(d, s)` in
   `R/limpar_nomes.R`): takes a `data.table` and a column name string.
   Creates `<s>_clean` plus one boolean flag column per problem detected
   (`falecido`, `cartorio`, `nada_nao`, `letra_repetida`, ...). Steps are
   numbered 0–11 inside the function; every step is wrapped in
   `tictoc::tic()/toc()` (timing prints on every run — noisy output in
   tests is normal). Downstream:
   `tabular_problemas_em_nomes(d, s)` summarizes the flag columns;
   `simplifica_PARTICULAS_AGNOMES_PATENTES()` (default input column
   `nome_clean`, output `<s>_simp`) then `segmentar_nomes()` /
   `identificar_adicionar_nome_proprio()`.
2. **Similarity / central-database pipeline** (`R/utils_com_central.R`):
   `consulta_nome_em_central()` (exact lookup in a DuckDB master table
   `nomes_limpos`, keyed by `nome_original_hash` UINT128), and
   `calcular_similaridade_nomes()` → `sugerir_correcao_nomes()` →
   `buscar_similares_indice()` (inverted phonetic index in DuckDB, table
   `indice_palavras_metaphone`) → `processamento_lote()` (chunked batch).

Supporting files: `R/regexes.R` holds **all** regex/constant definitions at
package level (executed at build time; order matters, some blocks are
duplicated/redefined deliberately). `R/utils.R` has internal helpers;
`R/utils_download_nomes_compostos.R` downloads a ~109MB dictionary
(`nomes_proprios_compostos.rds`) from a GitHub release into
`tools::R_user_dir("nomesbr", "cache")` on first use.

## Conventions

- Data manipulation is **data.table** idiom: `d[, (s2) := ...]` with
  column names passed as strings and `get(s)` / `(s2) :=` dynamic
  assignment; `data.table::copy()` before modifying to avoid mutating the
  caller's object (both main functions do this).
- Regexes live in `R/regexes.R` in UPPERCASE snake names (`regex_X`,
  `NA_X`); new cleaning rules should follow that pattern, not inline regex.
- Column-name convention: input `s` → `<s>_clean` → `<s>_simp` →
  `<s>_w1/_w2/_w3/_w2p/_w12p` → `<s>1_v2/_2p_v2`.
- Lambdas use base R `\(x)` shorthand, not `function(x)`.
- Several functions are exported under legacy aliases via
  `#' @rdname` + duplicate assignment (e.g. `find_and_clean_NAnames_and_extra_spaces
  <- limpar_nomes`). Keep aliases when refactoring.
- `R/nomesbr-package.R` lists all data.table-created flag columns in
  `utils::globalVariables()` — add new columns created via `d[, x := ...]`
  there to pass `R CMD check`.
- Optional heavy deps (`duckdb`, `DBI`, `metaphonebr`) are **Suggests** and
  must be accessed only via `requireNamespace()` guards + explicit
  `pkg::fun()` calls. Never add `@import`/`@importFrom` roxygen tags for
  them — that would turn them into hard Imports and break install.
- Roxygen tags must never include `@import nomesbr` (self-import → cyclic
  namespace error once NAMESPACE is regenerated).

## Testing

- testthat 3e (`Config/testthat/edition: 3`), files in `tests/testthat/`.
- `setup-cria-amostra-np2.R` is auto-run by testthat before every test file
  (name starts with `setup-`); it re-saves `testdata/amostra_np2_para_testes.RDS`.
- Mock external downloads with `mockery::stub(fun, 'obter_dic_nomes_proprios_compostos', ...)`.
  A stub whose target function is never called fails **silently** and the
  real download runs — verify the stubbed symbol is actually called.
- Tests needing absent optional deps must guard:
  `skip_if_not_installed("duckdb")`, `skip_if_not_installed("metaphonebr")`.
  Tests that hit network/disk-cache use `skip_on_cran()`.

## CRAN gotchas (this package was archived once for this)

- **Never write outside the session temp dir during check.** The package
  was removed from CRAN (May 2026) because `obter_dic_nomes_proprios_compostos()`
  wrote `~/.cache/R/nomesbr/...` during `R CMD check` (detritus NOTE).
  Triggers that must stay fixed: examples that download must be
  `\dontrun` (NOT `\donttest` — CRAN's `--run-donttest` machine executes
  those), and tests must mock or `skip_on_cran()` anything touching the cache.
- After adding/renaming exported functions always run `devtools::document()`
  **and delete orphaned `man/*.Rd`** — a stale NAMESPACE export (e.g. the
  `buscar_similares_otimizado` → `buscar_similares_indice` rename) breaks
  `library(nomesbr)` with "object not found" and check warns.
- Version bumps required for every CRAN resubmission; update `NEWS.md` and
  `cran-comments.md` together (`cran-comments.md` is .Rbuildignored).
- `R CMD check` runs on R ≥ 4.3 across 3 OSes incl. oldrel-2 — avoid
  bleeding-edge base R features.

## Local environment notes

- Local machine may lack `duckdb`/`metaphonebr` → relevant tests skip or
  print fallback messages; that is expected, not a bug.
- The dictionary cache (109MB) lives at `~/.cache/R/nomesbr/`; once cached,
  tests run in ~30–45s, first-ever run downloads it.
