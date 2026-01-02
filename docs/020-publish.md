---
layout: default
title: "PUBLISH"
nav_order: 20
---

# PUBLISH

Publish documents from Airtable to the web automatically with Github Pages.

## Overview

The PUBLISH system connects your Airtable documents to GitHub Pages. When you check the Publish box, your document appears on the web within minutes.

**Flow:**

```
DOCUMENT (Airtable)
    ↓
Automation triggers script
    ↓
Script pushes to GitHub
    ↓
GitHub Pages builds site
    ↓
Live on the web
```

**Key components:**

| Component | Role |
|-----------|------|
| CHANNEL | Defines where to publish (repo, path) |
| DOCUMENT | Your content + publish settings |
| Script | Moves content from Airtable to GitHub |
| GitHub Pages | Hosts the website |

---

## CHANNEL table

Each channel is a publishing destination.

| Field | Type | Purpose |
|-------|------|---------|
| Name | Text | Channel identifier (e.g. "Wiki", "Landing") |
| Platform | Select | GitHub-Pages, Substack, etc. |
| API_Owner | Text | GitHub username |
| API_Repo | Text | Repository name |
| API_Path | Text | Folder path (e.g. "docs") |

**Example:**

| Name | Platform | API_Owner | API_Repo | API_Path |
|------|----------|-----------|----------|----------|
| Wiki | GitHub-Pages | myuser | writebase-docs | docs |
| Landing | GitHub-Pages | myuser | writebase-landing | (empty) |

---

## DOCUMENT fields for publishing

These fields control how and when a document is published.

| Field | Type | Purpose |
|-------|------|---------|
| Publish | Checkbox | Should this be live on the web? |
| Slug | Text | URL-friendly filename (e.g. `010-getting-started`) |
| Published_Slug | Text | Last published slug (set by script) |
| Wiki_Order | Number | Sort order in navigation |
| CHANNEL | Link | Which channel to publish to |
| Needs_Publish | Formula | Triggers automation when true |
| Last_Modified | Last modified time | When document was last changed |
| Last_Published | Date & time | When document was last published |
| Publish_Log | Long text | History of publish actions |

**Needs_Publish formula:**

```
OR(
  {Last_Published} = BLANK(),
  {Last_Modified} > {Last_Published}
)
```

This triggers publishing when:
- Document has never been published, or
- Document was modified after last publish

---

## Slug format

Slugs follow the pattern: `XXX-title-in-lowercase`

| Wiki_Order | Title | Slug |
|------------|-------|------|
| 0 | Home | `000-index` |
| 10 | Getting Started | `010-getting-started` |
| 20 | Publishing | `020-publish` |

The three-digit prefix ensures correct sort order in navigation.

**Slug rules:**
- Lowercase
- Hyphens instead of spaces
- No special characters
- Max 50 characters

---

## Script

The script runs as an Airtable Automation and pushes documents to GitHub.

**Automation setup:**

| Setting | Value |
|---------|-------|
| Trigger | When record matches conditions |
| Condition | Needs_Publish = true |
| Action | Run script |

**Input variables:**

| Variable | Field |
|----------|-------|
| recordId | Record ID |
| title | Title |
| content | Content |
| slug | Slug |
| order | Wiki_Order |
| publishLog | Publish_Log |
| channelPlatform | Channel → Platform (lookup) |
| apiOwner | Channel → API_Owner (lookup) |
| apiRepo | Channel → API_Repo (lookup) |
| apiPath | Channel → API_Path (lookup) |
| publish | Publish |
| publishedSlug | Published_Slug |

---

## Secrets

Scripts need authentication to push to GitHub. Airtable Automations handles this securely with Secrets.

**Required secret:**

| Secret name | Value |
|-------------|-------|
| githubToken | GitHub Personal Access Token |

**Creating the token:**

1. Go to github.com → Settings → Developer settings
2. Personal access tokens → Tokens (classic)
3. Generate new token
4. Select scopes: `repo` (full control)
5. Copy token (shown only once)

**Adding to Airtable:**

1. Open your Automation
2. Edit the Script action
3. Click "Add secret"
4. Name: `githubToken`
5. Value: paste your token

**In the script:**

```javascript
const GITHUB_TOKEN = await input.secret('githubToken');
```

The token is never visible in logs or code. Only Airtable's secure vault can access it.

---

## How it works

**Publishing a document:**

1. You check `Publish = ✓` on a document
2. `Needs_Publish` formula returns true
3. Automation triggers
4. Script reads document content
5. Script pushes markdown file to GitHub
6. Script updates `Last_Published` and `Published_Slug`
7. GitHub Pages rebuilds site
8. Document is live

**Unpublishing a document:**

1. You uncheck `Publish = ☐`
2. `Needs_Publish` formula returns true
3. Script deletes file from GitHub
4. Document is removed from site

**Changing a slug:**

1. You change the Slug field
2. Script compares `Slug` vs `Published_Slug`
3. If different: deletes old file, creates new file
4. Updates `Published_Slug` to new value

---

## Getting started

**Step 1: Create a CHANNEL**

Add a record to the CHANNEL table:
- Name: `Wiki`
- Platform: `GitHub-Pages`
- API_Owner: your GitHub username
- API_Repo: your repository name
- API_Path: `docs` (or empty for root)

**Step 2: Set up GitHub repository**

1. Create a new repository on GitHub
2. Enable GitHub Pages (Settings → Pages → Source: main branch)
3. Add MkDocs configuration if using wiki format

**Step 3: Create the Automation**

1. New automation in Airtable
2. Trigger: When record matches conditions
3. Table: DOCUMENT
4. Condition: Needs_Publish = true
5. Action: Run script
6. Paste the publish script
7. Add secret: `githubToken`
8. Configure input variables

**Step 4: Publish a document**

1. Create or select a document
2. Link it to your CHANNEL
3. Set a Slug (e.g. `010-my-first-post`)
4. Check `Publish = ✓`
5. Wait for automation to run
6. Visit your GitHub Pages site

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| Document not publishing | Needs_Publish = false | Check Last_Modified vs Last_Published |
| 404 on site | Wrong slug or path | Verify Slug and API_Path |
| SHA conflict error | File changed during push | Run automation again |
| Wrong channel | CHANNEL link incorrect | Update CHANNEL field |

---

## Script versions

| Version | Date | Changes |
|---------|------|---------|
| v1.4.2 | 2026-01-02 | Index file renamed to index.md |
| v1.4.1 | 2025-12-31 | Renamed isPublished to publish |
| v1.4.0 | 2025-12-31 | Published_Slug tracking |
| v1.3.0 | 2025-12-31 | Unpublish support |
| v1.2.0 | 2025-12-29 | Empty API_Path support |
