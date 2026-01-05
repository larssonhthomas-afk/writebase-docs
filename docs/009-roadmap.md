---
layout: default
title: "Roadmap"
nav_order: 9
---

# WriteBase - Roadmap

What is prioritized? This is the current best guess of what we are fixing. If you need anything, please contact us in the Substack community.

This Backlog has a priority 1-3.
1. High (p1)
2. Medium (p2)
3. Low (p3)

# Release 1 - Beta - (p1)

### Marketing

- [x] MARCOM: Article to LinkedIn / Substack "Seeking Gang of 8".
- [x] MARCOM: Video introduction to the app.

### Last fixes before "Gang of 8" (Goal 2026 Q1)

**Major:**

- [ ] TEMPLATE: Create an Airtable Template for WriteBase. (p1)
- [x] DOCUMENTATION: How to get started. (p1)
- [x] APP: Open with url:link to app.writerbase.app/xxx - Verify
- [x] PROJECT: Add, change, remove.
- [ ] APP: Responsive web-app. UI / PWA
- [ ] SEARCH: For documents, tags, and so on.
- [x] [Import-Script for Notion](https://github.com/larssonhthomas-afk/WriteBase-Notion_Import) (very hacky but works)

**Minor:**

- [ ] METADATA: Settings don't save in the local file?
- [ ] SHORTCUTS: Review keyboard shortcuts.
- [] METADATA: Not updated after "New Document".
- [ ] APP: When you load a Workspace, the document list does not load.
- [ ] APP: Title is not visible in Workspace when I need to select.
- [ ] AGENT: JSON Output? Structure.
- [ ] AGENT: JSON Change, focus on the exact text.
- [ ] Verify local settings are saved at app.writebase.app after reopen.

- [x] LICENSE: Not the real logo.
- [x] DOCUMENT-LIST: Filter on Workspace via PROJECTS.
- [x] DOMAIN: Add write.writebase.app to Writing app.
- [x] MARKDOWN: [ ] - does not render correctly in Preview or Publish in Wiki.
- [x] METADATA: Wrong format on Time.      
- [x] METADATA: Show only content in AI fields.
- [x] PUBLISH-WIKI: Remove older page - status?
- [x] Separera Last_Modified (trigger) vs Content_Modified (UI/sortering)
- [x] Separate Last Modified (UI) vs Content Modified (trigger)
- [x] Fix Needs Publish loop - create separate modified fields (Content, Title, Slug, Publish) for trigger formula
- [x] DOCUMENTATION: table.DOCUMENT

### Last fixes before Release 1 - Beta (Goal 2026 Q2)

- [ ] TEST: Bug fixes, regression tests
- [x] PACKAGING: Tauri for Desktop - Tested ok.
- [x] PACKAGING: Vercel for Web - Tested ok.


# Later work and known issues
This is not a bucket list. But for now, our best guess.

## Known issues
- None other than in "Last fixes" above.

## Backlog

- [ ] / as a command (CTRL+K)?
- [ ] Cross-search, use embeddings per document.
- [ ] Reference Database
- [ ] Auto-reference similar job.
- [x] Notes,  connected to a Doc
- [ ] Node,  visualization
- [ ] Mermaid connection
- [ ] Highlight text — send to NOTE.
- [ ] Image upload

## Add Feedback field to Agent runs (Airtable)

- [ ] Collect over time (partly in History and Agent Logs)
- [ ] Manual revision of instruction when it feels right

## Markdown

Later possible markdown for Checkboxes, also see Obsidian.
- [-] ~~Todo 3 (Removed)~~
- [/] Todo 4 (Work in progress)

## Export

- [ ] Export to .docx using only the default format. Word's own defaults only.
- [x] ~~Print styles: no. Raw only.~~
  
## Outline Pane

- [ ] Drag and drop to move sections — unsure. Maybe?

## Agent Polish

- [ ] Toast notifications: "Applied!" / "Text not found" / "Saved."
- [ ] Keyboard shortcuts: Enter = Apply, Esc = Ignore on suggestions.
- [ ] Error handling
- [ ] Show a warning if the text has changed since the run.
- [ ] "Text not found" UI: disable Apply button, show strikethrough.

## Publish  

Integrate additional publication workflows in the future:

- [ ] WordPress
- [ ] Ghost
- [ ] Minor
  


