---
layout: default
title: "table.DOCUMENT"
nav_order: 50
---

# table.DOCUMENT

Baserow table for storing documents in WriteBase.

## Required Fields

| Field | Type | Purpose |
|-------|------|---------|
| Title | Single line text | Document name |
| Content | Long text | Markdown content |
| PROJECT | Link to PROJECT | Groups documents |
| WORKSPACE | Link to WORKSPACE | **Used for filtering** |
| Favorite | Checkbox | Quick access in sidebar |

## Filtering

Documents are fetched server-side using the WORKSPACE field:

```
filterByFormula=FIND("recXXX", ARRAYJOIN(WORKSPACE))
```

**Every document must have WORKSPACE set** to appear in the editor.

## Optional Fields

| Field | Type |
|-------|------|
| Last_Modified | Last modified time |
| Last_Modified_Content | Last modified time |
| Status | Single select |
| Slug | Formula |
| Type | Single/Multiple select |
