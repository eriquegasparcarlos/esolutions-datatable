# Changelog

## [v2.4.2] - 2026-09-08
### Fixed
- `Filter::value()` dropped its `mixed` parameter type. `mixed` is PHP 8.0+; on
  7.4 it is parsed as a **class name**, so every `->value('all')` call died with
  *"Argument 1 passed to Filter::value() must be an instance of
  Esolutions\Datatable\Table\mixed"*. 19 DataTables in qpospe call it 33 times,
  always to preselect the "Todos" option, so the whole listing was unusable on
  7.4. Behaviour on PHP 8 is unchanged: the type hint only removed a check.

### Note
- v2.4.0 claimed the two `badge()` named-argument calls were "the *only* PHP 8
  syntax in the whole package". They were not — this `mixed` survived, and the
  release note's own remedy would not have caught it: **`php -l` cannot detect
  it**, because `mixed` is a syntactically valid class name on 7.4. It only
  fails at call time. A lint pass is not enough; the package needs the 7.4 job
  in CI actually running the code, which is still pending (the token used to
  push lacks `workflow` scope, so `.github/` never made it to the remote).


## [v2.4.1] - 2026-09-03
### Fixed
- `Button::newButton()` now defaults its label to `'Nuevo'`. It was the only
  preconfigured button left with a null label, so XTableServer rendered it as a
  bare round icon — its header button template only shows text when
  `button.label` is set. Every sibling (`editButton`, `duplicateButton`,
  `exportButton`, `deleteButton`, `viewButton`) already had one; `refreshButton`
  stays icon-only on purpose. Passing an explicit label still overrides it.

## [v2.4.0] - 2026-09-03
### Changed
- **The package now also runs on PHP 7.4 / Laravel 5.7.** Constraints widened to
  `php: ^7.4|^8.0` and `laravel/framework: ^5.7|^11.0|^12.0|^13.0` so qpospe (5.7)
  and qpospev2 (13) can share the same listing code — a DataTable moves between
  them by changing the `use`, nothing else.
- `Cell::badgeIsActive()` and `Cell::badgeBoolean()` call `badge()` positionally
  instead of with named arguments (PHP 8.0+). Those two calls were the *only*
  PHP 8 syntax in the whole package; everything else already parsed on 7.4.
  Behaviour is unchanged — verified the four returned arrays are identical.

### Removed
- `esolutions/laravel` from `require`. It was never imported anywhere in `src/`
  and its own `php: ^8.2` was what actually blocked installing on 7.4.

### Note
- A `php -l` check over `src/` on PHP 7.4 is now **required** before releasing.
  Composer cannot catch this: with `^7.4|^8.0` declared, a named argument or an
  enum installs without complaint and only blows up at runtime on 7.4. The
  Actions workflow for it is pending (the token used to push lacked the
  `workflow` scope).

## [v2.3.0] - 2026-08-19
### Added
- `Filter::makePeriod()->includeAllOption()`: adds a "Todos" option that disables
  the date filter. The period block of `XTableServer` does not support the
  `include-all-option` prop, so the option is prepended server-side in the
  options array. `getFilterDate()` returns explicit nulls for `'all'` — the
  consumer must skip its `whereBetween` when both dates are null.

## [v2.2.0] - 2026-08-19
### Changed
- **Icons are now roles, not FontAwesome class names.** `Button::icon()` no longer
  prefixes `fal fa-`: it stores the role (`add`, `edit`, `delete`) and the frontend
  decides how to draw it. The four conventions that coexisted (Button prefixed,
  BulkAction expected a full string, DialogAction sent a bare name, ButtonBuilder
  had a hardcoded literal) are now the same one.
- Renamed to roles: `plus`→`add`, `pencil`→`edit`, `arrows-rotate`→`refresh`,
  `eye`→`view`, `shield-check`/`shield-xmark`→`activate`/`deactivate`,
  `triangle-exclamation`→`warning`, `circle-info`→`info`.
- `Button::deleteButton()` used `xmark` (close) — now uses `delete`.

### Requires
- `@esolutions/x-components >= 2.17.0`. With an older version the frontend does not
  resolve roles and buttons render without an icon.

## [v1.2.2] - 2026-06-11
### Fixed
- Removed hardcoded `"version"` field from `composer.json` (caused Packagist to skip tags)
- Published to Packagist — `repositories` block no longer needed in consumer projects

## [v1.2.1] - 2025-xx-xx
### Changed
- Internal improvements

## [v1.2.0] - 2025-xx-xx
### Added
- `Column`: added `visible()`, `sortField()`, `onlyExport()`, `summable()`, `excelWidth()`, `excelFormat()`, `excelWrap()`
- `Filter`: added `clearable()`, `filterable()`, `searchUrl()`, `makeSearch()`, `$class` param in `makePeriod()`

## [v1.1.0] - 2025-xx-xx
### Added
- `PaginationTenantTrait` and `PaginationSystemTrait`
- `GenericReportExport` for Excel exports with styled headers
- `DialogAction` for delete/active confirmation dialogs
- `ActionRequest` FormRequest for dialog endpoints

## [v1.0.0] - 2025-xx-xx
### Added
- Initial release: `Column`, `ColumnBuilder`, `Filter`, `FilterBuilder`, `Button`, `ButtonBuilder`
- `PaginationBaseTrait`, `ExcelTrait`, `FilterTrait`
