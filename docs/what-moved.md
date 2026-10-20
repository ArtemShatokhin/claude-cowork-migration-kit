# What moved and what did not

Kortix is open source, and this page is the honest accounting of the September 2026 change: five things a Cowork team owned in practice, what happened to each one, and who holds it now. Where Anthropic's product is described, the wording is Anthropic's, linked where it appears. Kortix is the open-source AI Operating System, and the destination this page argues for is a repository the team holds.

Anthropic's summary of the merge is a single sentence. People and enterprises already working in Cowork "retain their chats, projects, artifacts, connectors and skills" ([VentureBeat, 16 September 2026](https://venturebeat.com/technology/anthropic-is-killing-off-cowork-and-folding-it-into-claude-launching-claude-docs-and-claude-slides)). Retain is the operative verb. Everything on that list stays where it already was, inside the account Anthropic operates.

## The table

| Item | Moved, or did not move | Who holds it now |
| --- | --- | --- |
| Chats and projects | Did not move. Carried over intact, same account | Anthropic, in the Claude account |
| Memory | Did not move. Shared with chat in the cloud | Anthropic, in the Claude account |
| Plugins and connectors | Did not move. Saved to the account | Anthropic, in the Claude account |
| The work record | Did not move. Transcripts served on request | Anthropic, through the Compliance API |
| The account and plan | Did not move. Paid plans only | Anthropic |

## Chats and projects

Projects kept their own files, links, instructions and memory, and the Help Center describes them as "persistent workspaces with their own files, links, instructions, and memory" ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)). A person searching for a Monday brief from June still finds it. That is the good news, and it is also the reason a move is easy to postpone: the material looks safe because it is still on screen.

What changed is the doorway. On desktop, web and mobile the Chat and Cowork options shared one home, and now Claude picks the mode from the prompt as the rollout reaches each account. The project did not move. The way a person reaches it did.

## Memory

Memory is the item most likely to be miscounted, because Anthropic runs two behaviors under one word. "Memory is shared between Chat and Claude Cowork when Cowork runs in the cloud; Cowork sessions that run locally on your computer don't use memory" ([Claude Help Center](https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context)). A team that ran Cowork on desktop against local files never had that memory in the first place, so there is nothing to export and nothing to lose.

For the cloud case, memory survived the rename and it stays editable in one place. Settings → Memory offers Pause, which keeps existing memory and stops writing new entries, and Reset, which "Permanently deletes all memories including project memories" with no undo ([Claude Help Center](https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context)). Anyone planning a move should read the second option twice. Reset is the fastest way to destroy the one asset this migration most needs to carry.

## Plugins and connectors

"A plugin you add is saved to your account, so it works in chat and Claude Code as well as Cowork" ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)). The plugin did not follow a workstream. It followed the account, which is a better outcome for a person and a worse one for a team that wanted the plugin's definition in a review.

The plugin is the closest thing in Cowork to a file a team could version. It is stored as account state and configured through a settings surface, so the definition is not readable as a diff and it does not travel with the repository when the work does.

## The work record

This is where the merge cost the most and said the least. Anthropic documents a Compliance API that returns session transcripts, including "transcripts of Cowork sessions started on claude.ai web or mobile, which run in the cloud in Anthropic-managed environments" ([Anthropic documentation](https://platform.claude.com/docs/en/manage-claude/compliance-api)). It also states that the content endpoints "serve Claude Enterprise data only". A team on Pro or Max therefore has no documented transcript endpoint at all, and a team on Enterprise has one that returns what Anthropic retained.

Deletion runs on Anthropic's clock. "Your Cowork task will be removed from your task history immediately, and deleted from our backend storage systems within 30 days, in accordance with our data retention periods" ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)). Thirty days is a short window for a question about what an agent did last quarter.

The export a team can run is narrower than the record. Anthropic's export article says the Team and Enterprise export "includes your own chats. It doesn't include the contents of files you uploaded", and that "Exported data can't be imported into another personal Claude account, and we don't support migrating data between personal accounts" ([Claude Help Center](https://support.claude.com/en/articles/9450526-export-your-claude-data)). A CSV of conversations is not an audit trail, and it is not portable.

## The account

Cowork runs on paid plans only: Pro, Max, Team and Enterprise ([Claude Help Center](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork)). No step in the September change converted an account, transferred one, or offered a path between them. The account is the unit Anthropic sells and the unit that holds everything above.

## What a move actually carries

Read the carry-over list backwards and the migration plan falls out of it. Chats, projects, artifacts, connectors and skills stay with Anthropic. What a team can still take is the setup: the instructions that define a job, the memory that shapes it, the connections it reaches through, and the cadence it runs on. That material exists today as screenshots, as prose in someone's notes, and as habits.

The work of a migration is turning the setup into files a repository can hold, then proving one job runs from those files and lands through a review. The checklist in this repo does exactly that in six steps.

Kortix is the destination this kit points at, and nothing above depends on that choice. A team that prefers another repo-backed system can run the same six steps and end in the same place: a record it can read, diff and keep.
