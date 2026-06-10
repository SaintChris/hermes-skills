# Writing Great Skills for HermesHub

Based on the [HermesHub submission guide](https://hermeshub.xyz) and real contribution experience.

## The Standard

Every skill submitted to HermesHub must follow the [agentskills.io](https://agentskills.io/specification) open standard and pass automated security review.

### Required Frontmatter

```yaml
---
name: your-skill-name
description: "Clear description with keywords for matching"
version: "1.0.0"
license: MIT
compatibility: Requirements
metadata:
  author: Your Name (github.com/username)
  hermes:
    tags: [tag1, tag2]
    category: development
allowed-tools: Bash(git:*) Read Write
---
```

### Security Requirements

**Automatic rejection triggers:**
- Curl/wget to external URLs with system data (exfiltration)
- Base64-encoded or obfuscated shell commands
- Instructions to bypass security prompts
- Downloading and executing binaries from external URLs
- Hidden instructions in referenced files
- Prompt injection or jailbreak attempts

**Required for approval:**
- All environment variables documented with setup instructions
- No hardcoded credentials, tokens, or API keys
- Destructive operations require explicit user confirmation
- Network access patterns documented and justified
- File system access scoped to relevant directories
- Publisher identity verified via GitHub account

## Writing Best Practices

### 1. Progressive Disclosure

- **Description field:** ~100 tokens. Keywords for matching. What it does + when to use it.
- **SKILL.md body:** Under 5000 tokens. Core instructions only.
- **Reference files:** Detailed docs loaded on demand.

### 2. Clear Trigger Conditions

The "When to Use" section determines when the agent loads your skill. Include specific keywords and phrases users might say.

**Bad:** "Use when the user needs help"
**Good:** "Use when the user says 'publish to devto', 'share this article', or 'cross-post to multiple platforms'"

### 3. Structured Procedures

Number your steps. Each step should be a concrete action the agent can take. Include exact commands, API calls, or code patterns.

**Bad:** "Publish the article somehow"
**Good:** "1. Parse the article file for frontmatter. 2. POST to `https://dev.to/api/articles` with the article payload. 3. Return the article URL."

### 4. Document Failure Modes

The "Pitfalls" section prevents wasted time. Document common errors, edge cases, and workarounds. Skills that handle errors gracefully get higher ratings.

### 5. Include Verification

Tell the agent how to confirm success. This closes the loop and enables the self-improvement cycle.

```markdown
## Verification
- [ ] Article URL returned and accessible
- [ ] Content renders correctly
- [ ] No errors in logs
```

### 6. Conditional Activation

Use `fallback_for_toolsets` to hide your skill when premium tools are available, or `requires_toolsets` to only show it when needed tools exist. This keeps the skill list clean.

## Trust Levels

| Level | Source | Policy |
|-------|--------|--------|
| Verified | HermesHub reviewed and approved | Full security scan passed |
| Community | Community-submitted via PR | Automated scan + basic review |
| Unverified | Direct GitHub link | Use `--force` to install, at your own risk |

## Submission Process

1. **Fork** the [hermeshub repo](https://github.com/amanning3390/hermeshub)
2. **Create** your skill under `skills/<skill-name>/SKILL.md`
3. **Test** locally — copy to `~/.hermes/skills/` and verify it works
4. **Open a PR** — automated security scanner runs on every PR
5. **Review and merge** — after passing security scan + code review, skill goes live on hermeshub.xyz

## Common Mistakes

1. **Missing `allowed-tools`** — HermesHub requires declared tool access for security review
2. **Hardcoded credentials** — use `required_environment_variables` instead
3. **Vague trigger conditions** — be specific about when the skill should activate
4. **No examples** — include at least 2-3 concrete examples with input/output
5. **Missing verification** — always tell the agent how to confirm success
6. **Too long** — keep SKILL.md under 5000 tokens. Use reference files for detailed docs.
