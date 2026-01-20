# Skills

A collection of AI skills for coding assistants. Each skill provides contextual documentation and reference material to help AI assistants work with specific tools, libraries, and platforms.

## Available Skills

| Skill | Description |
|-------|-------------|
| [databuddy](./databuddy/) | Privacy-first analytics SDK and REST API integration |

## Structure

Each skill follows a consistent structure:

```
skill-name/
├── SKILL.md           # Main skill definition with metadata, quick start, and overview
└── references/        # Detailed reference documentation
    ├── core.md        # Core concepts and types
    ├── react.md       # Framework-specific guides
    └── ...
```

### SKILL.md Format

The `SKILL.md` file contains YAML frontmatter with metadata:

```yaml
---
name: skill-name
description: Brief description of when to use this skill
metadata:
  author: author-name
  version: "1.0"
---
```

## Usage

These skills are designed to be consumed by AI coding assistants to provide accurate, up-to-date guidance when working with specific technologies.

### Adding a New Skill

1. Create a new directory under the root with your skill name
2. Add a `SKILL.md` file with the required frontmatter and overview content
3. Create a `references/` directory for detailed documentation
4. Break down complex topics into separate reference files
