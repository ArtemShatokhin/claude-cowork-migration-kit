# The migration checklist

Kortix is open source, and this checklist is the part of the kit a team actually runs. Six steps, in this order, because the order is what keeps a job from being lost between the vendor's account and yours. Each step names where the work happens and the line that tells you it is finished. The destination is Kortix, the open-source AI Operating System, because the record has to end up in a repository that a diff can describe.

Work through it once for one job. A second pass over the next job is faster, and by the fourth the shape is obvious.

## 1. Inventory what the team ran in Cowork

Open the Claude app and work down the Tasks list and the project list. For each recurring job write down four things: the instructions that define it, the connectors it reaches through, the cadence it runs on, and the person who reads its output. Do not filter yet. A job someone ran twice and abandoned is worth one line, because it tells you what the team thought it needed.

Keep the notes in one markdown file, outside the vendor account. The export article is explicit that on a Team or Enterprise plan the archive covers your own chats and not the contents of files you uploaded, so anything a person typed into a set of instructions has to be copied by hand ([Claude Help Center](https://support.claude.com/en/articles/9450526-export-your-claude-data)).

**Done when** one file lists every task and project with its instructions, connectors, cadence and reader, and that file exists on a disk the team controls.

## 2. Export what Anthropic lets you export

On the web app or Claude Desktop, go to **Settings → Privacy** and click **Export data**. On a Team or Enterprise plan the button appears only after an owner turns on "Allow members to export their own data", and an owner who is not the Primary Owner exports from **Organization settings → Data and privacy** instead ([Claude Help Center](https://support.claude.com/en/articles/9450526-export-your-claude-data)).

Two details matter more than the archive itself. The download link expires 24 hours after delivery, so request it on a day someone is at a desk. And the Team or Enterprise export covers your own chats, not the contents of files you uploaded, so it will not replace step 1.

**Done when** the archive is downloaded, opened once to confirm what it holds, and stored somewhere the team controls rather than only in the account.

## 3. Stand up the owned system

Two routes, and they end in the same place. The managed route is two commands from the [quickstart](https://kortix.com/docs/quickstart):

```bash
curl -fsSL https://kortix.com/install | bash
kortix login
```

The install script supports macOS and Linux on x86_64 and arm64, and on Windows it runs inside WSL.

On your own server, the [self-hosting guide](https://kortix.com/docs/host) installs the CLI and the stack. Run it on a host with a public IP, A and AAAA records pointed at the server, and ports 80 and 443 open. Then:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com --admin-email you@example.com
kortix self-host start
```

The self-hosting guide names the one thing people skip: sign up as the admin as soon as the stack answers, because until `EMAIL_URL` or `DISABLE_SIGNUP=true` is set, anyone who reaches the instance can create a confirmed account. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free.

**Done when** `kortix doctor` exits 0 on the managed route, or `kortix self-host doctor` reports no failing check on your own server. The quickstart describes what the first command does: it checks your login and the project, starts a throwaway session, waits for its sandbox, sends a ping and deletes the session, exiting 1 if any check fails.

## 4. Move the agent config into the repo

A project is a git repository with a `kortix.yaml` at its root ([quickstart](https://kortix.com/docs/quickstart)). Create one from the starter:

```bash
kortix init my-agent
cd my-agent
```

Inside that directory, write one agent file per job from the step 1 notes. The instructions are the body of that file, and the mode and permission rules sit in its frontmatter. Then declare the agent in the manifest, which is where its grants live:

```yaml
agents:
  weekly-brief:
    file: agents/weekly-brief.md
    connectors: all
    secrets: all
    kortix_permissions: all
    skills: all
```

That is the shape the starter ships in `packages/starter/templates/base/kortix.yaml` in [Kortix on GitHub](https://github.com/kortix-ai/suna), with the agent renamed. The starter grants `all` so a new project is capable out of the box, and the manifest's own comment says an omitted grant resolves to none. Start wide, then take a line down to the one connector or skill the job actually uses.

Validate and push with `kortix ship`, which validates `kortix.yaml`, commits, asks for missing secrets, pushes the current branch and asks you to connect the declared connectors.

**Done when** the project repository has a commit that adds the agent file and its manifest block, and `kortix ship` has pushed it.

## 5. Set the review gate

Decide who reads and merges, and write the names down before the first session runs. The mechanism is in the docs: an agent declared in `kortix.yaml` merges only when its `kortix_permissions` include `project.gitops.merge`, and without that grant the merge returns 403 with the code `agent_scope_insufficient` ([quickstart](https://kortix.com/docs/quickstart)). Session work reaches `main` through a change request. Merge is default-deny for agents.

The reviewer's loop, from the same page, run from inside the clone:

```bash
kortix cr ls          # open change requests
kortix cr diff 1      # the unified diff
kortix cr merge 1     # merge into the base branch
git pull              # bring the merged work into your clone
```

To send work back instead, `kortix cr request-changes 1 --message "…"` puts the note into the change request's session. A review queue with no named owner is a queue nobody reads.

**Done when** each agent file names the person who merges its change requests, the grant list on that agent excludes `project.gitops.merge` unless the team decided otherwise, and everyone knows to run `kortix cr diff` before `kortix cr merge`.

## 6. Prove one piece of real work end to end

Pick the job with the clearest output, usually the weekly report. Run it from the repo:

```bash
kortix sessions new --prompt "Draft the weekly status report from the notes in memory/"
```

A session works on its own branch, named after the session. When it finishes, ask the agent to open a change request, or open one yourself with `kortix cr open --head <session_id> --session <session_id> --title "Weekly status report"`. Then run step 5's loop on it.

**Done when** the deliverable sits in the repository at a commit that came through a merged change request, the change request is closed, and a person other than the author has read the diff.

## After the sixth step

The first job is the template. Repeat steps 1 and 4 for the next one, and let step 6 do the arguing: a merged change request with a named reader behind it is the demonstration that the record now lives somewhere the team can read. The remaining decisions are operational, and the self-hosting guide covers them: DNS for previews, backups of the instance directory, the update channel, and closing sign-up once the team is in.
