This command will initialize claude-kit in current repo. This command will make sure developer has chosen all necessary tools and ensure right sub-agents, MCP servers are installed/enabled.

The settings are stored in the root of the repo at .claude-kit/settings.json

Below is the psuedo code of the algorithm to setup the current repo correctly.

Make sure below keys are available in settings.json. If not use the questions in the "prompts" section of this file to ask the user and update those values correctly in settings.json . Ensure you ask these questions one by one, so the user can answer individual question separately.

The keys are:
* tools.issue
* tools.documentation
* tools.git
* mcp.issue
* mcp.documentation
* mcp.git

## prompts

if ("tools.issue" not in settings.json) {
  tools.issue = prompt("Enter the tool used to track issues to be created. Possible options to choose are linear, github, jira")
}

if ("tools.documentation" not in settings.json) {
  tools.issue = prompt("Enter the tool used to document the specifications created. Possible options to choose are issue-tracker, confluence")
}

if ("tools.git" not in settings.json) {
  tools.issue = prompt("Enter where git repository is hosted. Possible options to choose are github, gitlab , custom")
}

if ("mcp.git" == "github") {
  Ensure that a remote github MCP is setup either directly or through plugins. Make sure the github mcp server URL is `https://api.githubcopilot.com/mcp/`.


  if (github mcp installation missing) {
    print the message that Github MCP server installation instructions are available at https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/#%f0%9f%94%97-how-to-use-it
    The user should be prompted where to add automatically.
    If you get yes, prompt to specify Github Personal access token , capture as variable GITHUB_ACCESS_TOKEN then execute the command `claude mcp add --header "Authorization: ${GITHUB_ACCESS_TOKEN}" --transport http github https://api.githubcopilot.com/mcp/` and let user know to restart claude command.
    Once installation is checked, Check if user has authenticated with github mcp. If not, initiate github MCP authentication
  }
}