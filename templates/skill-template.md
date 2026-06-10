---
name: your-skill-name
description: "A clear description of what this skill does and when to use it. Include keywords that help agents identify relevant tasks. Use when the user wants to [specific action]."
version: "1.0.0"
license: MIT
compatibility: Hermes Agent 1.0+. Requirements here.
metadata:
  author: Your Name (github.com/yourusername)
  hermes:
    tags: [tag1, tag2, tag3]
    category: development
    # Optional conditional activation:
    # fallback_for_toolsets: [web]
    # requires_toolsets: [terminal]
allowed-tools: Bash(git:*) Read Write
# Optional environment variables:
# required_environment_variables:
#   - name: API_KEY_NAME
#     prompt: Description shown to user
#     help: URL or instructions to get the key
#     required_for: full functionality
---

# Skill Title

Brief intro (1-2 sentences). What does this skill do and why does it exist?

## When to Use

- Trigger condition 1 — specific keywords or phrases the user might say
- Trigger condition 2 — what task the user is trying to accomplish
- Trigger condition 3 — what gap this skill fills

## Procedure

1. **Step one** — what to do first. Be specific. Include exact commands if applicable.
2. **Step two** — main operation. What the skill actually does.
3. **Step three** — format and present results. What the output looks like.
4. **Step four** — verify success. How to confirm it worked.

## Examples

### Example 1: [Scenario Name]
```
Input: [what the user says]
Expected behavior: [what the agent should do step by step]
```

### Example 2: [Scenario Name]
```
Input: [what the user says]
Expected behavior: [what the agent should do step by step]
```

### Example 3: [Edge Case]
```
Input: [edge case input]
Expected behavior: [how the skill handles it]
```

## Pitfalls

- **Known failure mode 1** — what goes wrong and how to handle it
- **Known failure mode 2** — edge case and workaround
- **Known failure mode 3** — common mistake and prevention

## Verification

After running the skill:

- [ ] Expected output was produced
- [ ] No errors in logs
- [ ] Result matches what the user asked for
- [ ] No sensitive data was leaked

## Sources

- Link to official docs
- Link to relevant repos
- Link to related skills
