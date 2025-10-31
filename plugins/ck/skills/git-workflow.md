---
name: git-workflow

description: This skill manages the complete git commit workflow including staging, creating conventional commit messages, and pushing changes.
---

## Required Git Commands

This skill requires permission to run the following git commands. Request approval once at the beginning of the workflow:

**Read-only commands (inspection):**
- `git status` / `git status --porcelain` - Check repository status
- `git diff` - View unstaged changes
- `git diff --cached` / `git diff --staged` - View staged changes
- `git diff --staged --stat` - Show summary of staged changes
- `git log -1` - Verify last commit
- `git remote get-url origin` - Check remote configuration
- `git branch --show-current` - Get current branch name

**Write commands (modifications):**
- `git add <files>` / `git add .` - Stage changes
- `git commit -m "<message>"` - Create commit
- `git push origin <branch>` - Push to remote
- `git push -u origin <branch>` - Push new branch to remote

**Permission Request:**
At the start of the workflow, present this list and ask:
"This workflow will use the git commands listed above. Do you approve running these commands for this repository?"

Only ask for permission once per repository. Do not prompt again for subsequent commits in the same session.

## Workflow Steps

Follow these steps in order to complete the git workflow:

### 0. Request Permission (First Time Only)

Before starting the workflow, if this is the first time running for this repository:
- Display the list of required git commands from the "Required Git Commands" section
- Ask: "This workflow will use the git commands listed above. Do you approve running these commands for this repository?"
- Wait for user approval
- If approved: proceed with the workflow and remember approval for this repository
- If declined: exit the workflow

### 1. Check Repository Status

Check the current git status to identify unstaged and staged files:
- Run `git status --porcelain` to get a machine-readable status
- Identify files that are modified but not staged (prefixed with ` M` or `M `)
- Identify new files that are untracked (prefixed with `??`)
- Identify files already staged (prefixed with `A `, `M `, etc.)

### 2. Handle Unstaged Changes

If there are modified or new files that are not staged:
- Present a clear list of unstaged files to the user
- Ask: "The following files have changes that are not staged. Would you like to stage these changes?"
- List each file with its status (modified/new)
- Wait for user confirmation (yes/no)
- If yes: stage all unstaged changes using `git add .` or specific files
- If no: proceed only with already staged changes

### 3. Review Staged Changes

Once files are staged (or if files were already staged):
- Run `git diff --cached` to see the actual changes that will be committed
- Analyze all the staged changes carefully
- Identify the type of changes (new features, bug fixes, refactoring, documentation, etc.)
- Note which files were modified and the nature of modifications

### 4. Generate Conventional Commit Message

Create a commit message following the Conventional Commits format:

**Format:**
```
<type>(<scope>): <subject>

<body>
```

**Type Options:**
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Changes that don't affect code meaning (formatting, missing semicolons, etc.)
- `refactor`: Code change that neither fixes a bug nor adds a feature
- `perf`: Performance improvement
- `test`: Adding missing tests or correcting existing tests
- `build`: Changes to build system or dependencies
- `ci`: Changes to CI configuration files and scripts
- `chore`: Other changes that don't modify src or test files

**Guidelines:**
- **Subject line**: Should be 50 characters or less, lowercase, no period at the end
- **Scope** (optional): The area of codebase affected (e.g., api, ui, auth, parser)
- **Body**: Provide detailed description of ALL changes, line by line if necessary
  - Explain what changed
  - Explain why the change was made (if not obvious)
  - List all modified files and their changes
  - Use bullet points for clarity
  - Wrap at 72 characters

**Example:**
```
feat(git): add automated commit workflow skill

- Created git-workflow.md skill to handle complete commit process
- Implemented staging check and user confirmation flow
- Added conventional commit message generation
- Included automatic push to remote if origin is configured
- Added detailed workflow steps and guidelines for consistent commits

This skill automates the git commit workflow making it easier to
create well-formatted commit messages following conventional commits
standard. It ensures all changes are reviewed and properly staged
before committing.
```

### 5. Commit the Changes

- Use the generated commit message to create the commit
- Run `git commit -m "$(cat <<'EOF'
[commit message here]
EOF
)"`
- Verify the commit was successful by checking `git log -1`

### 6. Push to Remote (if configured)

Check if the repository has a remote origin configured:
- Run `git remote get-url origin` to check for remote
- If a remote exists:
  - Get the current branch name using `git branch --show-current`
  - Push the changes using `git push origin <branch-name>`
  - If the branch doesn't exist on remote, use `git push -u origin <branch-name>`
- If no remote exists:
  - Inform the user that changes are committed locally
  - Let them know they can push manually later if needed

### 7. Provide Summary

After completing the workflow:
- Confirm the commit was successful
- Show the commit SHA
- If pushed to remote, confirm the push was successful
- Display a summary of what was committed

## Error Handling

- If no changes are staged and user declines to stage, inform them and exit
- If git commands fail, display the error and explain what went wrong
- If push fails (e.g., conflicts, authentication issues), inform user and suggest manual resolution

## Usage Notes

- Always review the changes before committing
- Ensure commit messages are meaningful and follow conventions
- Group related changes in a single commit when appropriate
- Ask for clarification if the type of change is ambiguous
