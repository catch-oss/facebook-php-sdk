# Migration Plan: facebook-php-sdk

## Summary

- **Package**: janu-software/facebook-php-sdk
- **Type**: A (Pure PHP library)
- **Tier**: 5
- **Risk Level**: Low
- **Estimated Scope**: 45 source files, ~45 classes/interfaces, ~30 test files

## Change Inventory

### Namespace Renames Required

None — this is a pure PHP library with no SilverStripe dependencies.

### Composer Dependency Changes

| Package | Current Version | Target Version | Notes |
|---|---|---|---|
| php | `>=8.3 <8.5` | `>=8.3` | Remove upper bound to allow PHP 8.5 |

All other dependencies are already at compatible versions:
- `phpunit/phpunit: ^12` — already current
- `psr/http-message: >=1` — fine
- `php-http/httplug: ^2.4` — fine
- `guzzlehttp/psr7: ^2.5` — fine
- `thecodingmachine/safe: ^2.5 \|\| ^3.0` — fine

### API Changes Required

None — no SilverStripe APIs are used.

### PHP 8.5 Compatibility Fixes

| Issue | Fix | Files Affected |
|---|---|---|
| PHP upper bound `<8.5` | Remove upper bound constraint | composer.json |
| Missing type hint on `$stream` property | Add `mixed` type (resource\|null) | src/FileUpload/File.php:39 |
| Missing parameter types on `set()` | Add `string $key, mixed $value` | src/PersistentData/SessionPersistentDataHandler.php:61 |

### PHPUnit Migration

No migration needed — the codebase is already fully PHPUnit 12 compatible:
- All `@dataProvider` annotations already converted to `#[DataProvider]` attributes
- All `@group` annotations already converted to `#[Group]` attributes
- All `setUp()`/`tearDown()` methods already have `: void` return types
- No `withConsecutive()`, `prophesize()`, `setMethods()`, or `ReflectionProperty::setAccessible()` usage

### Config Changes

None — no SilverStripe config files exist.

### Logging Integration

Not applicable — pure PHP library, no Catch logging standard needed.

## Risk Assessment

| Area | Risk | Notes |
|---|---|---|
| PHP version constraint | Low | Simple removal of upper bound `<8.5` |
| Type hint fixes | Low | 2 minor missing type hints, non-breaking |
| Test suite | Low | Already PHPUnit 12 with modern attributes, all tests pass |
| Dependencies | Low | All dependencies already at compatible versions |

## Migration Steps (Ordered)

### Phase 1: composer.json
- [ ] Change PHP constraint from `>=8.3 <8.5` to `>=8.3`
- [ ] Run `composer validate`

### Phase 2: PHP 8.5 Compatibility
- [ ] Add type hint to `$stream` property in `src/FileUpload/File.php`
- [ ] Add parameter type hints to `set()` in `src/PersistentData/SessionPersistentDataHandler.php`

### Phase 3: Verify Tests
- [ ] Run `vendor/bin/phpunit --exclude-group integration` to confirm all tests pass
- [ ] Verify coverage output generates correctly

## Dependencies

- Depends on: none (Type A library, no internal catch-oss dependencies)
- Blocks: abc-silverstripe-social (Tier 6, transitive dependency)
