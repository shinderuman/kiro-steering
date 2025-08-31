# Gitコマンドガイドライン

Gitコマンドを実行する際は、出力がページャー（lessなど）を通してパイプされることを防ぐため、常に`--no-pager`オプションを使用してください。

## 必須Gitコマンド形式：
- `git --no-pager status`
- `git --no-pager log`
- `git --no-pager diff`
- `git --no-pager commit`
- `git --no-pager show`

これにより、ページ化された結果をナビゲートするためのユーザー操作を必要とせず、出力が直接表示されることが保証されます。

## コミットポリシー：
- **変更を自動的にコミットしない**
- ユーザーから明示的に指示された場合のみ`git commit`を実行する
- 変更をコミットする前に、常にユーザーの明示的なコミット指示を待つ
- ユーザーはgitコミット操作に対して明確なコミット指示を与える必要がある

いかなる状況下でも、**明示的に指示されない限り**`git commit`操作を実行**しない**でください。
これは、自動的または推定されるコミットを一切行わないことを意味します。

## コミットメッセージガイドライン：
- **コミットメッセージを作成する前に、常に`git --no-pager diff`を使用して実際のソースコード差分を分析する**
- 会話のコンテキストではなく、差分に表示される実際のコード変更に基づいてコミットメッセージを作成する
- コード変更が実際に何を行うかを読み理解し、それらの変更を正確に説明する
- 行われた変更についての会話履歴や推測に依存しない
- 差分出力を直接調べることで変更の範囲と影響を確認する

## ステージされた変更レビュープロセス：
- **コミットメッセージを作成する前に、常に`git add .`または`git add <files>`を使用して変更をステージする**
- **コミット前に、常に`git --no-pager diff --cached`を使用してステージされた変更をレビューする**
- これにより、ステージされていない作業ディレクトリの変更ではなく、実際にコミットされる正確な変更を分析することが保証される
- `--cached`フラグはステージされた変更のみを表示し、これが実際にコミットに含まれる内容である
- ステージされていない変更を表示する`git --no-pager diff`だけに依存しない

## コミットメッセージ形式ルール：
このプロジェクトでは従来のコミットプレフィックスを使用します。すべてのコミットメッセージは以下のプレフィックスのいずれかで始まる必要があります：

### コアプレフィックス：
- `feat:` - 新機能の追加
- `fix:` - バグ修正とエラー訂正
- `refactor:` - 機能を変更せずにコードを再構築
- `improve:` - パフォーマンス改善と機能強化

### 追加プレフィックス（将来の使用のため）：
- `docs:` - ドキュメント変更
- `style:` - コードスタイル変更（フォーマット、セミコロン不足など）
- `test:` - テストの追加または更新
- `chore:` - メンテナンスタスク、依存関係更新、ビルド変更
- `perf:` - パフォーマンス改善（improve:のサブセット）
- `ci:` - CI/CDパイプライン変更
- `build:` - ビルドシステムまたは外部依存関係の変更
- `revert:` - 以前のコミットの取り消し

### 形式構造：
```
<prefix>: <description>

- <detailed change 1>
- <detailed change 2>
- <detailed change 3>
```

### 例：
```
feat: Add comprehensive logging for Kindle book processing in sale-checker
fix: Return error when Kindle search yields no results
refactor: Standardize error handling across checkers
improve: Enhance title cleaning logic and add comprehensive tests
docs: Update README with deployment instructions
test: Add unit tests for title cleaning function
chore: Update dependencies to latest versions
```

**常に上記のプレフィックスのいずれかを使用してください。プレフィックスなしの一般的な説明は使用しないでください。**

## Git出力表示ルール
- **gitコマンドをhead、tail、またはその他の出力制限ツールにパイプしない**
- git diff、git show、git logコマンドの完全な出力を常に表示する
- これにより変更とコミット情報の完全な可視性が保証される
- やってはいけないことの例：
  - ❌ `git --no-pager diff | head -20`
  - ❌ `git --no-pager show | tail -10`
  - ❌ `git --no-pager log | head -5`
- 正しい使用法：
  - ✅ `git --no-pager diff`
  - ✅ `git --no-pager show`
  - ✅ `git --no-pager log`

完全な出力の可視性は、適切なコードレビューと変更検証に不可欠です。

## 新セッションコミットメッセージガイドライン
新しいKiroセッションを開始して最初のコミットを行う際：

### 履歴コンテキストレビュープロセス：
- **常に`git --no-pager log -5`（--onelineではない）を使用して最近のコミット履歴をレビューする**
- **プロジェクトで使用されている完全なコミットメッセージ形式とスタイルを研究する**
- **以前のコミットメッセージの詳細レベルと構造を分析する**
- **以下について確立されたパターンに合わせる：**
  - メッセージの長さと詳細レベル
  - 箇条書きの構造とフォーマット
  - 技術用語と言語スタイル
  - 変更と理由の説明の深さ

### コミットメッセージ一貫性ルール：
- **参照のために省略されたgitログ形式（--oneline、--pretty=oneline）を使用しない**
- **プロジェクト基準を理解するために常に完全なコミットメッセージを調べる**
- **既存のコミットメッセージスタイルと詳細レベルとの一貫性を保つ**
- **プロジェクト履歴で見つかるのと同じ深さの技術的詳細を含める**
- **同じ箇条書き構造とフォーマット規約に従う**

