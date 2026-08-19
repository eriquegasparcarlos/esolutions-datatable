# Changelog

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
