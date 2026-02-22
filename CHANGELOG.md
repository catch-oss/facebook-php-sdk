# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Changed
- Updated PHP requirement to allow 8.5 (`>=8.3 <8.5` -> `>=8.3`)
- Added `mixed` type hint to `$stream` property in `File.php`
- Added parameter type hints to `SessionPersistentDataHandler::set()`

### Added
- MIGRATION-PLAN.md documenting all changes
- CI workflows (test, SonarCloud, Claude review)
- SonarCloud badges in README.md
