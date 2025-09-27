# コーディング規約

## 一般的なガイドライン
- 清潔で読みやすく、保守しやすいコードを書く
- 意味のある変数名と関数名を使用する（'hoge'、'foo'、'bar'などの名前は避ける）
- 複雑なロジックには適切なコメントを追加する
- 言語固有の規約とベストプラクティスに従う

## Go固有のガイドライン
- Go命名規約に従う（プライベートはcamelCase、パブリックはPascalCase）
- コンテキストを含む説明的なエラーメッセージを使用する
- サイレント失敗よりも明示的なエラーハンドリングを優先する
- プロジェクト全体で一貫したログ形式を使用する
- 関連する機能を適切に命名された関数にグループ化する

### Goビルド確認ルール
- **ビルド確認時は必ず`go build -o /dev/null .`を使用する**
- 実行ファイルを生成せずにコンパイルエラーのみをチェックする
- 作業ディレクトリを汚さないためのベストプラクティス

## PHP固有のガイドライン
- 文字列リテラルにはデフォルトでシングルクォートを使用する
- ダブルクォート内での変数展開は絶対に使用しない
- `.`演算子または`sprintf()`関数で文字列連結を使用する
- 改行には`\n`の代わりに`PHP_EOL`を使用する
- 改行付きのecho文では、カンマ区切りを使用する：`echo $foo, PHP_EOL`（`echo $foo . PHP_EOL`ではない）

### PHP文字列の例
```php
// 良い例
$message = 'Hello world';
$fullMessage = $greeting . ' ' . $name;
$formatted = sprintf('User %s has %d points', $name, $points);
echo $message, PHP_EOL;

// 悪い例
$message = "Hello world";
$fullMessage = "$greeting $name";
$formatted = "User $name has $points points";
echo $message . PHP_EOL;
```

## 関数組織化ガイドライン
**重要なルール：関数は呼び出し順序で整理する必要があります**

- **必須：新しい関数を追加する際は、それを呼び出す関数の直後に配置する**
- **ファイルの末尾やランダムな場所に新しい関数を配置してはいけない**
- **正確な実行フローに従う：関数Aが関数Bを呼び出す場合、関数Bは関数Aの直後に定義する必要がある**
- メイン関数から始めて、それが直接呼び出す関数を続ける
- 各関数について、そのヘルパー関数を直後に配置する
- これにより実行順序に合致する自然なトップダウンの読み取りフローが作成される
- プライベートヘルパー関数は呼び出し元関数の直下に配置する

### 関数順序の例
```go
func main() { ... }

func process() { ... }        // mainから呼び出される

func initConfig() { ... }     // processから呼び出される
func fetchData() { ... }      // processから呼び出される
func processData() { ... }    // processから呼び出される

func validateItem() { ... }   // processDataから呼び出される
func formatOutput() { ... }   // processDataから呼び出される
```

### 実施ルール
- 新しい関数を配置する前に、常に呼び出し順序を確認する
- 関数を間違った場所に配置した場合、正しい位置に移動する必要がある
- 正しい位置は常に呼び出し元関数の直後で、自然な実行フローに従う
- これはコードの可読性と保守性のために必須である

## コードレビュー基準
- すべての関数が明確で説明的な名前を持つことを確認する
- エラーハンドリングが包括的で情報提供的であることを確認する
- 一貫したフォーマットとスタイルをチェックする
- コミット前にプレースホルダー名や一時的なコードを削除する
- 関数が正しい呼び出し順序で配置されていることを確認する

# Coding Standards

## General Guidelines
- Write clean, readable, and maintainable code
- Use meaningful variable and function names (avoid names like 'hoge', 'foo', 'bar')
- Add appropriate comments for complex logic
- Follow language-specific conventions and best practices

## Go-specific Guidelines
- Follow Go naming conventions (camelCase for private, PascalCase for public)
- Use descriptive error messages with context
- Prefer explicit error handling over silent failures
- Use consistent logging format across the project
- Group related functionality into well-named functions

### Go Build Verification Rules
- **Always use `go build -o /dev/null .` when checking if build passes**
- Check for compilation errors without generating executable files
- Best practice to avoid cluttering the working directory

## PHP-specific Guidelines
- Use single quotes for string literals by default
- NEVER use variable interpolation inside double quotes
- Use string concatenation with `.` operator or `sprintf()` function
- Use `PHP_EOL` for line breaks instead of `\n`
- For echo statements with line breaks, use comma separator: `echo $foo, PHP_EOL` (not `echo $foo . PHP_EOL`)

### PHP String Examples
```php
// Good
$message = 'Hello world';
$fullMessage = $greeting . ' ' . $name;
$formatted = sprintf('User %s has %d points', $name, $points);
echo $message, PHP_EOL;

// Bad
$message = "Hello world";
$fullMessage = "$greeting $name";
$formatted = "User $name has $points points";
echo $message . PHP_EOL;
```

## Function Organization Guidelines
**CRITICAL RULE: Functions MUST be organized in call order**

- **MANDATORY: When adding ANY new function, place it immediately after the function that calls it**
- **DO NOT place new functions at the end of the file or in random locations**
- **Follow the exact execution flow: if function A calls function B, then function B must be defined immediately after function A**
- Start with main function first, followed by functions it calls directly
- For each function, place its helper functions immediately after it
- This creates a natural top-down reading flow that matches execution order
- Private helper functions should be placed directly under their calling function

### Example Function Order
```go
func main() { ... }

func process() { ... }        // Called by main

func initConfig() { ... }     // Called by process
func fetchData() { ... }      // Called by process
func processData() { ... }    // Called by process

func validateItem() { ... }   // Called by processData
func formatOutput() { ... }   // Called by processData
```

### Enforcement Rules
- Always check the call order before placing a new function
- If you place a function in the wrong location, it MUST be moved to the correct position
- The correct position is always immediately after the calling function, following the natural execution flow
- This is MANDATORY for code readability and maintainability

## Code Review Standards
- Ensure all functions have clear, descriptive names
- Verify error handling is comprehensive and informative
- Check for consistent formatting and style
- Remove any placeholder names or temporary code before committing
- Verify functions are placed in correct call order