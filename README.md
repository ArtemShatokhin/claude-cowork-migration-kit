# Claude Cowork migration kit

Kortix is open source. This kit is the record for a team that ran Claude Cowork: what changed on 16 September 2026, what actually moved, and a checklist that ends with the work in a repository the team owns.

The claim this repo proves is narrow. Nothing was migrated for Cowork customers in September. The surface got a new name. The work stayed in the same account. A team that wants an auditable record of what its agents did has to move that record itself.

## Who this is for

Teams on Pro, Max, Team or Enterprise that used Cowork for real work now have three questions. They want to know what survives the rename, what disappears if they leave, and where the record of an agent's work lives afterwards. You do not need to be leaving Claude to use the checklist. You need to want the record somewhere you control.

## What is in this repo

- `docs/timeline.md` holds every dated change from the January 2026 preview to today, each with the page it came from.
- `docs/what-moved.md` walks chats, memory, plugins, the work record and the account, quoting Anthropic on each.
- `docs/migration-checklist.md` runs six steps in order, each with the command or the page where the work happens and a "done when" line.
- `docs/audit-trail.md` compares where the record of an agent's work lives in each setup, with every cell sourced.

## Five dates that decide the move

- **12 January 2026.** Cowork arrived as a research preview for Max subscribers in the macOS desktop app ([VentureBeat](https://venturebeat.com/technology/anthropic-is-killing-off-cowork-and-folding-it-into-claude-launching-claude-docs-and-claude-slides)).
- **9 September 2026.** The last day Anthropic offered an export of legacy memory ([Claude Help Center](https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context)).
- **16 September 2026.** "Anthropic is killing off its Claude Cowork brand and product as a separate experience, instead folding all its capabilities back into the default Claude chatbot interface" ([VentureBeat, 16 September 2026](https://venturebeat.com/technology/anthropic-is-killing-off-cowork-and-folding-it-into-claude-launching-claude-docs-and-claude-slides)).
- **From 16 September 2026.** Pro and Max accounts move first on web, desktop and mobile, and Team and Free follow; on Enterprise the unified experience is a beta an admin turns on ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)).
- **20 October 2026.** The Help Center still calls the rollout gradual ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)), and Anthropic still says the Cowork name "will eventually disappear" ([VentureBeat](https://venturebeat.com/technology/anthropic-is-killing-off-cowork-and-folding-it-into-claude-launching-claude-docs-and-claude-slides)).

## Where the agents get declared

In a repo-backed setup the agents are files, and one manifest at the root says which ones exist. This is the block from the starter project:

```yaml
agents:
  kortix:
    file: agents/kortix.md
    connectors: all
    secrets: all
    kortix_permissions: all
    skills: all
```

Those seven lines are unedited from `packages/starter/templates/base/kortix.yaml` in [Kortix on GitHub](https://github.com/kortix-ai/suna), read on 20 October 2026. The manifest pins the schema with `kortix_version: 2` and names `default_agent: kortix`, so a session that names no agent still lands on a declared one. Behavior lives in the markdown file. The grants live here. That split is the whole reason a diff can answer "what was this agent allowed to do last month".

## What Kortix is

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. More at [kortix.com](https://kortix.com).

## Starting this week, not next quarter

[Using Cowork today](docs/using-cowork-today.md) runs the six-step checklist against a first week: inventory and export on days one and two, the install and the repository on days three and four, then one real job landed through a change request on day five. It ends with the file tree and the commit message that make up the record you are left holding.

## Reading on the same question

- [Migrating from Claude Cowork](https://opensourceclaudecowork.com/migrate-from-claude-cowork) takes one recurring Cowork job and rebuilds it as files, in an order that loses nothing.
- [What happened to Claude Cowork](https://opensourceclaudecowork.com/what-happened-to-claude-cowork) covers the merge itself, the rollout waves and what a team keeps afterwards.
- [Self-hosting the replacement](https://opensourceclaudecowork.com/self-hosting) takes a bare Linux server to a running stack and plans the review gate around it.
- [How to use Claude Cowork](https://opensourceclaudecowork.com/how-to-use-claude-cowork) walks the setup steps after the merge, and where the open-source line falls.
- [Self-hosted Claude Code](https://opensourceclaudecowork.com/self-hosted-claude-code) asks the same control-plane question about the coding harness.

## What this kit leaves out

Anthropic's export article describes chats and account data, and says nothing about exporting Cowork tasks or projects, so nothing here claims such an export exists (checked 20 October 2026). Where a fact depends on a plan, the linked page is the source and this file is not.