### 品質基準：
- 最近のコミットの冗長性と説明スタイルに合わせる
- 履歴メッセージと同じ深さの技術的詳細を含める
- 何が変更されたかだけでなく、なぜ変更され、コードベースにどのような影響を与えるかを説明する
- プロジェクト履歴からの一貫した用語とフレーズパターンを使用する

これにより、いつ作成されたかに関係なく、すべてのコミットメッセージがプロジェクトライフサイクル全体を通じて一貫した品質とスタイル基準を維持することが保証されます。

# Git Command Guidelines

When executing git commands, always use the `--no-pager` option to prevent output from being piped through a pager (like less).

## Required Git Command Format:
- `git --no-pager status`
- `git --no-pager log`
- `git --no-pager diff`
- `git --no-pager commit`
- `git --no-pager show`

This ensures output is displayed directly without requiring user interaction to navigate through paged results.

## Commit Policy:
- **NEVER commit changes automatically**
- Only execute `git commit` when explicitly instructed by the user
- Always wait for user's explicit commit instruction before committing any changes
- User must give clear commit instruction for any git commit operation

Do **not** perform any `git commit` operation **unless explicitly instructed** to do so.  
This means no automatic or assumed commits should be made under any circumstances.

## Commit Message Guidelines:
- **ALWAYS analyze actual source code differences using `git --no-pager diff` before creating commit messages**
- Base commit messages on the actual code changes shown in the diff, not on conversation context
- Read and understand what the code changes actually do, then describe those changes accurately
- Do not rely on conversation history or assumptions about what changes were made
- Verify the scope and impact of changes by examining the diff output directly

## Staged Changes Review Process:
- **ALWAYS use `git add .` or `git add <files>` to stage changes before creating commit messages**
- **ALWAYS use `git --no-pager diff --cached` to review staged changes before committing**
- This ensures you are analyzing the exact changes that will be committed, not unstaged working directory changes
- The `--cached` flag shows only the staged changes, which is what will actually be included in the commit
- Never rely on `git --no-pager diff` alone as it shows unstaged changes, not what will be committed

## Commit Message Format Rules:
This project uses conventional commit prefixes. All commit messages must start with one of the following prefixes:

### Core Prefixes:
- `feat:` - New feature additions
- `fix:` - Bug fixes and error corrections
- `refactor:` - Code restructuring without changing functionality
- `improve:` - Performance improvements and enhancements

### Additional Prefixes (for future use):
- `docs:` - Documentation changes
- `style:` - Code style changes (formatting, missing semicolons, etc.)
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks, dependency updates, build changes
- `perf:` - Performance improvements (subset of improve:)
- `ci:` - CI/CD pipeline changes
- `build:` - Build system or external dependency changes
- `revert:` - Reverting previous commits

### Format Structure:
```
<prefix>: <description>

- <detailed change 1>
- <detailed change 2>
- <detailed change 3>
```

### Examples:
```
feat: Add comprehensive logging for Kindle book processing in sale-checker
fix: Return error when Kindle search yields no results
refactor: Standardize error handling across checkers
improve: Enhance title cleaning logic and add comprehensive tests
docs: Update README with deployment instructions
test: Add unit tests for title cleaning function
chore: Update dependencies to latest versions
```

**Always use one of the prefixes above. Do not use generic descriptions without prefixes.**
## Git Output Display Rules
- **NEVER pipe git commands to head, tail, or other output limiters**
- Always show full output for git diff, git show, git log commands
- This ensures complete visibility of changes and commit information
- Examples of what NOT to do:
  - ❌ `git --no-pager diff | head -20`
  - ❌ `git --no-pager show | tail -10`
  - ❌ `git --no-pager log | head -5`
- Correct usage:
  - ✅ `git --no-pager diff`
  - ✅ `git --no-pager show`
  - ✅ `git --no-pager log`

Full output visibility is essential for proper code review and change verification.

## New Session Commit Message Guidelines
When starting a new Kiro session and making the first commit:

### Historical Context Review Process:
- **ALWAYS review recent commit history using `git --no-pager log -5` (NOT --oneline)**
- **Study the full commit message format and style used in the project**
- **Analyze the level of detail and structure in previous commit messages**
- **Match the established patterns for:**
  - Message length and detail level
  - Bullet point structure and formatting
  - Technical terminology and language style
  - Explanation depth for changes and reasoning

### Commit Message Consistency Rules:
- **NEVER use abbreviated git log formats (--oneline, --pretty=oneline) for reference**
- **Always examine complete commit messages to understand project standards**
- **Maintain consistency with existing commit message style and detail level**
- **Include similar level of technical detail as found in project history**
- **Follow the same bullet point structure and formatting conventions**

### Quality Standards:
- Match the verbosity and explanation style of recent commits
- Include technical details at the same depth as historical messages
- Explain not just what changed, but why and how it impacts the codebase
- Use consistent terminology and phrasing patterns from project history

This ensures all commit messages maintain consistent quality and style standards
throughout the project lifecycle, regardless of when they are created.
