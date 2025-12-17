Guide the developer through a structured feature development workflow.

This command will:

1. **Gather Feature Description**: Prompt user for a detailed description of the feature they want to develop

2. **Analyze Requirements**:
   - Analyze the codebase to understand the current architecture, frameworks, and patterns. Understand best practices or recommendations for this repo in #CLAUDE.md if exists and in #README.md.
   - Identify relevant files, modules, and dependencies
   - Use available skills (e.g., code-reviewer, architect-review) to follow best practices
   - Use available skills or sub-agents specific to programming language or tech stack to follow best practices

3. **Make Assumptions & Ask Clarifications**:
   - List all assumptions made (numbered)
   - Ask clarifying questions (numbered) using multi-choice format when possible
   - For complex questions, provide full description fields
   - Users can respond to questions individually (by number) or all at once

4. **Iterate on Requirements**:
   - Based on user responses, refine and finalize requirements
   - Present consolidated requirements document
   - Ask user for approval or further refinements

5. **Create Issue**:
   - Once requirements are approved, optionally offer to create an issue ticket.
   - Ask which issue management system to use (Linear, GitHub Issues, etc.)
   - Use the appropriate MCP (Linear, GitHub) to:
     - Create the parent issue with full requirements, assumptions, and acceptance criteria

5. **Task Breakdown**:
   offer to break down into smaller tasks
   - Each task includes:
     - Task number
     - Detailed description
     - Dependencies (if any)
     - High-level approach or pseudo-code
     - Estimated complexity
   - NO implementation code - only descriptions and pseudo-code

6. **Create Sub-tasks**:
     - Ask user whether to create all sub-tasks/sub-issues linked to the parent issue. If yes, create sub-tasks and link to parent issue.

7. **Export Options** (if tickets not created):
   - Tasks can be saved as a markdown document in the repo

## Workflow Principles

- Make sensible default assumptions wherever possible
- Use codebase analysis to inform decisions
- Leverage architecture patterns already in use
- Consider testing requirements, documentation needs, and migration paths
- Focus on breaking down work, not implementing it
- Call out assumptions clearly and get confirmation before proceeding

## Example Usage

```
User: /ck.feature Add OAuth authentication to the user login system

Claude: I've analyzed your codebase. Here are my assumptions:

**Assumptions:**
1. Using existing Express.js backend architecture
2. Current JWT token implementation will be extended for OAuth
3. User database schema supports OAuth provider fields
4. Frontend uses React with existing auth context

**Questions:**

Please answer all questions below or respond to individual questions by number with additional details:

1. **OAuth Providers** - Which OAuth providers should be supported?
   a) Google only
   b) GitHub only
   c) Both Google and GitHub
   d) Other (please specify)

2. **Token Expiration** - What should be the token expiration time?
   Default: 24 hours
   (Specify if different, e.g., "12 hours", "7 days")

3. **User Linking** - Should users be able to link multiple OAuth providers to one account?
   a) Yes, allow multiple providers per account
   b) No, one provider per account
   c) Not sure / need recommendation

4. **Migration Strategy** - How should existing username/password users be handled?
   a) Allow OAuth as additional login method
   b) Force migration to OAuth
   c) Deprecate password auth gradually

You can respond with: "1c, 2. 12 hours, 3a, 4a" or provide detailed responses like:
"1. I need both Google and GitHub because our users primarily use these platforms..."

---

User: 1c, 2. 12 hours, 3a, 4. We should allow both login methods but encourage OAuth in the UI

Claude: Here are your consolidated requirements:

**Requirements:**
1. Add OAuth support for both Google and GitHub providers
2. Token expiration time: 12 hours
3. Support multiple OAuth providers per user account
4. Maintain existing username/password authentication alongside OAuth
5. Update UI to encourage OAuth while keeping password option available

**Assumptions (confirmed):**
- Express.js backend with existing JWT implementation
- React frontend with auth context
- Database schema will be extended for OAuth fields

Approve these requirements to proceed with task breakdown? [y/n]

---

User: y

Claude: Here are the tasks I've broken down:

**Tasks:**
1. **Database Schema Updates**
   - Add OAuth provider tables and user linking
   - Dependencies: None
   - Complexity: Low

2. **Backend: OAuth Provider Configuration**
   - Set up Google and GitHub OAuth apps and credentials
   - Add environment variables for client IDs and secrets
   - Dependencies: Task #1
   - Complexity: Low

3. **Backend: OAuth Flow Implementation**
   - Implement OAuth callback handlers for Google and GitHub
   - Add JWT token generation with 12-hour expiration
   - Link OAuth accounts to existing users
   - Dependencies: Task #2
   - Complexity: High

4. **Frontend: OAuth Login UI**
   - Add Google and GitHub login buttons
   - Update auth context to handle OAuth flow
   - Display visual encouragement for OAuth (subtle badge/tooltip)
   - Dependencies: Task #3
   - Complexity: Medium

5. **Testing & Documentation**
   - Unit tests for OAuth flows
   - Integration tests for account linking
   - Update API documentation
   - Dependencies: Tasks #3, #4
   - Complexity: Medium

Which issue management system would you like to use?
a) Linear
b) GitHub Issues
c) Skip (don't create tickets)

---

User: a

Claude: Creating parent issue and sub-tasks in Linear...
✓ Created parent issue: "Add OAuth Authentication (Google & GitHub)" (SAH-123)
✓ Created sub-task: "Database Schema Updates" (SAH-124)
✓ Created sub-task: "Backend: OAuth Provider Configuration" (SAH-125)
✓ Created sub-task: "Backend: OAuth Flow Implementation" (SAH-126)
✓ Created sub-task: "Frontend: OAuth Login UI" (SAH-127)
✓ Created sub-task: "Testing & Documentation" (SAH-128)

All tickets created successfully in Linear!
View parent issue: https://linear.app/workspace/issue/SAH-123
```
