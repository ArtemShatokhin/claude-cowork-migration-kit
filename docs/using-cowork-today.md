# Using Cowork today, and the record it never leaves

None of what the product tour teaches leaves a record an auditor can read, because none of it is a file. Anthropic merged Cowork into Claude on 16 September 2026 ([VentureBeat](https://venturebeat.com/technology/anthropic-is-killing-off-cowork-and-folding-it-into-claude-launching-claude-docs-and-claude-slides)), and its own account of the merge says the capabilities carried over: "your chats, projects, artifacts, connectors, and skills" stayed where they were, inside the account ([the announcement](https://claude.com/resources/articles/cowork-is-now-claude)). The rename is why the record has to live outside the vendor.

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. What follows is the six-step checklist run against a first week, in the order that keeps a job from disappearing between two systems.

## Days one and two: write down what exists, then export

Start with the inventory, not the install. Work down the task and project lists and write four lines per job: the instructions that define it, the connectors it reaches, the cadence, and the person who reads the output. Keep that file outside the vendor account. On a Team or Enterprise plan the archive covers your own chats and not the contents of files you uploaded, so instructions typed into a task are copied by hand ([export article](https://support.claude.com/en/articles/9450526-export-your-claude-data)).

Take the export anyway. Settings → Privacy → Export data, and the download link expires 24 hours after delivery.

## Day three: stand up the system you will keep

```bash
curl -fsSL https://kortix.com/install | bash
kortix login
```

`kortix doctor` checks the login, starts a throwaway session, waits for its sandbox, sends a ping and exits 1 if a step fails. Done when it exits 0. On your own server, `kortix self-host init --domain kortix.example.com --admin-email you@example.com` then `kortix self-host start` brings up one Compose stack, and the done line is `kortix self-host doctor` with no failing check.

## Day four: turn the inventory into files

```bash
kortix init my-agent
cd my-agent
```

Write one agent file per job. Instructions go in the body, permission rules in the frontmatter, and grants in `kortix.yaml` under an `agents:` block that names the file each agent runs from. `kortix ship` validates the manifest, commits, asks for missing secrets and prompts for the declared connectors. Session work reaches `main` through a change request, and merge is default-deny for agents, so the grant list is the review policy.

## Day five: prove one job and keep the record

Pick the job with the clearest output. `kortix sessions new --prompt "Draft the weekly status report from the notes in memory/"` starts it on its own branch and machine. Open the review with `kortix cr open --head <session_id> --session <session_id> --title "Weekly status report"`, read it with `kortix cr diff 1`, and land it with `kortix cr merge 1`.

The week ends with:

```
my-agent/
  kortix.yaml
  agents/weekly-brief.md
  memory/monday-brief.md
  docs/record/2026-09-cowork-inventory.md
  reports/2026-10-19-weekly-status.md
```

and one commit message that carries the decision:

```
weekly-brief: move the Monday status job out of Cowork

Instructions, connector list and reader copied from the inventory. First
run lands through change request #12; reviewer named in the agent file.
```

That repository is the audit trail: instructions, grants, deliverable and reviewer, at commits someone else can read. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. For the setup steps inside Cowork itself, and the permission decision the tour skips, [how to use Claude Cowork](https://opensourceclaudecowork.com/how-to-use-claude-cowork) covers both.

## Sources
- https://claude.com/resources/articles/cowork-is-now-claude · https://support.claude.com/en/articles/9450526-export-your-claude-data
- https://opensourceclaudecowork.com/how-to-use-claude-cowork · https://kortix.com/docs/quickstart
