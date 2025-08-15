# ESLint Usage Guidelines

## ESLint Configuration Location
ESLint configuration is stored at the user level to maintain consistency across all projects:
- **Configuration file**: `~/.eslint.config.mjs`
- **Type**: ES Module format with UserScript-specific settings

## Required ESLint Command Format
Always use the `--config` option to specify the user-level configuration file:

### Basic Commands:
- `eslint --config ~/.eslint.config.mjs [file]` - Lint specific file
- `eslint --config ~/.eslint.config.mjs .` - Lint entire project
- `eslint --config ~/.eslint.config.mjs . --fix` - Auto-fix issues

### Examples:
```bash
# Lint a specific UserScript file
eslint --config ~/.eslint.config.mjs twitter/tweet_intent_clipboard/main.js

# Lint all JavaScript files in project
eslint --config ~/.eslint.config.mjs .

# Auto-fix all fixable issues
eslint --config ~/.eslint.config.mjs . --fix
```

## UserScript-Specific Rules
The configuration includes UserScript/Tampermonkey specific settings:

### Globals Defined:
- **Tampermonkey APIs**: `unsafeWindow`, `GM_setValue`, `GM_getValue`, etc.
- **Browser APIs**: `console`, `document`, `window`, `location`, etc.

### Code Style Rules:
- **Indentation**: 4 spaces
- **Quotes**: Single quotes required
- **Semicolons**: Always required
- **No trailing commas**: Enforced

### Best Practices:
- **Unused variables**: Warning (not error)
- **Console usage**: Allowed (common in UserScripts)
- **Undefined variables**: Error
- **Prefer const**: Warning for better practices

## Project Integration
- **No project-specific ESLint files**: Use user-level configuration only
- **No package.json required**: ESLint runs with global configuration
- **Consistent across projects**: Same rules apply to all UserScript projects

## Enforcement Policy
- **ALWAYS use the full command**: Never run `eslint` without `--config ~/.eslint.config.mjs`
- **Fix issues before committing**: Run `--fix` option to auto-resolve style issues
- **Address all errors**: Warnings are acceptable, but errors must be resolved

This ensures consistent code quality across all UserScript projects while maintaining user-level configuration management.
