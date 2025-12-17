Execute the git-workflow skill to perform a complete git commit workflow.

This command will:
1. Check if any code is staged.
  a. If no code is staged, but only see unstaged changes, then don't prompt user. Directly stage all changes and move to step 2.
  b. If code is staged, but no unstaged changes, then move to step 2.
  c. If any code is staged and you see some unstaged changes, then prompt user whether they would like to add unstaged changes to stage before moving to step 2.
2. Review all staged changes
3. Generate a conventional commit message based on the changes. Do not add message "co-authored by claude" at the end.
4. Commit the changes locally
5. Push to remote if origin is configured

The git-workflow skill will guide you through each step.
