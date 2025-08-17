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
