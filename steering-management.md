# Steeringファイル管理ガイドライン

## Steeringファイル変更ルール

### コンテンツレビュー要件
Steeringファイルを追加または変更する際は、以下を必ず行ってください：

1. **変更前にすべての既存Steeringファイルをレビューする**
2. **すべてのSteeringファイル間の一貫性をチェックする**
3. **ファイル間の重複を特定し解決する**
4. **異なるSteeringファイル間に矛盾がないことを確認する**
5. **明確性を保ち冗長性を避けるために必要に応じてコンテンツを再編成する**

### 変更プロセス
1. **完全なルールセットを理解するためにすべての現在のSteeringファイルを読む**
2. **潜在的な競合や重複について新しいコンテンツを分析する**
3. **新しいコンテンツに最も適切なファイルを特定する**
4. **新しいルールを追加する代わりに更新が必要な既存の類似ルールをチェックする**
5. **追加により冗長性が生じる場合は統合または再編成する**
6. **必要に応じてファイル間の相互参照を更新する**

### コンテンツ組織化原則
- **単一の真実の源**：各ルールは一箇所にのみ存在すべき
- **論理的グループ化**：関連するルールは同じファイルにあるべき
- **明確な階層**：より具体的なルールは一般的なルールを参照すべき
- **矛盾なし**：すべてのSteeringファイルは調和して機能する必要がある

### 品質保証
- **変更を確定する前**：一貫性を確保するためにすべてのSteeringファイルを再読する
- **相互参照を確認**：すべてのファイル参照が正確であることを確認する
- **ギャップをチェック**：再編成中に重要なルールが誤って削除されていないことを確認する
- **明確性を保つ**：ルールは明確で曖昧でないものにする

これにより、Steeringシステムがすべてのプロジェクトとコンテキストにわたって整理され、一貫性があり、効果的であることが保証されます。

# Steering File Management Guidelines

## Steering File Modification Rules

### Content Review Requirements
When adding or modifying any steering file, you MUST:

1. **Review ALL existing steering files** before making changes
2. **Check for consistency** across all steering files  
3. **Identify and resolve duplications** between files
4. **Ensure no contradictions** exist between different steering files
5. **Reorganize content** if necessary to maintain clarity and avoid redundancy

### Modification Process
1. **Read all current steering files** to understand the complete rule set
2. **Analyze the new content** for potential conflicts or overlaps
3. **Identify the most appropriate file** for the new content
4. **Check for existing similar rules** that might need updating instead of adding new ones
5. **Consolidate or reorganize** if the addition creates redundancy
6. **Update cross-references** between files if needed

### Content Organization Principles
- **Single source of truth**: Each rule should exist in only one place
- **Logical grouping**: Related rules should be in the same file
- **Clear hierarchy**: More specific rules should reference general ones
- **No contradictions**: All steering files must work together harmoniously

### Quality Assurance
- **Before finalizing changes**: Re-read all steering files to ensure coherence
- **Verify cross-references**: Ensure all file references are accurate
- **Check for gaps**: Ensure no important rules are accidentally removed during reorganization
- **Maintain clarity**: Rules should be clear and unambiguous

This ensures the steering system remains organized, consistent, and effective across all projects and contexts.
