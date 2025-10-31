This command will optimize to install, enable or disable MCPs, plugins, sub-agents, skills in claude such that it is optimized to have minimum token overhead in context for maximum productivity to work in current repo.


It looks through current code base, analyzes which programming language, frameworks are used. Then looks
for which MCPs, plugins and sub-agents, skills should be installed or enabled. It should look at different sources to come up with recommendation
* marketplace available at wshobson/agents
* look at MCPs useful in registry at https://github.com/mcp

If git remote origin is github or github CI/CD files are found in repo, then suggest to install github MCP.
If git commit follows git commit message convention, then suggest to install hooks which forces commit to follow convention.

Look at current claude settings and summarize what should be installed or enabled or disabled. Prompt user whether you would like to proceed with these recommendations. If yes, then execute corresponding claude commands. Make sure the recommended changes are installed in repo subfolder ./.claude/settings.json
