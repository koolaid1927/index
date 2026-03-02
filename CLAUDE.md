# CLAUDE.md — AI Assistant Guide for `index`

## Repository Overview

This is the `koolaid1927/index` repository. It is currently in its initial setup phase with no application code yet. This document establishes conventions and guidelines for AI assistants contributing to this project.

## Project Structure

```
index/
├── CLAUDE.md          # This file — AI assistant guidelines
└── .git/              # Git repository
```

> **Note:** Update this section as the project grows to reflect the actual directory layout, frameworks, and modules in use.

## Development Setup

### Prerequisites

- Git

### Getting Started

```sh
git clone <repository-url>
cd index
```

> **Note:** Add language runtime, package manager, and dependency installation instructions here once the tech stack is chosen.

## Common Commands

> **Note:** Fill in these sections as build tooling is added to the project.

### Build

```sh
# TBD — add build command
```

### Test

```sh
# TBD — add test command
```

### Lint / Format

```sh
# TBD — add lint and format commands
```

## Git Workflow

- **Default branch:** `main` (to be created with the first commit)
- Write clear, descriptive commit messages summarizing the "why" not just the "what"
- Keep commits focused — one logical change per commit
- Push feature work to feature branches; open pull requests for review

## Code Conventions

> **Note:** Define conventions here once the tech stack and coding standards are established. Consider documenting:
>
> - Language and framework versions
> - Naming conventions (files, variables, functions, classes)
> - Formatting and linting rules
> - Import ordering
> - Error handling patterns
> - Testing expectations (unit, integration, e2e)

## Guidelines for AI Assistants

1. **Read before writing.** Always read existing files before modifying them. Understand context before proposing changes.
2. **Keep it simple.** Make only the changes that are requested or clearly necessary. Avoid over-engineering, unnecessary abstractions, or speculative features.
3. **Don't add noise.** Avoid adding comments, docstrings, or type annotations to code you didn't change, unless explicitly asked.
4. **Respect existing patterns.** Follow the conventions and style already present in the codebase rather than introducing new ones.
5. **Security first.** Never introduce vulnerabilities (injection, XSS, exposed secrets, etc.). Never commit `.env` files or credentials.
6. **Test your changes.** Run the test suite after making changes. Don't mark work as complete if tests are failing.
7. **One concern per commit.** Keep commits atomic and focused on a single logical change.
