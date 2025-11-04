# CK Plugin - Claude Kit Core

The core plugin for claude-kit providing essential workflow for day to day developer work. This includes features similar to github spec-kit, but built natively for Claude to leverage claude specific features like slash commands, skills, plugins.  The plugin in lightweight and leverage other relevant plugins already installed in user's claude setup. 

## Features

- Initialize claude with right plugins, skills, MCPs based on current repo content
- Ability to quickly commit changes to current branch and push to remote
- Iterate on feature development using spec-driven approach. 

### Commands

- `/ckr.init` - Initialize Claude Kit in a project
- `/ck.commit` - Execute automated git commit workflow with conventional commits
- `/ck.suggest` - Optimize MCP/plugin/skill configuration for the current repository
- `/ck.feature` - Guide through structured feature development workflow with requirements gathering, task breakdown, and optional issue creation

### Skills

- **git-workflow** - Automated git workflow operations including commits and pull requests
