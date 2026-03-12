---
name: crux-archiver
description: Archive and visualize key challenges (crux) mentioned by users. Triggered when user types /crux to archive a crux or /crux show to visualize all archived crux as a dark-themed SVG todo list.
---

# Crux Archiver

## Trigger Conditions

This skill activates when:
1. User types `/crux <content>` → Archive the crux
2. User types `/crux show` → Visualize all archived crux as SVG
3. User types `/crux toggle <id>` → Toggle status between open/resolved
4. User types `/crux delete <id>` → Soft delete a crux
5. User types `/crux search <keyword>` → Search crux content
6. User types `/crux clear` → Clear all cruxes (with confirmation)
7. User types `/crux help` → Show usage help

## Archive Format

Each crux record contains:
- `content`: The crux text (string)
- `timestamp`: ISO 8601 UTC timestamp (string)
- `id`: Unique identifier (string, UUID)
- `status`: Current status - "open" or "resolved" (string)
- `deleted`: Soft delete flag (boolean)

## Storage Location

Crux data is stored in JSON format at:
- Windows: `%USERPROFILE%\.qoderwork\crux-data\cruxes.json`
- macOS/Linux: `~/.qoderwork/crux-data/cruxes.json`

## Workflows

### 1. Archive Crux (/crux)

When user types `/crux <content>`:

1. Validate content (not empty, 3-500 chars)
2. Create record: `{id, content, timestamp, status: "open", deleted: false}`
3. Load existing data from storage file
4. Append new record
5. Save back to storage file (with backup)
6. Confirm to user: "✅ 已归档crux #[id]: [content预览]"

### 2. Visualize Crux (/crux show)

When user types `/crux show`:

1. Load all active (non-deleted) crux records from storage
2. If empty: notify user "暂无归档的crux"
3. Generate dark-themed SVG visualization as todo list
4. Resolved items show filled checkbox with checkmark
5. Display SVG to user

### 3. Toggle Status (/crux toggle)

When user types `/crux toggle <id>`:

1. Find crux by id
2. Toggle status: "open" ↔ "resolved"
3. Save changes
4. Confirm: "✅ Crux #[id] 标记为 [status]"

### 4. Delete Crux (/crux delete)

When user types `/crux delete <id>`:

1. Find crux by id
2. Mark as deleted (soft delete)
3. Save changes
4. Confirm: "🗑️ Crux #[id] 已删除"

### 5. Search Crux (/crux search)

When user types `/crux search <keyword>`:

1. Search in content of all active cruxes
2. Display matching results as list

### 6. Clear All (/crux clear)

When user types `/crux clear`:

1. Ask for confirmation: "确定要清空所有crux吗？回复 'yes' 确认"
2. If confirmed: soft delete all cruxes
3. Confirm: "🗑️ 所有crux已清空"

## SVG Design Specification

Dark theme styling:
- Background: `#1a1a2e` (deep navy)
- Card background: `#16213e` (slightly lighter)
- Accent color: `#0f3460` (blue accent)
- Highlight: `#e94560` (coral red for emphasis)
- Text primary: `#eaeaea` (off-white)
- Text secondary: `#a0a0a0` (gray)

Layout:
- Title: "Crux Archive" at top
- Each crux as a todo item with checkbox
- Timestamp displayed in smaller text below content
- Scrollable if list exceeds viewport

## Utility Scripts

Use the provided scripts for data operations:

**List active cruxes:**
```bash
python scripts/storage.py list
```

**Add new crux:**
```bash
python scripts/storage.py add '<content>'
```

**Toggle crux status:**
```bash
python scripts/storage.py toggle <id>
```

**Soft delete crux:**
```bash
python scripts/storage.py delete <id>
```

**Generate SVG:**
```bash
python scripts/visualize.py '<json_array>'
```
