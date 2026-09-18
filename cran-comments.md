## Resubmission

This is a resubmission to restore the package after archival for leaving
detritus in the user's home directory (see
https://www.stats.ox.ac.uk/pub/bdr/donttest/nomesbr.out).

Changes:

* The example of `identificar_adicionar_nome_proprio()` that downloads a
  109MB dictionary (cached via `tools::R_user_dir()`) was moved from
  `\donttest` to `\dontrun`, so it is never executed during `R CMD check`,
  not even with `--run-donttest`.
* A unit test of `identificar_adicionar_nome_proprio()` intended to mock the
  dictionary download stubbed a nonexistent function, so the real download
  ran during check. The mock now correctly stubs
  `obter_dic_nomes_proprios_compostos()` and reads local test data only.
* Regenerated NAMESPACE: the stale export `buscar_similares_otimizado`
  (function renamed to `buscar_similares_indice`) broke package loading.
* Declared `stringi` in Suggests (used via `stringi::`).

## R CMD check results

0 errors | 0 warnings | 1 note

* This is a new release.
