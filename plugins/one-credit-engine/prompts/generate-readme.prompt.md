---
name: 'generate-readme'
description: 'Generate a comprehensive README.md for any project or repository'
agent: 'agent'
model: 'claude-sonnet-4-6'
tools: ['search/codebase', 'read', 'edit', 'web/githubRepo']
---

# Generate README.md

Your goal is to generate a comprehensive `README.md` file for the current project.

## Step 1 — Analyze the project

Use #tool:search/codebase to scan the project structure and identify:
- Project type (library, CLI tool, service, infrastructure module, etc.)
- Primary language and frameworks used
- Entry points, configuration files, and key directories
- Existing documentation or partial README

## Step 2 — Ask for missing context

If any of the following are not determinable from the codebase, ask the user:

- `${input:projectName:Project name (e.g. my-aks-cluster)}`
- `${input:projectDescription:One-sentence description of what this project does}`
- `${input:audience:Target audience (e.g. internal devs, open-source contributors)}`

## Step 3 — Generate README.md

Generate a `README.md` file with the following structure:

### Required sections (always include):
- **Title & badges** — project name, build status if CI config found
- **Description** — what it does, why it exists
- **Prerequisites** — required tools, versions, access rights
- **Installation / Setup** — step-by-step instructions
- **Usage** — basic usage with code examples
- **Configuration** — key environment variables or config files
- **Contributing** — how to contribute (if applicable)
- **License** — license type if found, otherwise omit

### Conditional sections (include only when relevant):
- **Architecture** — if infrastructure or multi-component project detected
- **Deployment** — if Dockerfile, Helm chart, or ArgoCD config found
- **API Reference** — if REST/gRPC endpoints found
- **Troubleshooting** — if known issues or FAQ patterns found in codebase

## Output requirements

- Write in English
- Use proper Markdown: H2 (`##`) for sections, H3 (`###`) for subsections
- Include YAML frontmatter at the top of the README:
```yaml
  ---
  title: <project name>
  description: <one-liner>
  updated: <today's date YYYY-MM-DD>
  ---
```
- Keep code examples in fenced code blocks with language tags
- Do NOT invent information — if unsure, leave a `<!-- TODO: ... -->` placeholder
- Save the output as `README.md` in the project root
