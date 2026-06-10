---
name: platform-picker
description: "Publish and share content across multiple platforms (Dev.to, GitHub, LinkedIn, HermesHub) from one place. Pick your platform, provide API key/token once, then publish anywhere."
version: 1.0.0
author: Alex Bogle (saintlex)
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [Publishing, Sharing, Multi-Platform, Automation]
    related_skills: [open-source-contribution]
---

# Platform Picker — Publish Anywhere

## Purpose
Publish and share content across multiple platforms from one place. Store API keys/tokens once, then pick where to publish each time.

**Supported platforms:**
- **Dev.to** — articles, blog posts (API key)
- **GitHub** — repos, gists, README updates (PAT / OAuth)
- **LinkedIn** — articles, posts (OAuth token)
- **HermesHub** — skill publishing (GitHub OAuth)

---

## Setup: Store Your Credentials

Run the setup command for each platform you want to use:

```bash
# Dev.to
python3 ~/.hermes/scripts/platform_picker.py setup devto --api-key YOUR_API_KEY

# GitHub
python3 ~/.hermes/scripts/platform_picker.py setup github --token YOUR_PAT

# LinkedIn
python3 ~/.hermes/scripts/platform_picker.py setup linkedin --token YOUR_OAUTH_TOKEN

# HermesHub (uses GitHub OAuth — no separate key needed)
python3 ~/.hermes/scripts/platform_picker.py setup hermeshub
```

Credentials are stored in `~/.hermes/config.yaml` under `platforms:` section.

---

## Usage: Publish Content

### Publish an article
```bash
# Pick platform interactively
python3 ~/.hermes/scripts/platform_picker.py publish --file article.md

# Publish to specific platform
python3 ~/.hermes/scripts/platform_picker.py publish --file article.md --platform devto

# Publish to multiple platforms
python3 ~/.hermes/scripts/platform_picker.py publish --file article.md --platform devto --platform linkedin
```

### Publish a skill to HermesHub
```bash
python3 ~/.hermes/scripts/platform_picker.py publish-skill --skill-path ~/.hermes/skills/devops/open-source-contribution/
```

### Check which platforms are configured
```bash
python3 ~/.hermes/scripts/platform_picker.py status
```

---

## Platform Details

### Dev.to
- **Auth:** API key (stored in config)
- **Endpoint:** `POST /api/articles`
- **Supports:** title, body_markdown, tags, published, series
- **Get key:** https://dev.to/settings/extended

### GitHub
- **Auth:** Personal Access Token (PAT) or OAuth
- **Supports:** repos, gists, README updates, file commits
- **Scopes needed:** `repo`, `gist`, `read:user`
- **Get token:** https://github.com/settings/tokens

### LinkedIn
- **Auth:** OAuth 2.0 token
- **Supports:** articles, text posts, image posts
- **Endpoint:** `POST /v2/ugcPosts`
- **Get token:** https://www.linkedin.com/developers/apps

### HermesHub
- **Auth:** GitHub OAuth (no separate key)
- **Supports:** skill publishing with security scanning
- **Site:** https://hermeshub.xyz
- **Process:** GitHub OAuth → submit skill → automated scan → publish

---

## Credential Storage

Credentials are stored in `~/.hermes/config.yaml`:

```yaml
platforms:
  devto:
    api_key: "your-api-key"
  github:
    token: "your-pat"
  linkedin:
    token: "your-oauth-token"
  hermeshub:
    enabled: true
```

**Security notes:**
- Never hardcode credentials in skills or scripts
- Use `config.yaml` or environment variables
- Tokens are never logged or displayed in output
- Each platform uses its own auth method — no shared secrets

---

## Pitfalls

1. **Dev.to rate limits** — max 10 articles/hour for new accounts
2. **LinkedIn token expiry** — OAuth tokens expire, need refresh
3. **GitHub PAT scope** — make sure token has the right scopes for what you need
4. **HermesHub security scan** — skills with hardcoded secrets or suspicious patterns get rejected
5. **Markdown differences** — each platform handles markdown slightly differently. Dev.to supports full markdown, LinkedIn is limited, GitHub has its own flavor.

---

## Sources

- Dev.to API docs: https://developers.forem.com/api
- GitHub API docs: https://docs.github.com/en/rest
- LinkedIn API docs: https://learn.microsoft.com/en-us/linkedin/
- HermesHub: https://hermeshub.xyz
