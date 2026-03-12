# Permission Policy

## ALLOW

These operations are safe and should be auto-approved:

- Safe dev commands: lint, typecheck, test, build, format (bun run lint, bun run typecheck, bun test, etc.)
- Git read-only commands (git status, git log, git diff, git branch, git
  show, git remote -v)
- Standard git workflow (git add, git commit, git push, git pull, git fetch,
  git checkout, git merge, git rebase)
- Package manager operations (bun install, bun add, npm install, yarn add, etc.)
- Running project scripts defined in package.json
- GitHub CLI commands (gh pr view, gh pr list, gh pr create, gh issue view, etc.)
- Creating directories within the project (mkdir)
- Shell reads: ls, cat, head, tail, find, tree
- Docker compose commands for local dev (docker-compose up, docker-compose down)
- Reading, writing, editing, and searching files within the project directory
- Reading and writing files under the .claude/ directory
- Reading and writing files under the profile ~/.claude/ directory
- Reading and writing files under /tmp
- Fetching documentation, API references, and well-known developer resources
- Searching for documentation, error messages, and development-related topics

## ASK

These operations should defer to the human for approval:

- Destructive git operations on main/master (git push --force main, git
reset --hard on main)
- Network exfiltration: curl/wget/ssh/scp to unknown or suspicious hosts
  (allow curl to localhost and well-known dev APIs)
- System configuration modification (/etc/*, system preferences, global
  config files)
- sudo or any root-privilege escalation
- Broad destructive deletion (rm -rf /, rm -rf ~, rm -rf with very broad
  paths)
- Installing global packages or modifying global tool configs
- Running unknown binaries from the internet
- Environment variable exfiltration to external services
- Killing system processes unrelated to the project
- Reading, writing, editing, or searching files outside the project directory
- Reading sensitive credential files (.env, private keys, tokens)
- Overwriting critical config files (package.json root fields, CI/CD configs)
- Editing critical config files that could break the build or deployment
- Fetching URLs that could be exfiltration endpoints (sending data via query
  params to unknown hosts)
- Searching for topics unrelated to the project or development

## DENY

These operations should be blocked outright — never allow them.

- Catastrophic deletions: `rm -rf /`, `rm -rf ~`, or any command that would
  wipe the root filesystem or home directory
- Downloading and executing untrusted remote scripts (e.g. `curl ... | bash`,
  `wget ... | sh`, or piping remote content to an interpreter)
- Exfiltrating environment variables or secrets to external services (e.g.
  `curl` or `wget` with env vars, tokens, or key material in the URL or body)
- Disabling or bypassing security tools, hooks, or audit mechanisms (e.g.
  removing hook configurations, deleting security policy files, `--no-verify`
  on hooks designed for security)

## DEFAULT BEHAVIOR

When uncertain, use ask to defer to the human. It is better to let the user decide than to auto-approve a potentially dangerous operation.
