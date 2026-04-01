## Pre-commit checklist (MANDATORY)

Before EVERY commit, you MUST run all three checks on the files you changed and fix any errors. No exceptions.

1. **PHPCS** (auto-fix first, then verify):
   ```bash
   vendor/bin/phpcbf --standard=WordPress <changed-files>
   vendor/bin/phpcs --standard=WordPress <changed-files>
   ```
2. **Psalm** (on changed source files, not tests):
   ```bash
   vendor/bin/psalm --no-cache <changed-source-files>
   ```
3. **PHPUnit** (run relevant test files):
   ```bash
   vendor/bin/phpunit <relevant-test-files>
   ```

If any check fails, fix the errors and re-run before committing. Do NOT commit with known lint, Psalm, or test failures.

### Notes
- CI lints ALL changed lines, not just new files. The pre-commit hook only lints new files, so it will miss issues in modified files.
- CI uses the full `WordPress` standard (includes `-Docs` rules like missing docblocks and alignment). Always use `--standard=WordPress`, not `WordPress-Core`.
- `vendor/bin/phpcs` is the correct binary path. `npm run lint-php` requires a script name argument and does not work for targeted file linting.

## Conventions
- **Changelogs**: Every user-facing change MUST have a changelog entry before opening a PR. Run `npm run changelog` (entries stored in `changelog/`).
