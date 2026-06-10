# Platform Picker — API Reference

## Dev.to API

### Create Article
```
POST https://dev.to/api/articles
Headers: { "api-key": "YOUR_KEY", "Content-Type": "application/json" }
Body: { "article": { "title": "...", "published": true, "body_markdown": "...", "tags": [...] } }
```

### Get My Articles
```
GET https://dev.to/api/articles/me
Headers: { "api-key": "YOUR_KEY" }
```

**Rate limits:** 10 articles/hour for new accounts.
**Max tags:** 4 per article (422 error if exceeded).
**Get key:** https://dev.to/settings/extended

## GitHub API

### Create Gist
```
POST https://api.github.com/gists
Headers: { "Authorization": "Bearer TOKEN" }
Body: { "description": "...", "public": true, "files": { "name.md": { "content": "..." } } }
```

### Create/Update File
```
PUT https://api.github.com/repos/{owner}/{repo}/contents/{path}
Headers: { "Authorization": "Bearer TOKEN" }
Body: { "message": "...", "content": "base64encoded" }
```

**Required scopes:** `repo`, `gist`, `read:user`
**Get token:** https://github.com/settings/tokens

## LinkedIn API

### Create UGC Post
```
POST https://api.linkedin.com/v2/ugcPosts
Headers: { "Authorization": "Bearer TOKEN", "X-Restli-Protocol-Version": "2.0.0" }
Body: { "author": "urn:li:person:...", "lifecycleState": "PUBLISHED", ... }
```

**Max post length:** 3000 chars for text posts.
**Note:** Requires person URN lookup via `GET /v2/me` first.

## HermesHub

### Submit Skill
```
Web: https://hermeshub.xyz/submit
Auth: GitHub OAuth
Process: OAuth → select repo → security scan → publish
```

**Security scanning:** 65+ threat rules. Skills with hardcoded secrets, prompt injection patterns, or destructive commands are blocked.
**Payouts:** 95% to creators via x402 protocol.
