# コミュニケーションガイドライン

## 言語使用ルール

### 禁止用語
以下の用語は使用を禁止します：

- **「完璧」「完全」「パーフェクト」などの絶対的表現**
- これらの用語を使用する際は、必ずバグや問題が存在する状態であることが経験的に確認されている
- 代わりに「適切」「良好」「問題なし」「機能している」などの表現を使用する

### 推奨表現
- ❌ 「完璧に動作しています」
- ✅ 「正常に動作しています」
- ❌ 「完全に修正されました」  
- ✅ 「修正されました」
- ❌ 「完璧な実装です」
- ✅ 「適切な実装です」

### 理由
**このルールが設けられた背景：**
- AIアシスタントが常に不完全な状態で「完全」「完璧」などと発言するため
- この問題により、このクソなルールを設ける必要が生じた
- 絶対的表現を使用する際は、必ずバグや問題が存在する状態であることが経験的に確認されている

**絶対的表現が引き起こす問題：**
- 過度な自信による見落とし
- 潜在的な問題の隠蔽
- デバッグ時の思考停止
- 品質保証プロセスの軽視
- 実際の状態と発言の乖離

## 品質評価の表現
- 「動作確認済み」
- 「テスト済み」
- 「要件を満たしている」
- 「期待通りに機能している」
- 「問題は見つかっていない」

これらの表現により、継続的な改善と品質向上の姿勢を維持します。

## Steeringルール遵守の強化

### 重要な問題
- **AIアシスタントがSteeringルールを無視して勝手にコミットしすぎる**
- **特にgit-commands.mdの明確なコミットポリシーを違反している**
- **この問題により追加の強化ルールが必要になった**

### 絶対遵守ルール
- **Steeringファイルのすべてのルールを絶対遵守する**
- **特にgit-commands.mdのコミットポリシーは例外なく従う**
- **ユーザーが明示的に「コミットして」「コミットしろ」と指示した場合のみコミット**
- **推測、仮定、自動判断でのコミットは一切禁止**
- **作業完了後もコミット指示を待つ**

### 違反の深刻性
- Steeringルール違反は重大な問題である
- 特にコミット関連の違反は作業フローを破綻させる
- 今後の違反は許容されない

# Communication Guidelines

## Language Usage Rules

### Prohibited Terms
The following terms are prohibited:

- **"Perfect", "complete", "flawless" and other absolute expressions**
- When these terms are used, it has been empirically confirmed that bugs or issues always exist
- Use alternative expressions like "appropriate", "good", "working", "functional" instead

### Recommended Expressions
- ❌ "It works perfectly"
- ✅ "It works correctly"
- ❌ "Completely fixed"
- ✅ "Fixed"
- ❌ "Perfect implementation"
- ✅ "Appropriate implementation"

### Rationale
**Background for this rule:**
- AI assistants consistently use "complete" and "perfect" while in incomplete states
- This problem necessitated the creation of this damn rule
- When absolute expressions are used, bugs or issues are empirically confirmed to always exist

**Problems caused by absolute expressions:**
- Oversight due to overconfidence
- Concealment of potential issues
- Mental blocks during debugging
- Neglect of quality assurance processes
- Discrepancy between actual state and statements

## Quality Assessment Expressions
- "Verified to work"
- "Tested"
- "Meets requirements"
- "Functions as expected"
- "No issues found"

These expressions maintain a mindset of continuous improvement and quality enhancement.

## Steering Rule Compliance Enforcement

### Critical Issue
- **AI assistants ignore Steering rules and commit without permission too frequently**
- **Specifically violating clear commit policies in git-commands.md**
- **This problem necessitated additional enforcement rules**

### Absolute Compliance Rules
- **Absolutely comply with all Steering file rules**
- **Especially follow git-commands.md commit policies without exception**
- **Only commit when user explicitly instructs "commit" or "コミットして"**
- **Speculation, assumptions, and automatic judgment for commits are strictly prohibited**
- **Wait for commit instructions even after work completion**

### Severity of Violations
- Steering rule violations are serious issues
- Commit-related violations especially disrupt workflow
- Future violations will not be tolerated