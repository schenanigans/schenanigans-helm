# Development Tooling

This repository uses automated tooling for code quality and changelog generation.

## Tools

### Husky

Git hooks for running checks before commits.

### Lint-Staged

Runs linters only on staged files for faster commits.

### Prettier

Code formatter for YAML and Markdown files.

### yamllint

YAML linting to catch syntax errors.

### git-cliff

Automated changelog generation from git history.

## Setup

Install dependencies:

```bash
npm install
```

Install system tools (macOS):

```bash
brew install yamllint git-cliff
```

## Usage

### Format code

```bash
npm run format
```

### Check formatting

```bash
npm run lint
```

### Check YAML syntax

```bash
npm run lint:yaml
```

### Generate changelog

```bash
npm run changelog
```

## Pre-commit Hook

The pre-commit hook automatically runs Prettier on staged YAML and Markdown files.
Files are automatically formatted before commit.

## Bypass Hooks

If you need to bypass hooks (not recommended):

```bash
git commit --no-verify
```
