# Skills

A collection of AI skills for coding assistants. Each skill provides contextual documentation and reference material to help AI assistants work with specific tools, libraries, and platforms.

## Available Skills

### Databuddy Skills

| Skill | Description |
|-------|-------------|
| [databuddy](./databuddy/) | Main overview - Privacy-first analytics SDK and REST API integration |
| [databuddy-core](./databuddy/databuddy-core/) | Core browser-side tracking utilities and types |
| [databuddy-react](./databuddy/databuddy-react/) | React/Next.js component and hooks for analytics |
| [databuddy-node](./databuddy/databuddy-node/) | Server-side tracking with batching and middleware |
| [databuddy-flags](./databuddy/databuddy-flags/) | Feature flags for React, Node.js, and Vue |
| [databuddy-ai-vercel](./databuddy/databuddy-ai-vercel/) | LLM observability for Vercel AI SDK |
| [databuddy-api](./databuddy/databuddy-api/) | REST API for querying analytics data |

## Structure

Each skill is a folder containing a `SKILL.md` file:

```
skills/
├── databuddy/
│   ├── SKILL.md                    # Main overview
│   ├── databuddy-core/
│   │   └── SKILL.md
│   ├── databuddy-react/
│   │   └── SKILL.md
│   ├── databuddy-node/
│   │   └── SKILL.md
│   ├── databuddy-flags/
│   │   └── SKILL.md
│   ├── databuddy-ai-vercel/
│   │   └── SKILL.md
│   └── databuddy-api/
│       └── SKILL.md
└── README.md
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
2. Add a `SKILL.md` file with the required frontmatter and comprehensive documentation
3. Include quick start examples, configuration options, and common patterns
4. Reference external documentation when available
