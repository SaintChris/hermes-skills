---
name: open-source-contribution
description: "Workflow for contributing to external open-source repos. Covers discovery, scoping, writing, tool discipline, PR process, and post-PR follow-up."
version: 2.0.0
author: Alex Bogle (saintlex)
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [Open Source, Contribution, Workflow, DevOps]
    related_skills: [github-umbrella]
---

# Open Source Contribution Workflow

## Purpose
Standard process for contributing to external open-source repositories. Ensures quality, consistency, no sensitive data leaks, and genuine improvement over documentation.

**Core principle:** A profile page alone is documentation, not improvement. Real improvement means setup guides people can actually follow, example workflows that show tools interacting, comparison pages that help readers decide, and cross-references that wire new content into existing decision paths.

---

## Phase 1: Discovery

Before writing anything, check if the repo is worth contributing to:

1. **Check recent activity** — look at recent commits, merged PRs, open issues. Dead repos waste your time.
2. **Find the gap** — scan for missing content, outdated pages, or "good first issue" labels. Don't duplicate what exists.
3. **Check for community** — Discord, Slack, or discussion boards. Ask if the contribution is wanted before building something large.
4. **Read the room** — study the repo's tone, style, and quality bar. Match it exactly.

---

## Phase 2: Pre-Contribution Checklist

1. **Read CONTRIBUTING.md** — every repo has one. Follow it exactly.
2. **Read the repo's templates** — `templates/system-profile.md`, `templates/capability-page.md`, etc. Use them.
3. **Study existing pages** — match writing style, tone, and format. Read at least 3-5 existing profiles before writing yours.
4. **Check for mirrors** — some repos have `ko/` (Korean) or other language directories. Don't touch unless asked.
5. **Scope check** — ask yourself:
   - Does this repo already have something similar?
   - Am I adding a distinct option or duplicating?
   - Is this the right layer/category for this contribution?

---

## Phase 3: Contribution Types

Ranked from simplest to most complex:

| Type | Location | When to use |
|------|----------|-------------|
| Watchlist entry | `watchlist.md` | Track a project not yet fully evaluated |
| Capability/comparison update | `comparisons/`, `capabilities/` | Focused addition to existing decision path |
| Example | `examples/` | Concrete workflow scenario |
| Setup guide | `setup-guides/` | Verified setup path |
| Core solution profile | `solutions/` | Full product/project profile |

**Start small.** A watchlist entry or capability update is better than an unfinished core profile.

---

## Phase 4: Core Profile Requirements

A full solution profile MUST include:

- `solutions/<name>.md` using the repo's template
- Entry in `solutions/README.md`
- Row in `comparisons/capability-matrix.md`
- Row in `comparisons/solution-layers.md`
- Rows in relevant comparison pages (local-vs-cloud, personal-vs-team, setup-burden, agent-access)
- Links from `README.md` lifecycle chooser and solution snapshot

**Conditionally required** (when source-backed and relevant):
- Setup guide under `setup-guides/`
- Example workflow under `examples/`
- Capability pages for workflows the solution actually supports

---

## Phase 5: Writing Rules

- **Factual and specific** — no fluff, no promotional language
- **Use primary sources** — official docs, repos, hands-on testing
- **Mark unknowns as `Unknown`** — never guess
- **Conservative wording** — "maintainer-published benchmarks report..." not "best in class"
- **No sensitive data** — never include API keys, credentials, personal identifiers, email addresses
- **Verify commands** — test all setup steps against live deployment before writing
- **Link, don't duplicate** — point to official docs instead of copying installation instructions

---

## Phase 6: Tool Discipline

### Markdown Tables
- Single `|` at start of table rows, never `||`
- After bulk edits, run `grep -n '^||' file.md` to catch double-pipes
- For bulk markdown edits, use Python string replacement instead of repeated `patch` calls
- Verify table rendering after any edit

### File Writing
- `write_file` has ~8K token limit per call
- For files over ~100 lines, use Python to write via `execute_code`, or break into multiple smaller writes
- Always verify file content after large writes

### Verification
- Test all commands against live deployment before writing setup guides
- Verify file content after every large write
- Check markdown rendering after table edits
- Never include real API keys, credentials, or personal data in public files

---

## Phase 7: PR Process

1. **Create a feature branch** — `git checkout -b <descriptive-name>`
2. **Make changes** — commit with descriptive messages
3. **Push branch** — `git push -u origin <branch>`
4. **Open PR against upstream** — `gh pr create --repo <upstream> --head <your-fork>:<branch>`
5. **PR body must include:**
   - What's new
   - What's updated
   - Verification evidence (what you tested, what commands you ran)
6. **One contribution per PR** — don't bundle unrelated changes

---

## Phase 8: Post-PR

- **Respond to reviews** — address comments promptly, don't take feedback personally
- **When to follow up** — if no response in 7-14 days, a polite comment is fine
- **Handle rejection gracefully** — your fork stays public, the work isn't lost
- **Update your portfolio** — link to the PR (merged or not) as evidence of contribution

---

## Quality Test: "Did I Actually Improve This?"

Before submitting, ask:

- [ ] Does this help a reader make a decision they couldn't make before?
- [ ] Is the setup guide something I verified against a real deployment?
- [ ] Does the example show tools interacting, not just list features?
- [ ] Are cross-references wired into existing decision paths?
- [ ] Would I be comfortable if this was the first page a new reader saw?

If the answer to most of these is "no," you wrote documentation, not improvement. Go deeper.

---

## Repo-Specific Notes

### awesome-second-brain (aristoapp/awesome-second-brain)
- **Fork:** SaintChris/awesome-second-brain
- **Korean mirrors:** `ko/` directory exists — don't touch unless asked
- **Template:** `templates/system-profile.md` for solutions, `templates/capability-page.md` for capabilities
- **Style:** Landscape comparison, not tutorial. Decision-oriented, not instructional.
- **Quality bar:** High. Read 5+ existing profiles before writing. Match their depth.
- **PRs:** #18 (solution profile), #19 (setup guide + examples + comparison)

### chroma (chroma-core/chroma)
- **Fork:** SaintChris/chroma
- **Type:** Technical documentation (vector DB)
- **Audience:** Developers integrating Chroma into applications
- **PR:** Haystack docs integration

---

## Pitfalls (Learned the Hard Way)

1. **Double-pipe markdown** — bulk patching can introduce `||` at line starts. Always verify with `grep`.
2. **Stream timeouts** — large `write_file` calls fail silently. Use Python for big files.
3. **Patch vs Python** — for bulk markdown edits, Python string replacement is more reliable than repeated `patch` calls.
4. **Guessing commands** — never write a setup step you haven't tested. "It should work" doesn't count.
5. **Scope creep** — one contribution per PR. Don't bundle unrelated changes.
6. **Forgetting cross-references** — a profile page without links to comparison pages is incomplete.

---

## Sources

- Created by Alex Bogle (github.com/SaintChris) based on real contributions to awesome-second-brain and chroma.
- Tested against live Hermes Agent v0.16.0 deployment on macOS M1.
