# Where the record of an agent's work lives

Kortix is open source, and this page answers the question a migration actually settles: six months from now, who can show what an agent did, in a form someone else can check. A team moving off Cowork does not lose its record in September. It keeps a record it does not operate, on terms another company writes, for as long as that company serves it. Kortix, the open-source AI Operating System, is the setup where that record is a repository instead.

## What Anthropic documents for its own product

The record exists and it is documented. "The Compliance API gives Claude Enterprise and Claude Console customers programmatic access to their organization's Activity Feed", and for Enterprise organizations it also covers the underlying chats, files and projects plus sessions in Cowork and other Claude surfaces ([Anthropic documentation](https://platform.claude.com/docs/en/manage-claude/compliance-api), checked 20 October 2026).

Three properties of that record decide what a team can do with it.

It serves Enterprise data only. The same page states that "the content endpoints (chats, files, projects, project attachments, and sessions) serve Claude Enterprise data only", and that a standalone Console organization can query the Activity Feed only ([Anthropic documentation](https://platform.claude.com/docs/en/manage-claude/compliance-api)). A team on Pro, Max or Team has no documented transcript endpoint.

It describes events more than content. "The Activity Feed records resource events but not prompt or response text", and no session transcript "includes thinking blocks or tool definitions" ([Compliance API FAQ](https://platform.claude.com/docs/en/manage-claude/compliance-faq)). An investigator can learn that a file was created or that a session ran. Reconstructing the reasoning means opening the transcript, if the plan has one.

It starts when someone turns it on. The Activity Feed "retains 6 years of organization activity", and recording "is not retroactive, and activity from before enablement is not backfilled" ([Compliance API FAQ](https://platform.claude.com/docs/en/manage-claude/compliance-faq)). The separate audit log export is narrower again: "a capped lookback window, CSV download only, and no access to chat, file, or project content" ([Anthropic documentation](https://platform.claude.com/docs/en/manage-claude/compliance-api)). A Cowork task a person deletes is removed from task history immediately, and from Anthropic's backend storage within 30 days ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)).

## What a repo-backed system gives you

The alternative is a record the team writes and keeps: a repository where the agent's configuration and the agent's output are both files, and the path between them is a branch, a diff and a change request.

Everything in that record is a git object. The agent's instructions and its grants are in the commit that added them, so the question "what was this agent allowed to do in August" has an answer that is a `git log` away. The output is a file at a commit. The review is a change request with a diff and a person's name on the merge. Nothing in that chain needed an API key, an Enterprise plan or a vendor's cooperation to read.

Kortix records the session side as well. Every action is recorded. Reading, exporting and streaming the audit log depend on the plan. The repo is what makes the record portable. A `git clone` on a laptop after the vendor relationship ends is a complete copy of the configuration history and every delivered artifact.

The limit is worth stating plainly. A repository holds what was committed. The conversation that produced a file, the false starts and the abandoned attempts, stays in the session unless someone saves it. A repo-backed system gives a team a strong record of what changed and a weaker one of how it was decided. Anthropic's API does better on the second and worse on everything a plan gates.

## The comparison

| Dimension | Kortix | Claude with Cowork today |
| --- | --- | --- |
| Open source | Yes, the whole platform | No, runs on Anthropic's servers |
| Where the record lives | Commits, diffs and change requests in your repo | Compliance API records and a CSV export |
| What it captures | The config change and the deliverable | Session transcripts and resource events |
| Who can read it | Members of the project with read access | Enterprise owners, through compliance keys |
| Retention | As long as the repository exists | 6 years of events; 30 days after a task delete |
| Where it runs | Self-hosted, or on Kortix Cloud | Anthropic's servers |

The Claude column comes from the pages linked above and from the Help Center's account of where the work runs: "Claude's work runs on Anthropic's servers, in an isolated environment, and your sessions and files are saved to your Claude account" ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)). The two limits this page has already named apply to the Kortix column: the event feed carries no prompt text, and an uncommitted conversation is not in the repo.

## What to check before you rely on either

Three questions, and the answers are on the vendor's page rather than in a migration plan. Which plan is the team on, because it decides whether transcript endpoints exist at all. When was recording turned on, because nothing before that date can be recovered. And who holds the copy, because a record you can only read through someone else's API is a record you rent.

Kortix's own plan entitlements for reading and exporting the audit log are on [kortix.com/pricing](https://kortix.com/pricing), and this page does not restate them.

## One property that outlasts both

A record is worth what it costs to keep it readable. A CSV export with a capped lookback is readable until the window closes. An API is readable while the key works. A repository is readable with `git`, which is a tool the team already has and will still have after this vendor, this product and this name are gone.

That is the argument for moving the record while the work still exists, and it does not depend on which system a team picks. It depends on the record being a file.
