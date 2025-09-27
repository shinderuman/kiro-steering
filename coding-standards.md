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

### 呼び出し順序の正確な理解
**重要：関数の配置は呼び出し元関数内での呼び出し順序に厳密に従う必要がある**

#### 正しい配置例
```go
func main() {
    a := getA()     // 1番目の呼び出し
    b := processB() // 2番目の呼び出し  
    outputC(b)      // 3番目の呼び出し
}

// 正しい関数配置順序
func main() { ... }
func getA() { ... }     // ✅ 1番目の呼び出し順
func processB() { ... } // ✅ 2番目の呼び出し順
func outputC() { ... }  // ✅ 3番目の呼び出し順
```

#### よくある間違い
- 推測による配置：呼び出し順序を確認せずに配置する
- 機能的重要度による配置：重要度で順序を決める
- 修正時の注意不足：関数移動時に呼び出し順序を再確認しない

## 変数使用ガイドライン

### 再利用しない変数の回避
**RULE: 一度しか使用されない変数は一行がよっぽど長くならない限り使用しない**

#### 再利用の定義
変数が**2回以上使用される**場合は再利用とみなす：
- 代入時（1回目）
- 参照時（2回目以降）

#### 悪い例（一度しか使用されない）
```go
// ❌ 悪い：一度しか使用されない変数
func generateURL(name string) string {
    encodedName := url.QueryEscape(name)  // 1回目：代入
    return config.BaseURL + encodedName   // 2回目：使用（これは再利用ではない）
}

func isError(err error) bool {
    errMsg := err.Error()                 // 1回目：代入
    return strings.Contains(errMsg, "error") // 2回目：使用（これは再利用ではない）
}
```

#### 良い例（直接使用）
```go
// ✅ 良い：直接使用
func generateURL(name string) string {
    return config.BaseURL + url.QueryEscape(name)
}

func isError(err error) bool {
    return strings.Contains(err.Error(), "error")
}
```

#### 良い例（再利用している）
```go
// ✅ 良い：変数が複数回使用される
func main() {
    characters := processCategory(category, jsonFile)  // 1回目：代入
    outputJSON(characters)                             // 2回目：使用（再利用）
}

func processData(input string) error {
    result := complexProcessing(input)    // 1回目：代入
    if result == nil {                    // 2回目：使用
        return errors.New("failed")
    }
    return saveResult(result)             // 3回目：使用（明確な再利用）
}
```

#### 例外：行が長すぎる場合
```go
// ✅ 許可：行が長すぎる場合は変数を使用
func processComplexData(data *ComplexStruct) error {
    processedResult := data.ProcessWithMultipleParameters(param1, param2, param3, param4, param5)
    return validateAndStoreResult(processedResult, additionalParam1, additionalParam2)
}
```

#### 例外：複数の戻り値がある場合
```go
// ✅ 許可：複数の戻り値を受け取る場合
func cleanText(text string) string {
    before, _, _ := strings.Cut(text, "(")
    return strings.TrimSpace(before)
}
```

### 判定基準
1. **使用回数を数える**: 代入 + 参照の合計回数
2. **2回以上なら変数使用**: 再利用とみなす
3. **1回のみなら直接使用**: 変数を避ける
4. **行の長さ**: 80-100文字を超える場合は例外
5. **複数戻り値**: 必要な値のみ変数に格納

### 間違いやすいパターン
```go
// ❌ これは再利用ではない（1回の代入 + 1回の使用 = 計2回だが実質1回の処理）
result := function()
return result

// ✅ これは再利用（1回の代入 + 2回の使用 = 計3回）
result := function()
if result != nil {
    return process(result)
}
```

この規則により、真に再利用される変数のみを使用し、不要な複雑さを排除する。
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

### Understanding Call Order Precisely
**Critical: Function placement must strictly follow the call order within the calling function**

#### Correct Placement Example
```go
func main() {
    a := getA()     // 1st call
    b := processB() // 2nd call  
    outputC(b)      // 3rd call
}

// Correct function placement order
func main() { ... }
func getA() { ... }     // ✅ 1st call order
func processB() { ... } // ✅ 2nd call order
func outputC() { ... }  // ✅ 3rd call order
```

#### Common Mistakes
- Placement by assumption: Placing without verifying call order
- Placement by functional importance: Ordering by importance rather than call sequence
- Insufficient attention during modifications: Not re-verifying call order when moving functions

## Variable Usage Guidelines

### Avoiding Non-Reused Variables
**RULE: Do not use variables that are only used once unless the line would become excessively long**

#### Definition of Reuse
A variable is considered reused when it is **used 2 or more times**:
- Assignment (1st time)
- Reference (2nd time and beyond)

#### Bad Examples (Used Only Once)
```go
// ❌ Bad: Variable used only once
func generateURL(name string) string {
    encodedName := url.QueryEscape(name)  // 1st: assignment
    return config.BaseURL + encodedName   // 2nd: use (this is not reuse)
}

func isError(err error) bool {
    errMsg := err.Error()                 // 1st: assignment
    return strings.Contains(errMsg, "error") // 2nd: use (this is not reuse)
}
```

#### Good Examples (Direct Use)
```go
// ✅ Good: Direct use
func generateURL(name string) string {
    return config.BaseURL + url.QueryEscape(name)
}

func isError(err error) bool {
    return strings.Contains(err.Error(), "error")
}
```

#### Good Examples (Actually Reused)
```go
// ✅ Good: Variable used multiple times
func main() {
    characters := processCategory(category, jsonFile)  // 1st: assignment
    outputJSON(characters)                             // 2nd: use (reuse)
}

func processData(input string) error {
    result := complexProcessing(input)    // 1st: assignment
    if result == nil {                    // 2nd: use
        return errors.New("failed")
    }
    return saveResult(result)             // 3rd: use (clear reuse)
}
```

#### Exception: Line Too Long
```go
// ✅ Allowed: Use variable when line is too long
func processComplexData(data *ComplexStruct) error {
    processedResult := data.ProcessWithMultipleParameters(param1, param2, param3, param4, param5)
    return validateAndStoreResult(processedResult, additionalParam1, additionalParam2)
}
```

#### Exception: Multiple Return Values
```go
// ✅ Allowed: When receiving multiple return values
func cleanText(text string) string {
    before, _, _ := strings.Cut(text, "(")
    return strings.TrimSpace(before)
}
```

#### Judgment Criteria
1. **Count usage**: Total of assignment + references
2. **2+ times means use variable**: Consider it reuse
3. **Only 1 time means direct use**: Avoid variables
4. **Line length**: Exception when exceeding 80-100 characters
5. **Multiple returns**: Store only needed values in variables

#### Common Mistake Patterns
```go
// ❌ This is not reuse (1 assignment + 1 use = 2 times total but essentially 1 operation)
result := function()
return result

// ✅ This is reuse (1 assignment + 2 uses = 3 times total)
result := function()
if result != nil {
    return process(result)
}
```

This rule ensures only truly reused variables are used, eliminating unnecessary complexity.

## Code Review Standards
- Ensure all functions have clear, descriptive names
- Verify error handling is comprehensive and informative
- Check for consistent formatting and style
- Remove any placeholder names or temporary code before committing
- Verify functions are placed in correct call order
