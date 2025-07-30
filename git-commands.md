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

## Commit Policy

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
