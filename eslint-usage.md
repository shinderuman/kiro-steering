# ESLint使用ガイドライン

## ESLint設定場所
ESLint設定は全プロジェクトで一貫性を保つためにユーザーレベルで保存されます：
- **設定ファイル**: `~/.eslint.config.mjs`
- **タイプ**: UserScript固有設定を含むESモジュール形式

## 必須ESLintコマンド形式
ユーザーレベル設定ファイルを指定するために、常に`--config`オプションを使用してください：

### 基本コマンド：
- `eslint --config ~/.eslint.config.mjs [file]` - 特定ファイルをリント
- `eslint --config ~/.eslint.config.mjs .` - プロジェクト全体をリント
- `eslint --config ~/.eslint.config.mjs . --fix` - 問題を自動修正

### 例：
```bash
# 特定のUserScriptファイルをリント
eslint --config ~/.eslint.config.mjs twitter/tweet_intent_clipboard/main.js

# プロジェクト内のすべてのJavaScriptファイルをリント
eslint --config ~/.eslint.config.mjs .

# 修正可能なすべての問題を自動修正
eslint --config ~/.eslint.config.mjs . --fix
```

## UserScript固有ルール
設定にはUserScript/Tampermonkey固有の設定が含まれています：

### 定義されたグローバル：
- **Tampermonkey API**: `unsafeWindow`、`GM_setValue`、`GM_getValue`など
- **ブラウザAPI**: `console`、`document`、`window`、`location`など

### コードスタイルルール：
- **インデント**: 4スペース
- **クォート**: シングルクォート必須
- **セミコロン**: 常に必須
- **末尾カンマなし**: 強制

### ベストプラクティス：
- **未使用変数**: 警告（エラーではない）
- **コンソール使用**: 許可（UserScriptでは一般的）
- **未定義変数**: エラー
- **const優先**: より良いプラクティスのための警告

## プロジェクト統合
- **プロジェクト固有のESLintファイルなし**: ユーザーレベル設定のみ使用
- **package.json不要**: ESLintはグローバル設定で実行
- **プロジェクト間で一貫**: すべてのUserScriptプロジェクトに同じルールを適用

## 実施ポリシー
- **常に完全なコマンドを使用**: `--config ~/.eslint.config.mjs`なしで`eslint`を実行しない
- **コミット前に問題を修正**: `--fix`オプションを実行してスタイル問題を自動解決
- **すべてのエラーに対処**: 警告は許容されるが、エラーは解決する必要がある

これにより、ユーザーレベル設定管理を維持しながら、すべてのUserScriptプロジェクトで一貫したコード品質が保証されます。

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
