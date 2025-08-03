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