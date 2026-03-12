# Crux Archiver

> Qoder Skill for archiving and visualizing key challenges

## What is this?

Crux Archiver is a Qoder Skill that helps you capture and track important challenges (crux) in your work and thinking. It provides:

- **Simple archiving**: Type `/crux <content>` to save a challenge
- **Visual overview**: `/crux show` generates a dark-themed SVG todo list
- **Status tracking**: Toggle between "open" and "resolved"
- **Soft delete**: Safe removal with 30-day recovery

## Installation

```bash
# Via skills.sh
npx skills add stowisdom/qoder-skill-crux-archiver

# Or manual install
cd ~/.qoderwork/skills
git clone https://github.com/stowisdom/qoder-skill-crux-archiver.git crux-archiver
```

## Commands

| Command | Action |
|---------|--------|
| `/crux <content>` | Archive a new crux |
| `/crux show` | Visualize all cruxes as SVG |
| `/crux toggle <id>` | Toggle status open/resolved |
| `/crux delete <id>` | Soft delete a crux |
| `/crux search <keyword>` | Search crux content |
| `/crux clear` | Clear all (with confirmation) |
| `/crux help` | Show usage help |

## Data Storage

- **Windows**: `%USERPROFILE%\.qoderwork\crux-data\cruxes.json`
- **macOS/Linux**: `~/.qoderwork/crux-data/cruxes.json`

## Example

```
> /crux 如何在干扰环境中保持深度工作？

✅ 已归档crux #a1b2c3d4: 如何在干扰环境中保持深度工作？

> /crux show

[SVG visualization appears]
```

## License

MIT
