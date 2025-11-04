Guide the developer through a structured feature development workflow.

This command will:

1. **Gather Feature Description**: Prompt user for a detailed description of the feature they want to develop

2. **Analyze Requirements**:
   - Analyze the codebase to understand the current architecture, frameworks, and patterns. Understand best practices or recommendations for this repo in #CLAUDE.md if exists and in #README.md.
   - Identify relevant files, modules, and dependencies
   - Use available skills (e.g., code-reviewer, architect-review) to follow best practices

3. **Make Assumptions & Ask Clarifications**:
   - List all assumptions made (numbered)
   - Ask clarifying questions (numbered) using multi-choice format when possible
   - For complex questions, provide full description fields
   - Users can respond to questions individually (by number) or all at once

4. **Iterate on Requirements**:
   - Based on user responses, refine and finalize requirements
   - Present consolidated requirements document
   - Ask user for approval or further refinements

5. **Optional: Create Issue Ticket**:
   - Offer to create a ticket in the issue management system (Linear, GitHub Issues, etc.)
   - Use the appropriate MCP (Linear, GitHub) to create the ticket
   - Include all requirements, assumptions, and acceptance criteria

6. **Task Breakdown**:
   - Once requirements are approved, offer to break down into smaller tasks
   - Each task includes:
     - Task number
     - Detailed description
     - Dependencies (if any)
     - High-level approach or pseudo-code
     - Estimated complexity
   - NO implementation code - only descriptions and pseudo-code

7. **Export Options**:
   - Tasks can be exported as sub-issues/tasks in the issue management system
   - Can be saved as a markdown document in the repo

## Workflow Principles

- Make sensible default assumptions wherever possible
- Use codebase analysis to inform decisions
- Leverage architecture patterns already in use
- Consider testing requirements, documentation needs, and migration paths
- Focus on breaking down work, not implementing it
- Call out assumptions clearly and get confirmation before proceeding

## Example Usage

```
User: /ck feature
Claude: Please describe the feature you want to develop:

User: Add user authentication with OAuth
Claude: I've analyzed your codebase. Here are my assumptions:
1. [Assumption] Using existing Express.js backend
2. [Assumption] JWT tokens for session management
...

Here are my questions:
1. Which OAuth providers? [Multi-choice: a) Google, b) GitHub, c) Both, d) Other]
2. Token expiration time? [Default: 24 hours]
...
```
