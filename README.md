# Hermes Skills

Community skills for [Hermes Agent](https://hermes-agent.nousresearch.com/) by Nous Research. Open source workflows for contributing to repos, publishing content across platforms, and more.

## Skills

| Skill | Description | Install |
|-------|-------------|---------|
| `open-source-contribution` | Complete workflow for contributing to external repos + publishing across platforms (Dev.to, GitHub, LinkedIn). Discovery, scoping, writing, tool discipline, PR process, post-PR, and multi-platform publishing. | `hermes skills install github:SaintChris/hermes-skills/skills/devops/open-source-contribution` |

## Installation

### Via Hermes CLI
```bash
hermes skills install github:SaintChris/hermes-skills/skills/devops/open-source-contribution
```

### Manual
```bash
# Clone the repo
git clone https://github.com/SaintChris/hermes-skills.git

# Copy skill to your Hermes skills directory
cp -r hermes-skills/skills/devops/open-source-contribution ~/.hermes/skills/devops/

# Copy the platform picker script
cp hermes-skills/scripts/platform_picker.py ~/.hermes/scripts/
chmod +x ~/.hermes/scripts/platform_picker.py
```

## Platform Picker

The open-source-contribution skill includes a platform picker for publishing content across multiple platforms.

### Setup (one-time per platform)
```bash
# Dev.to
python3 ~/.hermes/scripts/platform_picker.py setup devto --api-key YOUR_KEY

# GitHub
python3 ~/.hermes/scripts/platform_picker.py setup github --token YOUR_PAT

# Check status
python3 ~/.hermes/scripts/platform_picker.py status
```

### Publishing
```bash
# Publish an article to Dev.to
python3 ~/.hermes/scripts/platform_picker.py publish --file article.md --platform devto

# Publish to multiple platforms
python3 ~/.hermes/scripts/platform_picker.py publish --file article.md --platform devto --platform linkedin
```

### Supported Platforms
| Platform | Auth | What it publishes |
|----------|------|-------------------|
| Dev.to | API key | Articles with full markdown |
| GitHub | PAT | Gists, repo files |
| LinkedIn | OAuth token | Text posts (3000 char limit) |
| HermesHub | GitHub OAuth | Skills (via web) |

### Credential Storage
API keys and tokens are stored in `~/.hermes/config.yaml` under the `platforms:` section. Never hardcoded in scripts or skills.

```yaml
platforms:
  devto:
    api_key: "your-key"
  github:
    token: "your-pat"
  linkedin:
    token: "your-token"
```

## Contributing

These skills are open source (MIT). Contributions welcome:

1. Fork the repo
2. Add your skill under `skills/<category>/<skill-name>/`
3. Include a `SKILL.md` following the [Hermes skill format](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills)
4. Submit a PR

## Author

**Alex Bogle** — [@SaintChris](https://github.com/SaintChris) · [saintlex.sbs](https://saintlex.sbs) · [Dev.to](https://dev.to/saintchris_21)

Built and documented from Jamaica.
